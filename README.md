# Next AI Draw.io - LazyCat App

[Next AI Draw.io](https://github.com/DayuanJiang/next-ai-draw-io)（AI + draw.io 图表生成）的懒猫微服（LazyCat）打包。

## 模式

- **镜像模式（mirror）**：`ghcr.io/dayuanjiang/next-ai-draw-io` 镜像经 `ghcr.1ms.run` 加速器拉取，`require_digest_match: true` 校验镜像内容与上游一致。
- **自动跟随上游**：每日检查上游 semver tag（`channel: stable`），发现新版本自动更新版本号与镜像、构建 LPK、发布商店。
- **喵喵商店发布**：仅私有商店（MiaoMiao private store），不发布官方商店。
- **单容器 + SQLite 无依赖**：draw.io 前端内嵌镜像（离线可用），无数据库；持久化 `/lzcapp/var/next-ai-draw-io:/app/data`（管理面板设置 + 服务端模型配置）。

## AI 模型配置

两种方式二选一：

1. **部署参数（服务端统一配置）**：安装时填 `AI Provider`（如 `openai`、`deepseek`、`glm`、`qwen`、`custom`=OpenAI 兼容端点）、`AI Model`、`API Key`、可选 `Base URL`，自动生成 `ai-models.json`，所有用户免配置直接用。
2. **用户自带 Key**：部署参数全部留空，每个用户在聊天面板设置里填自己的 provider 和 Key（仅存浏览器）。

管理面板 `/admin`：可选设置 `Admin Panel Password` 启用。

## 结构

| 文件 | 说明 |
| --- | --- |
| `package.yml` | 包元数据（`community.lazycat.app.next-ai-draw-io`） |
| `lzc-manifest.yml` | 服务、路由与模型配置注入 |
| `lzc-deploy-params.yml` | 安装参数（AI provider/model/key、管理面板密码） |
| `lzc-build.yml` | 构建配置 |
| `icon.png` | 图标（上游 favicon-512） |
| `.github/lazycat-action.yml` | [lazycat-github-action](https://github.com/ca-x/lazycat-github-action) 配置 |
| `.github/workflows/lazycat.yml` | 构建 + 发布工作流 |

## 所需 Secrets

| Secret | 说明 |
| --- | --- |
| `APPSTORE_URL` / `APPSTORE_TOKEN` | 喵喵商店 API 地址与发布令牌 |
| `APP_ID` | 可选 |
| `PRIVATE_STORE_GROUP_CODES` | 可选，私有分组码 |

## 说明

- 官方商店已有上游作者自发的同款应用（`cloud.lazycat.app.drawio-next-ai`），本包使用 `community.lazycat.app.next-ai-draw-io` 独立发布于喵喵商店。

## 许可

Apache-2.0（上游）
