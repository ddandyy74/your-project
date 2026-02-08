# 04_tech_stack.md - 技术栈与约束

> **备注**: docs/ ⭐⭐ 重要
> 技术栈与约束，语言/框架/平台/版本（DEV 编程参考）

## 技术选型

| 层级 | 技术 | 版本 | 用途 |
|------|------|------|------|
| 前端 | [React/Vue] | >=18.x | UI 框架 |
| 后端 | [Node/Python/Go] | 最新 LTS | 服务端 |
| 数据库 | [PostgreSQL/MySQL] | >=14 | 主数据库 |
| 缓存 | [Redis] | >=7 | 缓存层 |
| 部署 | [Docker/K8s] | 最新 | 容器化 |

## 开发环境要求

```bash
# 最低版本要求
Node.js >= 18.x
npm >= 9.x 或 yarn >= 1.x
Git >= 2.x
```

## 项目约束

### 语言规范

- JavaScript/TypeScript 使用 ESLint + Prettier
- Python 使用 Black + isort
- 代码注释使用英文

### 框架约束

- React 函数式组件 + Hooks
- 后端 RESTful API 设计
- 数据库使用 ORM 框架

### 安全约束

- 敏感信息使用环境变量
- API 必须认证授权
- 输入必须校验

### 兼容性

- Chrome >= 90
- iOS >= 14
- Android >= 10

## 依赖管理

```bash
# 锁定版本
npm install --save-exact
# 或
yarn -W --exact
```
