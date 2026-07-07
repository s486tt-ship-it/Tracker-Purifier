<div align="center">
  <img src="https://raw.githubusercontent.com/s486tt-ship-it/Tracker-Purifier/main/assets/screenshot-1.png" alt="首页仪表盘" width="80%">
  <br><br>
  <img src="https://raw.githubusercontent.com/s486tt-ship-it/Tracker-Purifier/main/assets/screenshot-2.png" alt="列表下载中心" width="80%">
</div>

# BT Tracker List Service

一个提供 BitTorrent Tracker 列表自动更新与获取服务的网页工具，帮助用户便捷地获取最新的活跃 Tracker，提升 BT/磁力链接的下载速度与连接成功率。

**在线地址：** [https://tracker.uszijian.dpdns.org](https://tracker.uszijian.dpdns.org)

---

## 项目简介

BitTorrent 下载时，优质的 Tracker 服务器能帮助客户端更快地找到 peer（同伴）节点。本项目自动收集、净化并整理活跃的 Tracker 地址，提供直观的网页界面，方便一键复制或直接订阅。

### 核心功能

- **自动更新** — 定期检测并更新 Tracker 列表，自动过滤失效节点
- **DNS 净化** — 通过 DoH 解析过滤无效/恶意域名，内置安全黑名单拦截
- **多格式支持** — 提供适用于 qBittorrent、Transmission、Aria2 等客户端的格式（换行分隔、逗号分隔等）
- **在线率追踪** — 记录 HTTP/HTTPS Tracker 的历史存活状态，低于阈值的节点自动排除
- **Geo-Routing** — 支持按请求来源国家排序，同国优先
- **轻量高效** — 基于 Cloudflare Workers 运行，响应迅速，无需部署服务器

---

## 使用方法

### 1. 手动复制

访问 [Tracker 列表下载中心](https://tracker.uszijian.dpdns.org/lists)，根据使用的客户端选择对应格式，点击复制后粘贴至客户端的 Tracker 设置中。

### 2. 客户端配置

**qBittorrent**
`设置 → BitTorrent → 勾选"自动添加以下 Tracker 到新的下载"`，粘贴订阅 URL 或列表内容。

**Transmission**
`偏好设置 → 对等网络 → Tracker 栏`，填入订阅 URL，Transmission 会自动获取。

**Aria2**
在 `aria2.conf` 中修改 `bt-tracker=` 项，填入以逗号分隔的 Tracker 列表。

### 3. API 自定义

通过 `/txt` 接口可自由组合查询参数，支持：
- `?mode=all` — 获取全部节点（含 IPv4 + IPv6 + 双栈）
- `?protocol=http,https` — 按协议过滤
- `?format=aria2` — 输出 Aria2 逗号分隔格式
- `?exclude=ws,wss` — 排除特定协议
- `?geo=1` — 按请求来源国家排序

示例：`/txt?format=aria2&exclude=ws,wss`

---

## 致谢

本项目的实现与数据源离不开开源社区的贡献，特别感谢：

- [**ngosang/trackerslist**](https://github.com/ngosang/trackerslist) — 高质量、持续维护的公共 Tracker 列表数据源
- [**trackerslist.com (XIU2)**](https://trackerslist.com) — 优秀的 Tracker 汇总方案与中文使用指引参考

---

## 开源协议

本项目基于 **MIT License** 开源。
