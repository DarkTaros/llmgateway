# COOKIE_DOMAIN 与 ADMIN_EMAILS 配置

## 1. 修改 `.env`

```env
# Cookie 共享域名，不要填写协议或路径
COOKIE_DOMAIN=ahchat.ai

# 管理员邮箱；多个邮箱使用英文逗号分隔
ADMIN_EMAILS=admin@ahchat.ai
```

多个管理员示例：

```env
ADMIN_EMAILS=admin@ahchat.ai,ops@ahchat.ai
```

管理员邮箱必须与实际登录账号的邮箱完全一致。

## 2. 检查 Docker Compose

确保 API 服务的 `environment` 中包含：

```yaml
services:
  api:
    environment:
      - COOKIE_DOMAIN=${COOKIE_DOMAIN:-localhost}
      - ADMIN_EMAILS=${ADMIN_EMAILS:-}
```

如果服务名称不是 `api`，请把配置添加到实际运行后端 API 的服务中。

## 3. 重建容器

在 `docker-compose.yml` 所在目录执行：

```bash
docker compose up -d --force-recreate api
```

如果相关内容参与镜像构建，则执行：

```bash
docker compose up -d --build --force-recreate api
```

也可以重建全部服务：

```bash
docker compose up -d --build --force-recreate
```

## 4. 重新登录

清除浏览器中 `ahchat.ai`、`www.ahchat.ai` 和 `api.ahchat.ai` 的旧 Cookie，然后重新登录。使用 `ADMIN_EMAILS` 中的账号访问：

```text
https://admin.ahchat.ai/
```
