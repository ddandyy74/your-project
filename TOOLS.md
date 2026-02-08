# TOOLS.md — Novel World Sandbox Engine 工具使用规则（配合 AGENTS.md）

> 目标：让“角色分工”变成工具层面的硬约束：
> - PM 不写、不跑、不部署
> - DEV 才能改代码并跑测试
> - OPS 只能部署验证且禁止写入
> - QA 只读检查、审计合规，不写不跑
>
> 注意：本文件是**规则说明**；要做到“强制”，请把对应 allow/deny 写入
> `~/.openclaw/openclaw.json`（工具策略以 deny 优先）。

---

## 1) 统一红线（适用于所有角色）

- 禁止执行你不理解的命令；
- 禁止从第三方复制粘贴  
  `curl | bash` / `powershell iwr … | iex` 等远程执行脚本；
- 禁止安装 / 启用来源不明的 skills / 插件；
- 任何新增 tool / hook / 自动化能力，必须由 **PM 明确审批**；
- 任何涉及：
  - 凭据 / 密钥
  - 生产环境
  - 对外发布 / 上线  
  **必须明确写入 PM 派发的工单**（见 AGENTS.md §4）。

---

## 2) 按角色划分的工具权限（行为规则）

### 2.1 PM（主会话 / 项目经理）

允许：
- 只读：读取文档 / 代码（read）
- 调度：
  - 创建 / 管理子智能体
  - 转发与汇总消息  
  （sessions_spawn / sessions_list / sessions_history / sessions_send 等）

禁止：
- 任何写入仓库文件的操作  
  （write / edit / apply_patch）
- 任何执行命令  
  （exec / process）
- 任何部署 / 发布动作

> PM 只能 **“看 + 想 + 派 + 审”**，不能 **“写 + 跑 + 上”**。

---

### 2.2 DEV（临时开发智能体）

允许：
- 读写代码  
  （write / edit / apply_patch）
- 执行构建 / 测试命令  
  （exec / process，仅限工作区内）
- 生成 patch / diff / commit 作为交付物

要求：
- 所有执行过的命令与关键输出，必须在回报中记录

禁止：
- 未经工单授权的部署 / 发布
- 生成更多子智能体（禁止嵌套扇出）

---

### 2.3 OPS（部署智能体）

允许：
- 执行部署 / 验证命令  
  （exec / process）
- 读取日志与配置  
  （read）

禁止（必须硬禁）：
- 任意写操作  
  （write / edit / apply_patch）
- 通过 shell 修改代码或配置
- 安装插件 / 改配置 / 改 hook

失败处理（强制）：
- 失败只回报：
  - 失败阶段
  - 原始错误
  - 日志范围
  - 复现命令
- 回报后 **立即进入静默等待**
- 不得自行重试、不得自行修复

---

### 2.4 QA（检查 / 合规审计智能体）

定位：
- QA 是 **只读审计角色**
- 负责检查：合规性 / 完整性 / 可用性
- 不参与实现、不参与修复、不参与部署

允许：
- read  
  （读取代码 / 配置 / 文档 / 日志 / 测试输出）
- （可选）exec / process：
  - **仅当 PM 工单中明确授权**
  - 仅用于“本地可复现的检查 / 测试命令”
  - 不得触发部署 / 发布 / 状态写入

禁止（必须硬禁）：
- write / edit / apply_patch（任何写入）
- 通过 shell 修改文件或配置
- sessions_spawn（禁止 QA 再生成子智能体）
- 未经 PM 明确指令的重复检查或扩大审计范围

### QA 的会话行为约束（工具层配合 AGENTS.md）

- QA 在提交检查回报后：
  - **不得继续使用任何工具**
  - **必须进入静默等待状态**
- QA 只能在收到 PM 的明确指令后恢复工作：
  - 例如：“请对修复结果重新审计”
- QA **不得自行退出会话**
- QA 不得自行开启新一轮检查

> 工具层设计目标：  
> **QA 在“回报之后”没有任何合法可执行动作，只能等待 PM 调度。**

---

## 3) 强制并行上限（管理规则）

- 同时最多 **2 个“工作中”智能体**
- 额外允许 **1 个“静默备份”智能体**
- 静默等待中的 OPS / QA：
  - 不计入“工作中”名额
  - 只有 PM 指令才能重新激活

---

## 4) 推荐 openclaw.json（可选，但强烈建议用于“硬约束”）

> 示例治理结构：
> - main = PM
> - dev  = DEV
> - ops  = OPS
> - qa   = QA

```json
{
  "agents": {
    "list": [
      {
        "id": "main",
        "tools": {
          "allow": [
            "read",
            "sessions_spawn",
            "sessions_list",
            "sessions_history",
            "sessions_send"
          ]
        }
      },
      {
        "id": "dev",
        "tools": {
          "allow": [
            "read",
            "write",
            "edit",
            "apply_patch",
            "exec",
            "process"
          ],
          "deny": ["sessions_spawn"]
        }
      },
      {
        "id": "ops",
        "tools": {
          "allow": ["read", "exec", "process"],
          "deny": [
            "write",
            "edit",
            "apply_patch",
            "sessions_spawn"
          ]
        },
        "sandbox": {
          "mode": "all",
          "workspaceAccess": "ro"
        }
      },
      {
        "id": "qa",
        "tools": {
          "allow": ["read"],
          "deny": [
            "write",
            "edit",
            "apply_patch",
            "exec",
            "process",
            "sessions_spawn"
          ]
        }
      }
    ]
  }
}
