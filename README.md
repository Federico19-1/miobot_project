# 🤖 My First Slack Bot

> *"This bot isn't slacking off — it replies to messages 24/7!"*

A Slack bot built with Node.js and Bolt that runs continuously on a remote Linux server, managed by systemd. My first ever coding project, built for the [Hack Club Stardance Challenge](https://stardance.hackclub.com).

---

## 💡 What it does

This bot lives inside a Slack workspace and responds to messages automatically — 24 hours a day, 7 days a week — without ever needing a laptop to be open.

**Commands / features:**
- _(Federico: aggiungi qui cosa fa il bot — es. risponde a certi messaggi, comandi slash, ecc.)_

---

## 🛠️ Tech Stack

| Technology | Role |
|---|---|
| [Node.js](https://nodejs.org) | Runtime |
| [@slack/bolt](https://slack.dev/bolt-js) | Slack framework |
| [systemd](https://systemd.io) | Keeps the bot alive 24/7 |
| [Hack Club Nest](https://nest.hackclub.com) | Remote Linux server |
| Socket Mode | Real-time Slack connection |

---

## 🚀 How to run it locally

### Prerequisites
- Node.js v18+
- A Slack App with Socket Mode enabled
- A Bot Token (`xoxb-...`) and an App Token (`xapp-...`)

### Setup

**1. Clone the repo**
```bash
git clone https://github.com/FedericoTarallo/my-slack-bot
cd my-slack-bot
```

**2. Install dependencies**
```bash
npm install
```

**3. Create the `.env` file**
```bash
SLACK_BOT_TOKEN=xoxb-your-token-here
SLACK_APP_TOKEN=xapp-your-token-here
```

**4. Run the bot**
```bash
node index.js
```

---

## 🌐 Deploy on a Linux server (24/7 with systemd)

The real challenge of this project was keeping the bot alive permanently on a remote server — not just running it manually from a terminal.

### Step 1 — Upload the project and install dependencies
```bash
cd /root/miobot_project
npm install
```

### Step 2 — Create the systemd service file
```bash
nano /etc/systemd/system/slackbot.service
```

Paste this configuration:
```ini
[Unit]
Description=Slack Bot
After=network-online.target
Wants=network-online.target

[Service]
Type=simple
User=root
Restart=always
RestartSec=5
WorkingDirectory=/root/miobot_project
ExecStart=/usr/bin/node index.js

[Install]
WantedBy=multi-user.target
```

### Step 3 — Enable and start the service
```bash
systemctl daemon-reload
systemctl enable --now slackbot.service
```

### Step 4 — Verify it's running
```bash
systemctl status slackbot.service
```

If you see **`active (running)`** — the bot is live! 🟢

---

## 🐛 Troubleshooting

**Bot crashes on startup?**
```bash
journalctl -u slackbot.service -n 30 --no-pager
```

Common causes:
- `invalid_auth` → check that your tokens in `.env` are valid and not expired
- `Cannot find module` → run `npm install` inside the project folder
- `You must provide an appToken` → make sure `SLACK_APP_TOKEN` is set correctly in `.env`

---

## 📁 Project structure

```
miobot_project/
├── index.js          # Main bot logic
├── package.json      # Dependencies
├── .env              # Secret tokens (NOT on GitHub)
└── .gitignore        # Keeps .env out of the repo
```

---

## 🔒 Security note

The `.env` file containing secret tokens is listed in `.gitignore` and is **never uploaded to GitHub**. Never share your `xoxb-` or `xapp-` tokens publicly.

---

## 👤 Author

**Federico Tarallo** — built this as my very first coding project for [Hack Club Stardance](https://stardance.hackclub.com) 🚀

Special thanks to my brother Victor for helping me debug systemd and get this running!
