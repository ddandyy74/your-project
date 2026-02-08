# TOOLS.md - 工具规则与硬约束

本文件记录项目使用的工具、环境配置和硬约束规则。

## 开发环境

| 工具 | 版本 | 用途 |
|------|------|------|
| Node.js | >=18.x | 运行时环境 |
| npm/yarn | 最新版 | 包管理 |
| Git | 最新版 | 版本控制 |

## IDE 配置

推荐使用 VS Code，配置以下扩展：
- ESLint
- Prettier
- GitLens

## 硬约束

### 代码风格
- 使用 ESLint + Prettier 进行代码格式化
- 提交前必须通过 lint 检查

### Git 规范
- 分支命名: `feature/*`, `bugfix/*`, `hotfix/*`
- Commit message 格式: `type(scope): description`
- 必须通过 CI 才能合并

### 测试要求
- 单元测试覆盖率 >= 80%
- 集成测试覆盖核心流程

## 快捷命令

```bash
# 安装依赖
npm install

# 开发启动
npm run dev

# 代码检查
npm run lint

# 运行测试
npm run test

# 构建
npm run build

# 部署
npm run deploy
```
