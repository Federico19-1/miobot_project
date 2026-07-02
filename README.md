# 🤖 My First Slack Bot
A Slack bot built with Node.js and Bolt that runs continuously on a remote Linux server, managed by systemd.
This is my very first ever coding project where I built a Slack bot following the Hack Club guide for the Stardance challenge.

<img width="800" height="450" alt="SlackbotGIF" src="https://github.com/user-attachments/assets/623d5339-20b4-4034-acb2-e0dee4b815ac" />

---

## ▶️ Try it

Add the bot to your Slack workspace and type `/miobot-help` to get started.

If you want to build your own just follow this guide:
<img width="772" height="220" alt="image" src="https://github.com/user-attachments/assets/1c80ddc5-100e-40d9-a1cc-6511a9838798" />

---

## ✨ Here the Features

- `/miobot-latency` — measures and displays the bot's latency
- `/miobot-help` — lists all available commands
- `/miobot-joke` — fetches a random joke from an external API
- Restarts automatically if it ever crashes (managed by systemd)
- Stays online 24/7, even when my laptop is closed

---

## ⚙️ How it works

The bot connects to Slack using **Socket Mode** instead of a public HTTP endpoint — meaning it doesn't need a domain or open ports, just an outbound connection. This made it perfect for running on Hack Club's Nest server without any extra networking setup.











