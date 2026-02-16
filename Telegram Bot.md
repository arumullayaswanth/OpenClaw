

# 📦 README.md – Connect OpenClaw + Ollama to Telegram Bot

---

# 🤖 Local Autonomous AI Telegram Bot

Control your **local powerful AI agent** from Telegram using:

* 🧠 OpenClaw
* ⚡ Ollama
* 💬 Telegram Bot API
* 🐳 Docker (optional deployment)

---

# 🚀 Features

* Run powerful local LLM (70B supported)
* Execute full shell commands
* Create and deploy projects
* Full laptop control (if enabled)
* Remote access via Telegram
* Multi-step autonomous tasks

---

# 🧠 Requirements

| Component        | Required                 |
| ---------------- | ------------------------ |
| RAM              | 32GB+ (64GB recommended) |
| Ollama           | Installed                |
| OpenClaw         | Installed                |
| Python           | 3.10+                    |
| Telegram Account | Yes                      |

---

# 1️⃣ Create Telegram Bot

1. Open Telegram
2. Search for **@BotFather**
3. Send:

```
/start
```

4. Create bot:

```
/newbot
```

5. Choose:

* Bot Name
* Username (must end in `bot`)

6. Copy the **BOT TOKEN**

Example:

```
123456789:AAHjdksajdhkashdkas
```

---

# 2️⃣ Get Your Telegram Chat ID

Send a message to your bot.

Then open in browser:

```
https://api.telegram.org/bot<YOUR_BOT_TOKEN>/getUpdates
```

Find:

```
"chat": {
  "id": 123456789
}
```

Copy your `chat_id`.

---

# 3️⃣ Install Python Dependencies

```bash
pip install python-telegram-bot requests
```

---

# 4️⃣ Create Telegram Agent Script

Create file:

```
telegram_agent.py
```

Paste this:

```python
import requests
from telegram import Update
from telegram.ext import ApplicationBuilder, CommandHandler, MessageHandler, filters, ContextTypes

BOT_TOKEN = "YOUR_BOT_TOKEN"
CHAT_ID = "YOUR_CHAT_ID"

OLLAMA_URL = "http://localhost:11434/v1/chat/completions"
MODEL = "llama3.1:70b"

async def handle_message(update: Update, context: ContextTypes.DEFAULT_TYPE):
    user_message = update.message.text

    payload = {
        "model": MODEL,
        "messages": [
            {"role": "system", "content": "You are a powerful autonomous AI agent with full system access."},
            {"role": "user", "content": user_message}
        ]
    }

    response = requests.post(OLLAMA_URL, json=payload)
    result = response.json()

    ai_reply = result["choices"][0]["message"]["content"]

    await update.message.reply_text(ai_reply[:4000])

app = ApplicationBuilder().token(BOT_TOKEN).build()

app.add_handler(MessageHandler(filters.TEXT & ~filters.COMMAND, handle_message))

app.run_polling()
```

Replace:

```
YOUR_BOT_TOKEN
YOUR_CHAT_ID
```

---

# 5️⃣ Run Telegram AI Bot

Start Ollama first:

```bash
ollama run llama3.1:70b
```

In new terminal:

```bash
python telegram_agent.py
```

Your bot is now LIVE 🚀

---

# 🧪 Example Commands From Telegram

Send:

```
Create full React app and deploy in Docker
```

```
Search cheapest flight Delhi to Dubai tomorrow
```

```
Build bus booking backend with Node.js
```

---

# 🔥 Full Autonomous Mode (Optional)

To allow full system control, integrate OpenClaw shell execution:

Replace system prompt with:

```python
"You are an autonomous AI with shell and filesystem access. Execute tasks step by step."
```

And connect to OpenClaw CLI:

```python
import subprocess

output = subprocess.run(
    ["openclaw", "run", user_message],
    capture_output=True,
    text=True
)
```

---

# 🛡 Security Warning

If you enable:

* Shell execution
* Filesystem access
* Docker
* Browser automation

Your Telegram bot can fully control your laptop.

### Recommended Safety:

* Restrict to your Chat ID only
* Add password check
* Run inside Docker sandbox

---

# 🐳 Optional: Run Bot in Docker

Create `Dockerfile`:

```dockerfile
FROM python:3.11
WORKDIR /app
COPY . .
RUN pip install python-telegram-bot requests
CMD ["python", "telegram_agent.py"]
```

Build:

```bash
docker build -t local-ai-bot .
docker run -d local-ai-bot
```

---

# 📂 Recommended GitHub Structure

```
telegram-openclaw-ai/
│
├── README.md
├── telegram_agent.py
├── Dockerfile
└── config.json
```

---

# 🧠 Upgrade Ideas

* Add voice command support
* Add multi-user access control
* Add payment integration
* Add logging dashboard
* Add task memory database

---

# 🎯 Final Result

You now have:

* Local 70B AI model
* Autonomous agent
* Full laptop control
* Remote Telegram interface
* Deployable AI infrastructure

All running from your machine 🔥

---
