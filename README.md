# 🤖 My First Slack Bot
A Slack bot built with Node.js and Bolt that runs continuously on a remote Linux server, managed by systemd.
This is my very first ever coding project where I bult a Slack bot following the Hack Club guide for the Stardance challenge.

<img width="800" height="450" alt="SlackbotGIF" src="https://github.com/user-attachments/assets/623d5339-20b4-4034-acb2-e0dee4b815ac" />

---

## ▶️ Try it

Add the bot to your Slack workspace and type `/miobot-help` to get started.

---

## ⚡ Quick start

```bash
git clone https://github.com/FedericoTarallo/miobot_project
cd miobot_project
npm install
```

Create a `.env` file:
```
SLACK_BOT_TOKEN=xoxb-your-token-here
SLACK_APP_TOKEN=xapp-your-token-here
```

Run it:
```bash
node index.js
```

---

## ✨ Features

- `/miobot-latency` — measures and displays the bot's response time in milliseconds
- `/miobot-help` — lists all available commands
- `/miobot-joke` — fetches a random joke from an external API
- Restarts automatically if it ever crashes (managed by systemd)
- Stays online 24/7, even when my laptop is closed

---

## 🖥️ How to deploy it permanently (Linux + systemd)

**Requirements:** Node.js v18+, a Linux server, a Slack App with Socket Mode enabled.

**1. Upload the project and install dependencies**
```bash
cd /root/miobot_project
npm install
```

**2. Create the systemd service**
```bash
nano /etc/systemd/system/slackbot.service
```

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

**3. Enable and start**
```bash
systemctl daemon-reload
systemctl enable --now slackbot.service
```

**4. Verify**
```bash
systemctl status slackbot.service
```

`active (running)` in green = bot is live. 🟢

---

## ⚙️ How it works

The bot connects to Slack using **Socket Mode** instead of a public HTTP endpoint — meaning it doesn't need a domain or open ports, just an outbound connection. This made it perfect for running on Hack Club's Nest server without any extra networking setup.











