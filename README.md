# openwrt-filebrowser

OpenWrt 软件包及 LuCI 管理界面，基于 [FileBrowser Quantum](https://github.com/gtsteffaniak/filebrowser)（`v2.1.6-beta`）构建，提供现代化多存储源 Web 文件管理、实时全文索引搜索、WebDAV 挂载与多媒体在线预览能力。

## 包含组件

- **`filebrowser-q`**：FileBrowser Quantum 核心二进制与 `procd` 服务脚本。
- **`luci-app-filebrowser-q`**：精简实用的原生 LuCI JS 管理界面（含简体中文 `zh_Hans` 本地化）。

## LuCI 核心配置项

- **基本设置**：服务开关、监听地址与端口、动态防火墙端口自动放行、认证模式（密码认证 / 内网免密）及管理员账号密码同步、主存储目录与附加多存储目录（当路径为 `/` 时自动设置 `name: "root"` 并排除 `/proc` `/sys` `/dev` 虚拟文件系统索引）、SQLite 数据库路径、缓存目录与预览缓存上限、禁用缩略图开关、反向代理 `baseURL` / 转发头信任及原生 HTTPS（TLS 证书/私钥）。
- **自定义配置**：支持启用自定义 YAML 模式直接在 LuCI 在线编辑 `/etc/filebrowser-q/config.yaml`（便于按需配置 OIDC、OnlyOffice 或复杂过滤规则）。
- **运行日志**：内置 `logread` 服务日志实时查看与刷新。
