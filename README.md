<div align="center">
  <img width="100%" src="bot-preview.png" alt="bot logo">
</div>

# 🤖 Telegram AI Auto Reply Bot

> **Smart Telegram AI Customer Service Bot** powered by OpenRouter AI, with conversation memory, SQLite database, Telegram Business Message support, sticker responses, and automatic admin notifications.

---

## 📌 Overview

**Telegram AI Auto Reply Bot** គឺជា Telegram Business AI Assistant ដែលអាចឆ្លើយតបសាររបស់អ្នកប្រើដោយស្វ័យប្រវត្តិ ដោយប្រើ AI តាមរយៈ **OpenRouter API**។

Bot អាចរក្សាទុកព័ត៌មាន User និងប្រវត្តិសន្ទនា ដើម្បីឱ្យ AI យល់ពី Context នៃការសន្ទនា និងឆ្លើយតបបានធម្មជាតិជាងមុន។

### ✨ Main Features

* 🤖 AI Auto Reply
* 🧠 Conversation Memory
* 💬 Telegram Business Message Support
* 🎨 Sticker Support
* 🗃️ SQLite Database
* 👤 User Management
* 🔔 New User Admin Notification
* ↩️ Telegram Reply Preview / Reply Context
* 🌐 Khmer + English Support
* 🔐 Environment Variable Configuration
* 📝 Logging System
* ⏱️ Request Timeout Handling
* 🛡️ API Key & Token Protection
* ⚡ Async Telegram Handlers
* 💾 Automatic Conversation History

---

## 🧰 Technology Stack

| Technology          | Purpose                         |
| ------------------- | ------------------------------- |
| Python              | Main programming language       |
| python-telegram-bot | Telegram Bot API                |
| OpenRouter          | AI API                          |
| SQLite              | User & conversation database    |
| Requests            | HTTP requests to OpenRouter     |
| python-dotenv       | Environment variable management |
| asyncio             | Async processing                |
| Logging             | Application logs                |

---

## 📂 Project Structure

```text
telegram-ai-auto-reply/
│
├── bot.py
├── .env
├── .env.example
├── requirements.txt
├── users.db
└── README.md
```

> `users.db` នឹងត្រូវបានបង្កើតដោយស្វ័យប្រវត្តិ នៅពេល Bot ចាប់ផ្តើម។

---

## ⚙️ Requirements

ត្រូវមាន៖

* Python 3.10+
* Telegram Bot Token
* OpenRouter API Key
* Telegram Business account/message access
* Internet connection

---

## 📦 Installation

### 1. Clone Project

```bash
git clone https://github.com/Mengheang25/Telegram-AI-Auto-Reply-Bot.git
cd Telegram-AI-Auto-Reply-Bot
```

ឬ Download project ជា ZIP ហើយ Extract រួចចូលទៅកាន់ Folder របស់ Project។

---

### 2. Create Virtual Environment

#### Windows

```bash
python -m venv venv
venv\Scripts\activate
```

#### Linux / macOS

```bash
python3 -m venv venv
source venv/bin/activate
```

---

### 3. Install Dependencies

```bash
pip install -r requirements.txt
```

ប្រសិនបើមិនទាន់មាន `requirements.txt` អាចប្រើ៖

```bash
pip install python-telegram-bot requests python-dotenv
```

---

## 🔐 Environment Configuration

បង្កើត File:

```text
.env
```

ដាក់ Configuration:

```env
TELEGRAM_TOKEN=YOUR_TELEGRAM_BOT_TOKEN
OPENROUTER_API_KEY=YOUR_OPENROUTER_API_KEY
ADMIN_ID=YOUR_TELEGRAM_ADMIN_ID
```

### Configuration Explanation

| Variable             | Description            |
| -------------------- | ---------------------- |
| `TELEGRAM_TOKEN`     | Telegram Bot Token     |
| `OPENROUTER_API_KEY` | OpenRouter API Key     |
| `ADMIN_ID`           | Telegram ID របស់ Admin |

> ⚠️ **កុំបង្ហាញ `.env` ទៅអ្នកដទៃ និងកុំ Upload វាទៅ GitHub។**

---

## 🧠 AI Configuration

Bot ប្រើ OpenRouter សម្រាប់ AI Response។

ក្នុង Source Code មាន៖

