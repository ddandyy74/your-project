# 08_deploy_plan.md - 部署方案

> 给 OPS 用的部署指南

## 部署环境

| 环境 | URL | 状态 |
|------|-----|------|
| Dev | dev.example.com | ✅ 活跃 |
| Staging | staging.example.com | ✅ 活跃 |
| Production | example.com | ✅ 活跃 |

## 基础设施

| 组件 | 规格 | 数量 |
|------|------|------|
| Web Server | 2C4G | 2 |
| DB Server | 4C8G | 1 |
| Cache | 2C4G | 1 |

## 部署步骤

### 1. 准备工作

```bash
# 确认版本
export VERSION="1.0.0"

# 拉取代码
git checkout ${VERSION}
git pull origin main
```

### 2. 构建

```bash
# 安装依赖
npm ci

# 构建
npm run build
```

### 3. 测试

```bash
# 冒烟测试
npm run test:smoke
```

### 4. 部署

```bash
# 使用部署脚本
./deploy/deploy.sh ${VERSION}
```

### 5. 验证

```bash
# 健康检查
curl -f https://example.com/health

# 冒烟验证
npm run test:smoke:production
```

## 回滚方案

### 自动回滚

如果健康检查失败，自动回滚到上一版本。

### 手动回滚

```bash
# 回滚到上一版本
./deploy/rollback.sh

# 回滚到指定版本
./deploy/rollback.sh ${VERSION}
```

## 监控指标

| 指标 | 阈值 | 告警方式 |
|------|------|----------|
| CPU 使用率 | > 80% | 邮件 |
| 内存使用率 | > 85% | 邮件 |
| 错误率 | > 1% | 电话 |
| 响应时间 | > 500ms | 邮件 |

## 部署窗口

- 时间: 周二、周四 14:00-18:00
- 通知: 提前 1 天邮件通知
