# Intern Day 2 · Backend

FastAPI 登录鉴权 + 待办清单接口。配套前端仓库：<替换为 frontend GitHub 地址>

## 接口约定
- GET /health 健康检查（无需登录）
- POST /auth/login 登录，返回 Bearer token
- GET /auth/me 当前用户（需登录）
- POST /auth/logout 退出，服务端删除会话
- GET / POST / PATCH / DELETE /todos 待办清单（需登录）

## 登录状态方案
随机不透明会话令牌（secrets.token_urlsafe），后端内存保存会话与过期时间，
退出即删除，过期或无效返回 401。服务重启后所有数据重置，
练习账号 admin / demo 在启动时自动创建（密码由环境变量注入）。

## 验收条件
1. 错误账号与错误密码返回统一提示
2. 未携带、伪造、过期或已退出的凭证访问受保护接口返回 401
3. 待办接口校验登录状态，用户之间数据隔离
