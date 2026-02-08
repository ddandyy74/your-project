# src/ - 源码目录

> **备注**: src/ 💻 （如果有代码）源码目录（DEV 写）
> 项目源代码存放位置

## 目录结构

```
src/
├── index.js          # 入口文件
├── components/       # 组件
├── utils/            # 工具函数
├── services/         # 服务层
├── models/           # 数据模型
└── assets/           # 静态资源
```

## 规范

- 遵循 [04_tech_stack.md](../docs/04_tech_stack.md) 中的技术规范
- 代码风格遵循 [TOOLS.md](../TOOLS.md) 的 lint 规则
- 单元测试覆盖 >= 80%

## 注意事项

- 不在此目录创建 README，由代码注释和 docs/ 替代
- 复杂模块可在 src/ 下创建独立 README.md
