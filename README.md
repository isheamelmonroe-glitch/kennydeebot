# @kennydeebot — Telegram Dictionary Bot

A Telegram bot that looks up English word definitions, deployed via
GitHub + Railway.

## Files

- `bot.py` — the bot
- `requirements.txt` — Python dependencies
- `Procfile` — tells Railway how to start the bot (`worker: python bot.py`)
- `runtime.txt` — pins the Python version
- `.gitignore` — keeps secrets/junk out of git
- `.env.example` — shows what env var to set (don't commit a real `.env`)

## 1. Get your bot token

1. Message **@BotFather** on Telegram
2. Send `/newbot`, follow the prompts, set username to `kennydeebot`
3. Copy the token BotFather gives you — you'll need it in step 3 below

## 2. Push this project to GitHub

```bash
cd kennydeebot
git init
git add .
git commit -m "Initial commit: kennydeebot dictionary bot"
git branch -M main
git remote add origin https://github.com/<your-username>/kennydeebot.git
git push -u origin main
```

(Create the empty `kennydeebot` repo on GitHub first if you haven't.)

**Important:** never commit your real token. `.gitignore` already excludes
`.env`, and `bot.py` only reads the token from an environment variable — it's
never hardcoded in the file.

## 3. Deploy on Railway

1. Go to [railway.app](https://railway.app) and sign in with GitHub
2. Click **New Project → Deploy from GitHub repo**
3. Select your `kennydeebot` repo
4. Once the project is created, go to **Variables** and add:
   - `TELEGRAM_BOT_TOKEN` = the token from BotFather
5. Railway will detect the `Procfile` and run `python bot.py` as a worker
   process automatically. Check the **Deployments** tab for build/runtime logs.

That's it — the bot runs continuously on Railway using polling, so no public
URL or webhook setup is needed.

## 4. Test it

Open Telegram, search **@kennydeebot**, and send it a word like `hello`, or
use `/define serendipity`.

## Local development (optional)

```bash
python -m venv venv
source venv/bin/activate      # Windows: venv\Scripts\activate
pip install -r requirements.txt
export TELEGRAM_BOT_TOKEN="your-token-here"   # Windows: set TELEGRAM_BOT_TOKEN=your-token-here
python bot.py
```

## Commands

- `/start` — welcome message
- `/help` — usage instructions
- `/about` — about this bot
- `/define <word>` — explicit lookup
- Typing any plain word also triggers a lookup automatically

## Updating the bot later

Any time you push new commits to the `main` branch on GitHub, Railway
automatically redeploys the bot with the changes.

```bash
git add .
git commit -m "Update bot"
git push
```