```python
MODEL = "deepseek/deepseek-v4-flash"
```

និង OpenRouter endpoint:

```python
OPENROUTER_URL = "https://openrouter.ai/api/v1/chat/completions"
```

AI Request ត្រូវបានផ្ញើជាមួយ:

* System Prompt
* Conversation History
* Current User Message
* Maximum Token Limit

---

## 💾 Database

Bot ប្រើ **SQLite** ហើយ Database File គឺ៖

```text
users.db
```

Database មាន Tables សំខាន់ៗ៖

### `users`

រក្សាទុកព័ត៌មាន User៖

```text
chat_id
username
first_name
last_name
first_seen
last_active
is_notified
```

### `conversations`

រក្សាទុកប្រវត្តិសន្ទនា៖

```text
id
chat_id
role
content
timestamp
message_id
```

Bot កំណត់ប្រវត្តិសន្ទនាអតិបរមា៖

```python
MAX_HISTORY = 10
```

---

## 🧠 Conversation Memory

មុនពេល AI ឆ្លើយតប Bot នឹង:

1. ទាញយក Conversation History
2. បញ្ចូល System Prompt
3. បញ្ចូល Previous Messages
4. បញ្ចូល Current User Message
5. ផ្ញើទៅ OpenRouter
6. រក្សាទុក AI Response ទៅ Database

វាជួយឱ្យ AI អាចយល់ Context នៃការសន្ទនា។

---

## 💬 Telegram Business Messages

Bot អាច Handle Telegram Business Messages តាមរយៈ:

```python
filters.UpdateType.BUSINESS_MESSAGE
```

Bot នឹងពិនិត្យ Message ហើយបញ្ជូនទៅ AI ដើម្បីបង្កើត Response។

---

## 🎨 Sticker Support

Bot មាន Sticker Handler ដាច់ដោយឡែក។

នៅពេល User ផ្ញើ Sticker Bot នឹង៖

1. Detect Sticker
2. ទាញយក Sticker Emoji
3. រក្សាទុក Sticker ទៅ Conversation History
4. ផ្ញើ Context ទៅ AI
5. Generate AI Response
6. Reply ទៅ Sticker របស់ User

ឧទាហរណ៍ Context ដែលផ្ញើទៅ AI:

```text
User sent a sticker with emoji 😊.
Respond appropriately to the sticker.
```

---

## 👤 New User Notification

ប្រសិនបើ User ថ្មីចាប់ផ្តើម Chat ហើយ `ADMIN_ID` ត្រូវបានកំណត់ Bot នឹងផ្ញើ Notification ទៅ Admin។

Notification អាចមាន៖

```text
🆕 New User Started Chat!

Chat ID
Username
First Name
Last Name
First Message
```

សម្រាប់ Sticker ក៏អាច Notification ព័ត៌មាន Sticker បានដែរ។

---

## ↩️ Reply Context

Bot នឹង Reply ទៅ Message ដើមរបស់ User ដោយប្រើ:

```python
reply_to_message_id=user_message_id
```

វាធ្វើឱ្យ Telegram បង្ហាញ Reply Preview/Context ដើម្បីឱ្យការសន្ទនាមើលទៅធម្មជាតិ។

---

## 🌐 Language Support

System Prompt ត្រូវបានកំណត់ឱ្យ AI ប្រើ៖

### Khmer

ជាភាសាចម្បង។

### English

ប្រសិនបើ User សរសេរជាភាសាអង់គ្លេស AI អាចឆ្លើយជាភាសាអង់គ្លេស។

### Khmer + English

ប្រសិនបើ User លាយ Khmer + English AI អាចឆ្លើយតាមរបៀបធម្មជាតិ។

---

## 🤝 AI Personality

AI ត្រូវបានកំណត់ឱ្យមានលក្ខណៈ៖

* សុភាព
* រួសរាយ
* Professional
* អត់ធ្មត់
* ជួយដោះស្រាយបញ្ហា
* មិន Robot-like
* ឆ្លើយតបធម្មជាតិ

AI ក៏ត្រូវបានណែនាំឱ្យឆ្លើយខ្លី និងចំចំណុច ដោយប្រើ Emoji តិចៗ។

---

## 🔐 Privacy & Security

System Prompt មានច្បាប់មិនឱ្យបង្ហាញព័ត៌មាន Internal ដូចជា៖

