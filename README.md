# PLAC-CRIC

Here’s a clean README.md you can directly copy and use 👇

⸻

# 🤖 Telegram Group Bot with Python (AI Ready)
This project demonstrates how to create a Telegram bot using Python, add it to a group, and automatically reply to messages.
🚀 Future Goal: Integrate AI (via OpenRouter API) so the bot can intelligently answer questions.
---
## 📌 Features
- Responds to messages in Telegram group
- Simple keyword-based replies (starter logic)
- Ready to integrate AI (OpenRouter / LLM APIs)
- Lightweight and beginner-friendly
---
## 🧱 Prerequisites
- Python 3.9+
- Telegram account
- Basic knowledge of Python
---
## ⚙️ Step 1: Create Telegram Bot
1. Open Telegram
2. Search for **@BotFather**
3. Run command:

/newbot

4. Follow instructions
5. Copy your **BOT TOKEN**
---
## ⚙️ Step 2: Install Dependencies
```bash
pip install python-telegram-bot

⸻

⚙️ Step 3: Python Bot Code

Create file: bot.py

import os
import requests
from telegram import Update
from telegram.ext import ApplicationBuilder, CommandHandler, MessageHandler, ContextTypes, filters
BOT_TOKEN = os.getenv("TELEGRAM_BOT_TOKEN")
# Optional: OpenRouter config (future use)
OPENROUTER_API_KEY = os.getenv("OPENROUTER_API_KEY")
# Basic command
async def start(update: Update, context: ContextTypes.DEFAULT_TYPE):
    await update.message.reply_text("Hi, I am your Telegram bot 🤖")
# Simple reply logic (non-AI)
async def reply_message(update: Update, context: ContextTypes.DEFAULT_TYPE):
    user_text = update.message.text
    if "hello" in user_text.lower():
        reply = "Hello! 👋"
    elif "help" in user_text.lower():
        reply = "Ask me anything. AI coming soon 😉"
    else:
        reply = f"You said: {user_text}"
    await update.message.reply_text(reply)
# --- AI Integration (OpenRouter) ---
def ask_ai(question):
    url = "https://openrouter.ai/api/v1/chat/completions"
    headers = {
        "Authorization": f"Bearer {OPENROUTER_API_KEY}",
        "Content-Type": "application/json"
    }
    data = {
        "model": "openai/gpt-4o-mini",
        "messages": [
            {"role": "user", "content": question}
        ]
    }
    response = requests.post(url, headers=headers, json=data)
    if response.status_code == 200:
        return response.json()["choices"][0]["message"]["content"]
    else:
        return "AI error. Try again later."
# AI-enabled reply (optional)
async def reply_ai(update: Update, context: ContextTypes.DEFAULT_TYPE):
    user_text = update.message.text
    ai_reply = ask_ai(user_text)
    await update.message.reply_text(ai_reply)
def main():
    app = ApplicationBuilder().token(BOT_TOKEN).build()
    app.add_handler(CommandHandler("start", start))
    # Choose ONE:
    # 1. Basic bot:
    app.add_handler(MessageHandler(filters.TEXT & ~filters.COMMAND, reply_message))
    # 2. AI bot (uncomment below and comment above):
    # app.add_handler(MessageHandler(filters.TEXT & ~filters.COMMAND, reply_ai))
    print("Bot is running...")
    app.run_polling()
if __name__ == "__main__":
    main()

⸻

▶️ Step 4: Run the Bot

export TELEGRAM_BOT_TOKEN="your_bot_token"
export OPENROUTER_API_KEY="your_openrouter_key"
python bot.py

⸻

👥 Step 5: Add Bot to Group

1. Add bot to your Telegram group
2. Disable privacy mode:

Go to @BotFather

/mybots → Your Bot → Bot Settings → Group Privacy → Turn OFF

⸻

🧠 Future Enhancement (AI)

You can upgrade this bot to:

* Answer technical questions
* Summarize conversations
* Help in group discussions
* Act like support bot

Using:

* OpenRouter (multi-model access)
* OpenAI / Anthropic / Mistral
* Local LLM (Ollama)

⸻

🛠️ Ideas for Improvement

* Add user tagging
* Store chat history (DB)
* Add commands like /ask
* Rate limiting
* Logging

⸻

⚠️ Notes

* Do NOT expose API keys publicly
* Use .env file in production
* Respect Telegram rate limits

⸻

📚 Learning Purpose

This project is meant for:

* Learning Telegram Bot APIs
* Understanding async Python
* Integrating AI with real apps



