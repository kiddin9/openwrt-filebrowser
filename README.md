# openwrt-filebrowser

OpenWrt 软件包及 LuCI 管理界面，基于 [FileBrowser Quantum](https://github.com/gtsteffaniak/filebrowser)（`v2.1.6-beta`）构建，提供现代化多存储源 Web 文件管理、实时全文索引搜索、WebDAV 挂载、细粒度权限控制及多媒体/Office 在线预览能力。

## 包含组件

- **`filebrowser-q`**：FileBrowser Quantum 核心二进制与 `procd` 服务脚本（支持动态防火墙放行、环境变量安全注入密钥、SQLite 数据库保护及 YAML 配置生成）。
- **`luci-app-filebrowser-q`**：基于原生 LuCI客户端 JavaScript（`luci-base`）构建的多标签管理界面与完整简体中文（`zh_Hans`）本地化支持。

## 主要特性与配置项

1. **基本设置**：服务开关、监听地址（`0.0.0.0` / `127.0.0.1` / `::`）、监听端口、动态防火墙端口自动放行、反向代理子路径（`baseURL`）、默认界面语言（`zhCN` 等）、站点名称、禁用更新检查/PWA 安装提示/节日主题等。
2. **存储与目录**：主存储根目录与显示名称、只读模式、禁止公开分享、按用户自动隔离目录、逻辑文件大小统计（适配 FUSE/CloudDrive2/rclone）、`/` 根目录自动排除 `/proc` `/sys` `/dev` 虚拟内核文件系统索引、附加多存储源（支持 `/路径:显示名:ro`）、隐藏文件/软链接/空目录过滤、默认新建文件与目录权限。
3. **认证与安全**：支持账号密码认证、反向代理请求头认证（Authelia/Authentik 等）及免密内网模式；通过 `FILEBROWSER_ADMIN_PASSWORD` 环境变量同步初始/重置密码（避免明文落盘，清空后保留 Web 界面修改的密码）；支持用户自助注册、强制 TOTP 两步验证（2FA）、Passkey 通行密钥、会话有效期与防爆破限流开关。
4. **网络、TLS 与反代**：WebDAV 开关、信任反向代理转发头（`trustProxyHeaders`）、公网分享地址（`externalUrl`）、内网回调地址（`internalUrl`）、原生 HTTPS（TLS 证书/私钥）以及本地 Unix Domain Socket 监听模式。
5. **性能与外部集成**：自定义 SQLite 数据库存储路径（自动拦截 `database.db` 命名冲突并兼容旧版迁移）、缓存目录与预览缓存上限（`cacheDirMaxSizeMB`）、在线打包归档大小上限、并发缩略图线程数控制、索引库启动校验模式（`quickCheck` / `probe` / `off`）、FFmpeg 视频缩略图与内嵌字幕/HEIC 转换、OnlyOffice 在线文档预览与协同编辑、日志级别与 API 日志控制。
6. **自定义配置与日志**：支持开启“自定义 YAML 配置模式”直接在 LuCI 在线编辑 `/etc/filebrowser-q/config.yaml`（便于配置 OIDC、LDAP 或复杂访问规则），并内置运行日志实时查看器。

## 编译说明

在 OpenWrt 源码根目录执行：

```bash
git clone https://github.com/kiddin9/openwrt-filebrowser package/openwrt-filebrowser
make menuconfig
# LuCI -> 3. Applications -> <*> luci-app-filebrowser-q
make package/openwrt-filebrowser/luci-app-filebrowser-q/compile V=s
```
