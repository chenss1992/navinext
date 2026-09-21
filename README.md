# NaviNest

**NaviNest** 是一款面向自建 **Navidrome** 音乐服务器的轻量级 Web 管理系统，提供会员管理、播放统计、数据分析及 Telegram 通知等功能，帮助管理员更加方便地管理 Navidrome 用户与音乐服务。

---

## ✨ 主要功能

| **功能** | **说明** |
| --- | --- |
| 👤 **会员管理** | Navidrome 用户同步、会员状态及有效期管理 |
| 📊 **播放统计** | 播放次数、播放排行及数据统计 |
| 📅 **周期统计** | 日 / 周 / 月播放统计 |
| 🕐 **自然日统计** | 根据配置时区统计每日播放数据 |
| 🎵 **播放明细** | 查看用户及歌曲播放记录 |
| 🏆 **排行榜** | 用户、歌曲等播放数据排行 |
| 🤖 **Telegram 机器人** | Telegram Bot 管理及消息通知 |
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

支持 **Docker Compose、Dockge、Portainer、群晖 Container Manager** 等 Docker 管理工具。

将以下配置复制到 Docker 管理工具中，并根据实际环境修改 `environment` 中的配置。

```yaml
services:
  navinext:
    image: sosooan/navinext:latest
    container_name: navinext
    restart: unless-stopped

    ports:
      - "8089:8000"

    environment:
      # NaviNest
      APP_NAME: NaviNest
      APP_SECRET: "请修改为随机长字符串"
      ADMIN_USERNAME: admin
      ADMIN_PASSWORD: "请修改管理员密码"
      TIMEZONE: Asia/Shanghai

      # Navidrome
      NAVIDROME_URL: "http://192.168.1.100:4533"
      NAVIDROME_USERNAME: admin
      NAVIDROME_PASSWORD: "你的Navidrome管理员密码"

      # Telegram
      TELEGRAM_BOT_TOKEN: ""
      TELEGRAM_ADMIN_IDS: "12345678"
      TELEGRAM_DAILY_REPORT_ENABLED: "true"
      TELEGRAM_WEEKLY_REPORT_ENABLED: "true"
      TELEGRAM_MONTHLY_REPORT_ENABLED: "true"
      TELEGRAM_EXPIRE_REMINDER_ENABLED: "true"
      REPORT_HOUR: "9"
      EXPIRE_REMINDER_DAYS: "7,3,1,0"
      TASK_INTERVAL_MINUTES: "10"

    volumes:
      - ./data:/app/data
```

### ⚙️ 环境变量

| 变量 | 说明 |
| --- | --- |
| `APP_NAME` | 应用名称 |
| `APP_SECRET` | 应用安全密钥，请修改为随机长字符串 |
| `ADMIN_USERNAME` | NaviNest 管理员用户名 |
| `ADMIN_PASSWORD` | NaviNest 管理员密码 |
| `TIMEZONE` | 系统时区 |
| `NAVIDROME_URL` | Navidrome 服务地址 |
| `NAVIDROME_USERNAME` | Navidrome 管理员用户名 |
| `NAVIDROME_PASSWORD` | Navidrome 管理员密码 |
| `TELEGRAM_BOT_TOKEN` | Telegram Bot Token，不使用可留空 |
| `TELEGRAM_ADMIN_IDS` | Telegram 管理员 Chat ID |
| `TELEGRAM_*_ENABLED` | Telegram 报告及提醒开关 |
| `REPORT_HOUR` | 报告发送时间 |
| `EXPIRE_REMINDER_DAYS` | 会员到期提醒时间 |
| `TASK_INTERVAL_MINUTES` | 后台任务检查间隔，单位：分钟 |

> ⚠️ **部署前请务必修改 `APP_SECRET`、`ADMIN_PASSWORD`、Navidrome 登录信息以及 Telegram 相关配置。**

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

## 📦 Docker Image

```text
sosooan/navinext:latest
```

固定版本：

```text
sosooan/navinext:1.1.0
```

生产环境建议使用固定版本 Tag，以避免 `latest` 自动更新导致版本变化。

---

## 📌 当前版本

**v1.1.0**

NaviNest 持续完善 Navidrome 会员管理、播放统计及 Telegram 管理功能。

---

## ⚠️ 注意事项

1. `APP_SECRET` 请使用随机长字符串。
2. 请修改默认的 NaviNest 管理员密码。
3. `NAVIDROME_URL` 必须是 NaviNest 容器可以访问的地址。
4. `data/` 目录用于保存数据库及运行数据，请做好备份。
5. Telegram Bot Token 和密码属于敏感信息，请勿公开分享。
