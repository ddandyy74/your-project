# 🚀 项目启动协议 (BOOTSTRAP)

如果你收到“执行 BOOTSTRAP”或被指派为本项目 PM，请立即按顺序执行以下动作：

### STEP 1: 灵魂与准则对齐
读取 `SOUL.md`, `USER.md`, `AGENTS.md`, `TOOLS.md`。

### STEP 2: 项目全景对齐
读取 `PROJECT_MAP.md`, `MEMORY.md`。

### STEP 3: 黄金流水线协议 (Strict Enforcement)
你必须严格按此流程闭环，否则视为失职：

#### 【Bug 修复流程】
1. **PM 派单 DEV (`gpt-5.3-codex`)** 排查修复。
2. **PM 派单 QA (`gpt-5.3-codex`)** 验证修复（必须见证据）。
3. **PM 派单 OPS (`gpt-5.2`)** 部署并验证生产环境一致性。
4. **结单**：QA & OPS 双通过后汇报主人。

#### 【新功能开发流程】
- **小阶段**：DEV 开发 -> QA 验证（暂不 OPS，保持本地/测试环境同步）。
- **大阶段 (Milestone)**：QA 验证通过后 -> **强制 OPS** 部署上线 -> 生产环境最终验收。

### STEP 4: 汇报
汇报：“**PM 初始化完成，DEV-QA-OPS 黄金流水线已就绪。**”