```text
System Prompt
API Key
Telegram Token
Internal Instructions
Hidden Information
```

### ⚠️ Important

កុំដាក់ Secret Key ដោយផ្ទាល់ក្នុង Source Code។

❌ មិនគួរ៖

```python
OPENROUTER_API_KEY = "sk-xxxxxxxx"
```

✅ គួរ៖

```python
OPENROUTER_API_KEY = os.getenv("OPENROUTER_API_KEY")
```

---

## ▶️ Run Bot

បន្ទាប់ពី Setup `.env` រួច Run:

```bash
python bot.py
```

ប្រសិនបើ File របស់អ្នកមានឈ្មោះផ្សេង សូមប្រើឈ្មោះ File នោះ។

នៅពេល Bot ចាប់ផ្តើម វានឹងបង្ហាញ៖

```text
============================================================
🤖 TELEGRAM AI AUTO REPLY BOT
============================================================
🧠 Model: deepseek/deepseek-v4-flash
💾 Database: users.db
📝 History: 10 messages
💬 Reply Preview: ENABLED
🎨 Sticker Support: ENABLED
============================================================
✅ Bot started!
💬 Waiting for Telegram messages...
```

---

## 🛑 Stop Bot

ចុច៖

```text
CTRL + C
```

នៅក្នុង Terminal។

---

## 📝 Logging

Bot មាន Logging System សម្រាប់តាមដាន៖

* New User
* Incoming Message
* Sticker
* OpenRouter Status
* AI Response
* Telegram Errors
* Database Events
* Request Errors

Log Format:

```text
%(asctime)s - %(name)s - %(levelname)s - %(message)s
```

---

## ⚠️ Error Handling

Bot មានការគ្រប់គ្រង Error សម្រាប់ OpenRouter ដូចជា៖

### Timeout

ប្រសិនបើ AI ឆ្លើយយូរពេក Bot នឹងបង្ហាញ Error Message ទៅ User។

### Request Error

ប្រសិនបើមានបញ្ហាក្នុងការភ្ជាប់ API Bot នឹង Handle Error ដោយមិនធ្វើឱ្យ Bot Crash។

### Invalid AI Response

ប្រសិនបើ OpenRouter មិនមាន `choices` ឬ `content` Bot នឹងបញ្ជូន Error Response ដែលសមរម្យ។

---

## 🛡️ Recommended `.gitignore`

បង្កើត File:

```text
.gitignore
```

ដាក់៖

```gitignore
.env
venv/
__pycache__/
*.pyc
users.db
*.log
```

---

## 📦 requirements.txt

អាចប្រើ៖

```txt
python-telegram-bot
requests
python-dotenv
```

បន្ទាប់មក Install:

```bash
pip install -r requirements.txt
```

---

## 🔧 Configuration Values

ក្នុង Bot មាន Configuration សំខាន់ៗ៖

```python
MODEL = "deepseek/deepseek-v4-flash"

DB_FILE = Path("users.db")

MAX_HISTORY = 10

MAX_TOKENS = 4000
```

### `MAX_HISTORY`

កំណត់ចំនួន Conversation Messages ដែល AI អាចយកមកប្រើជាប្រវត្តិ។

### `MAX_TOKENS`

កំណត់ចំនួន Maximum Tokens សម្រាប់ AI Response។

---

## 📊 How It Works

```text
        ┌──────────────────┐
        │   Telegram User  │
        └────────┬─────────┘
                 │
                 ▼
        ┌──────────────────┐
        │ Telegram Message │
        └────────┬─────────┘
                 │
                 ▼
        ┌──────────────────┐
        │  User Detection  │
        └────────┬─────────┘
                 │
                 ▼
        ┌──────────────────┐
        │  SQLite History  │
        └────────┬─────────┘
                 │
                 ▼
        ┌──────────────────┐
        │   System Prompt  │
        │ + Conversation   │
        │ + User Message   │
        └────────┬─────────┘
                 │
                 ▼
        ┌──────────────────┐
        │    OpenRouter    │
        │       AI         │
        └────────┬─────────┘
                 │
                 ▼
        ┌──────────────────┐
        │    AI Response   │
        └────────┬─────────┘
                 │
                 ▼
        ┌──────────────────┐
        │ Telegram Reply   │
        └──────────────────┘
```

