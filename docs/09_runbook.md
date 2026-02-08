# 09_runbook.md - 运维手册/故障处理

> **备注**: docs/ ⭐ 推荐（给 OPS 用）
> 运维手册/故障处理，常用命令、故障排查（OPS 运维用）

> 给 OPS 用的故障处理指南

## 常用命令

### 服务管理

```bash
# 查看服务状态
systemctl status your-service

# 重启服务
sudo systemctl restart your-service

# 查看日志
sudo journalctl -u your-service -f

# 查看错误日志
sudo journalctl -u your-service --since "1 hour ago" | grep ERROR
```

### 数据库

```bash
# 连接数据库
psql -h localhost -U user -d dbname

# 查看连接数
SELECT count(*) FROM pg_stat_activity;
```

## 故障处理流程

```
发现问题
    ↓
评估影响
    ↓
确定级别
    ↓
处理故障
    ↓
恢复验证
    ↓
复盘总结
```

## 常见故障

### 🔴 P0 - 紧急故障

#### 服务不可用

**症状**: 502/503 错误，用户无法访问

**处理步骤**:
1. 检查服务状态
   ```bash
   systemctl status your-service
   ```
2. 查看错误日志
   ```bash
   journalctl -u your-service -n 100
   ```
3. 重启服务
   ```bash
   systemctl restart your-service
   ```
4. 验证恢复
   ```bash
   curl -f https://example.com/health
   ```

**升级**: 立即通知值班工程师

### 🟠 P1 - 严重故障

#### 性能下降

**症状**: 响应时间 > 1s

**处理步骤**:
1. 检查资源使用
   ```bash
   top -bn1 | head -20
   ```
2. 检查数据库连接
   ```bash
   psql -c "SELECT count(*) FROM pg_stat_activity;"
   ```
3. 重启服务或扩容

### 🟡 P2 - 一般故障

#### 功能异常

**症状**: 特定功能不可用

**处理步骤**:
1. 记录问题
2. 创建 Bug 跟踪
3. 安排修复

## 联系方式

| 角色 | 电话 | 备注 |
|------|------|------|
| 值班工程师 | xxx-xxxx-xxxx | 24/7 |
| 技术负责人 | xxx-xxxx-xxxx | 工作时间 |
| 运维经理 | xxx-xxxx-xxxx | 紧急升级 |
