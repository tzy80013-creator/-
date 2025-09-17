from pyrogram import Client, filters
import os

API_ID = int(os.getenv("API_ID"))
API_HASH = os.getenv("API_HASH")
BOT_TOKEN = os.getenv("BOT_TOKEN")
SESSION = os.getenv("SESSION")

app = Client(
    name="KianSource",
    api_id=API_ID,
    api_hash=API_HASH,
    bot_token=BOT_TOKEN,
    session_string=SESSION
)

# رسالة الترحيب
@app.on_message(filters.command("start") & filters.private)
async def start(_, message):
    await message.reply_text(
        "👋 أهلاً بك في **سورس كيان**\n"
        "✨ المطور: كيان\n"
        "📡 قناة السورس: @k_ian_1"
    )

# أمر كتم
muted = set()

@app.on_message(filters.command("كتم", prefixes=".") & filters.group)
async def mute(_, message):
    if message.reply_to_message:
        user_id = message.reply_to_message.from_user.id
        muted.add(user_id)
        await message.reply_text(
            f"🤫 هشش ولا نفس!\n✅ تم كتم {message.reply_to_message.from_user.mention}"
        )

# أمر الغاء كتم
@app.on_message(filters.command("الغاءكتم", prefixes=".") & filters.group)
async def unmute(_, message):
    if message.reply_to_message:
        user_id = message.reply_to_message.from_user.id
        if user_id in muted:
            muted.remove(user_id)
            await message.reply_text(
                f"🔊 تم إلغاء الكتم عن {message.reply_to_message.from_user.mention}"
            )

# حماية من رسائل المكتومين
@app.on_message(filters.text & filters.group)
async def block_muted(_, message):
    if message.from_user and message.from_user.id in muted:
        await message.delete()

print("🚀 سورس كيان جاهز للعمل ...")
app.run()