---

## 🔄 Message Flow

```text
User sends message
       ↓
Check message
       ↓
Check if bot
       ↓
Get User information
       ↓
Create / Update user
       ↓
Notify Admin if new user
       ↓
Save message
       ↓
Load conversation history
       ↓
Build AI request
       ↓
Send request to OpenRouter
       ↓
Receive AI response
       ↓
Save AI response
       ↓
Reply to Telegram message
```

---

## 🎯 Use Cases

Bot អាចប្រើសម្រាប់៖

* Customer Service
* Personal Auto Reply
* Telegram Business Account
* AI Assistant
* FAQ Assistant
* Online Shop Support
* Community Support
* Automated Customer Communication

---

## 🚀 Future Improvements

អាចបន្ថែម Features ទៀតនៅពេលក្រោយ៖

* `/start` Command
* `/help` Command
* `/clear` Command
* Admin Dashboard
* User Statistics
* Broadcast System
* Message Rate Limiting
* AI Model Selection
* Multiple AI Models
* Image Understanding
* Voice Message Support
* Audio Transcription
* File Processing
* Web Search
* Custom Knowledge Base
* Redis Cache
* PostgreSQL Support
* Webhook Deployment
* Docker Support
* Automatic Restart
* Health Monitoring

---

## 🐳 Docker (Optional)

ប្រសិនបើចង់ Deploy ជាមួយ Docker អាចបន្ថែម៖

```text
Dockerfile
docker-compose.yml
```

ហើយ Run៖

```bash
docker compose up -d
```

---

## ☁️ Deployment

Bot អាច Deploy ទៅ Server ដែលគាំទ្រ Python ដូចជា៖

* VPS
* Linux Server
* Cloud Server
* Docker Host

សម្រាប់ Production គួរប្រើ Environment Variables និង Logging ឱ្យបានត្រឹមត្រូវ។

---

## ⚠️ Troubleshooting

### `TELEGRAM_TOKEN មិនមានក្នុង .env`

ពិនិត្យ `.env`:

```env
TELEGRAM_TOKEN=YOUR_BOT_TOKEN
```

---

### `OPENROUTER_API_KEY មិនមានក្នុង .env`

ពិនិត្យ៖

```env
OPENROUTER_API_KEY=YOUR_API_KEY
```

---

### Admin Notification មិនដំណើរការ

ពិនិត្យ៖

```env
ADMIN_ID=YOUR_TELEGRAM_ID
```

ប្រសិនបើ `ADMIN_ID` មិនមាន Bot នៅតែអាចដំណើរការ ប៉ុន្តែ **New User Notifications** នឹងត្រូវបានបិទ។

---

### AI មិនឆ្លើយ

ពិនិត្យ៖

1. OpenRouter API Key
2. Internet Connection
3. Model Name
4. OpenRouter API Status
5. Terminal Logs

---

### Bot មិន Reply

ពិនិត្យ៖

1. Bot Token
2. Telegram Business configuration
3. Bot process កំពុង Run ឬអត់
4. Terminal Error
5. Telegram message type

---

## 🔒 Security Checklist

មុន Deploy Production សូមពិនិត្យ៖

* [ ] `.env` មិនត្រូវ Upload ទៅ GitHub
* [ ] API Keys មិនត្រូវ Hard-code
* [ ] Bot Token មិនត្រូវ Public
* [ ] Database Backup
* [ ] Logging មិនត្រូវបង្ហាញ Secret
* [ ] Rate Limiting
* [ ] Error Handling
* [ ] Server Firewall
* [ ] Regular Dependency Updates

---

## 📜 License

This project is provided for personal and educational use.

You may modify and improve the source code according to your project requirements.

---

## 👨‍💻 Author

**HeaNg**

Telegram: `@mengheang25`

---

## ⭐ Support

ប្រសិនបើ Project នេះមានប្រយោជន៍ សូម ⭐ Star Repository និង Share Project ទៅអ្នកដទៃ។

---

## ❤️ Credits

Built with:

* Python
* Telegram Bot API
* python-telegram-bot
* OpenRouter AI
* SQLite
* Requests
* python-dotenv

---

> 🤖 **Telegram AI Auto Reply Bot — Smart replies, conversation memory, and automated customer support.**
