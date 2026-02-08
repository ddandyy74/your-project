# 00_index.md — 文档索引（必读）

> ⭐⭐⭐ **docs/ 是本项目最重要的目录**  
> 本文件用于告诉 AI 与新成员：  
> **项目文档的阅读顺序、优先级，以及“什么时候该看哪个文件”。**

---

## 阅读顺序（必读）

### 🔥 第一优先级（进入项目前必须读）

1. [README.md](../README.md)  
   项目入口，3 分钟了解项目全貌

2. [PROJECT.md](../PROJECT.md)  
   项目总览，包含更完整的背景、目标与约束

3. [AGENTS.md](../AGENTS.md)  
   项目流程铁律，定义 PM / DEV / OPS / QA 的职责边界与工作方式

4. [SOUL.md](../SOUL.md)  
   主会话人格与项目推进方式（项目文化与决策心智模型）

---

### ⭐ 第二优先级（开始实际工作前必须读）

5. [02_requirements.md](02_requirements.md)  
   需求与范围：当前阶段做什么 / 不做什么

6. [04_tech_stack.md](04_tech_stack.md)  
   技术栈与约束：语言、平台、依赖、禁止项

7. [05_workflow_rules.md](05_workflow_rules.md)  
   项目级流程与协作规则（对 AGENTS.md 的项目补充）

---

### 📋 第三优先级（执行任务时参考）

8. [03_acceptance.md](03_acceptance.md)  
   验收标准：QA 判定 pass / fail 的直接依据

9. [06_architecture.md](06_architecture.md)  
   架构设计：模块划分、数据流、关键接口

10. [07_test_plan.md](07_test_plan.md)  
    测试策略与回归计划

---

### 🛠️ 第四优先级（部署与运维相关）

11. [08_deploy_plan.md](08_deploy_plan.md)  
    部署方案（OPS 执行依据）

12. [09_runbook.md](09_runbook.md)  
    运维与故障处理手册

---

## 快速导航（按常见问题）

| 你现在想做什么 | 先看这些文件 |
|----------------|--------------|
| 了解项目是干什么的 | README.md → PROJECT.md |
| 知道现在该做什么任务 | 02_requirements.md + work/01_wbs.md |
| 知道代码应该怎么写 | 04_tech_stack.md + 06_architecture.md |
| 判断是否算“做完了” | 03_acceptance.md |
| 准备部署或验证 | 08_deploy_plan.md |
| 出现问题如何处理 | 09_runbook.md |

---

## 使用说明（给 AI 和新成员）

- 本目录中的文档**按编号顺序阅读**
- 探索阶段允许内容频繁调整
- 一旦阶段稳定，应将结论沉淀为正式文档或 ADR

---

## 文档更新日志

| 日期 | 更新内容 | 更新人 |
|------|----------|--------|
| 2026-02-08 | 初始化文档索引 | doggo |
