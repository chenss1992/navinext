# 🎵 NaviNest

**NaviNest** 是一款面向自建 **Navidrome** 音乐服务器的轻量级 Web 管理系统，提供会员管理、播放统计、数据分析及 Telegram 通知等功能，帮助管理员更加方便地管理 Navidrome 用户与音乐服务。

---

## ✨ 主要功能

| 功能 | 说明 |
| --- | --- |
| 👤 **会员管理** | Navidrome 用户同步、会员状态及有效期管理 |
| 📊 **播放统计** | 播放次数、播放排行及数据统计 |
| 📅 **周期统计** | 日 / 周 / 月播放统计 |
| 🕐 **自然日统计** | 根据配置时区统计每日播放数据 |
| 🎵 **播放明细** | 查看用户及歌曲播放记录 |
| 🏆 **排行榜** | 用户、歌曲等播放数据排行 |
| 🤖 **Telegram Bot** | Telegram Bot 管理及消息通知 |
| 📢 **通知管理** | 新会员、续期、到期、播放等通知 |
| 📈 **定时报告** | 日报 / 周报 / 月报 |
| 🐳 **Docker 部署** | Docker Compose 快速部署 |

---

## 🛠️ 技术特点

- Python / FastAPI
- SQLite
- Docker
- Navidrome API
- Telegram Bot API
- 支持自定义时区
- Web 管理界面

---

## 🚀 Docker Compose

### 1. 准备配置文件

请先从 GitHub 下载项目中的：

```text
.env.example
```

根据自己的服务器环境修改配置，然后将文件重命名为：

```text
.env
```

> ⚠️ **必须先配置 `.env`，再启动容器。**

---

### 2. 创建 `docker-compose.yml`

```yaml
services:
  navinext:
    image: sosooan/navinext:latest
    container_name: navinext
    restart: unless-stopped

    ports:
      - "8089:8000"

    env_file:
      - .env

    volumes:
      - ./data:/app/data
```

---

### 3. 启动

在 `docker-compose.yml` 所在目录执行：

```bash
docker compose up -d
```

查看运行状态：

```bash
docker compose ps
```

查看日志：

```bash
docker logs -f navinext
```

---

## 📁 推荐目录结构

```text
navinext/
├── docker-compose.yml
├── .env
└── data/
```

其中：

- `.env`：服务器及 Navidrome / Telegram 等配置
- `data/`：NaviNest 数据库及运行数据
- `docker-compose.yml`：Docker 容器配置

---

## 🌐 Web 管理界面

容器启动后访问：

```text
http://你的服务器IP:8089
```

例如：

```text
http://192.168.1.100:8089
```

---

## 🔗 项目地址

GitHub：  
**NaviNest**

---

## 📦 Docker Image

```text
sosooan/navinext:latest
```

固定版本：

```text
sosooan/navinext:1.1.0
```

建议生产环境使用固定版本 Tag，以避免 `latest` 自动更新导致版本变化。

---

## 📌 当前版本

**v1.1.0**

NaviNest 持续完善 Navidrome 会员管理、播放统计及 Telegram 管理功能。

---

## ⚠️ 注意事项

1. 首次部署前请务必正确配置 `.env`。
2. `.env` 包含服务器及 Bot 等敏感配置，**不要提交到公开仓库**。
3. `data/` 目录用于保存运行数据，请做好备份。
4. NaviNest 需要能够正常访问你的 Navidrome 服务及相关 API。
