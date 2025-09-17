ZThon-Kian/
├─ main.py
├─ requirements.txt
├─ Procfile
├─ railway.json
├─ README.md
├─ start.sh
└─ zthron/               # مجلد سورس ZThon
    ├─ __init__.py
    ├─ commands.py
    ├─ utils.py
    └─ ...              # باقي ملفات سورس
from zthron import bot
import os

API_ID = int(os.getenv("API_ID"))
API_HASH = os.getenv("API_HASH")
BOT_TOKEN = os.getenv("BOT_TOKEN")
SESSION = os.getenv("SESSION")

bot.start(api_id=API_ID, api_hash=API_HASH, bot_token=BOT_TOKEN, session_string=SESSION)
pyrogram==2.0.106
tgcrypto
worker: python3 main.py
{
  "build": {
    "builder": "python"
  },
  "deploy": {
    "startCommand": "python3 main.py"
  }
}
# سورس كيان مبني على ZThon

### خطوات التشغيل
1. إعداد متغيرات البيئة:
2. رفع المستودع إلى GitHub.

3. في Railway:
   - New Project → Deploy from GitHub
   - إضافة المتغيرات البيئية
   - Deploy

### أوامر أساسية
- `.start` : رسالة الترحيب
- `.كتم` : كتم مستخدم
- `.الغاءكتم` : إلغاء كتم
- بقية الأوامر داخل `zthron/commands.py`
#!/bin/bash
export API_ID=xxxx
export API_HASH=xxxx
export BOT_TOKEN=xxxx
export SESSION=xxxx
python3 main.py
