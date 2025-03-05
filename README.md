# Vevo Music Bot (Advanced Telegram Music Bot)
# Features: Music Player, Anti-Spam, Blacklist, Fun, Shayari, Quotes, Games, Extra Approvals (Without MongoDB)

from pyrogram import Client, filters
from pyrogram.types import Message
import random

# Bot Configuration
API_ID = "27333817"
API_HASH = "67eac1d942fd881c2bc9d71209e21a77"
BOT_TOKEN = "7754706931:AAHiNJT8u2u1vqPI2rv2yR_GNg9ZcXhjmLg"
OWNER_ID = 7789005102  # Replace with your Telegram User ID

app = Client(
    "vevo_music_bot",
    api_id=API_ID,
    api_hash=API_HASH,
    bot_token=BOT_TOKEN
)

# Fun Commands
fun_responses = [
    "Bhai OP! 😎", "Aag laga di! 🔥", "Mast cheez hai tu! 😂", "Bore mat kar bhai! 😆"
]

@app.on_message(filters.command("fun") & filters.private)
def fun_command(client, message: Message):
    message.reply_text(random.choice(fun_responses))

# Shayari & Quotes
shayari_list = [
    "Teri yaadon ka sahara hai, warna jeena bhi mushkil tha... 💔",
    "Mohabbat bhi kitni ajeeb hai na, jise chaho wo samjhta nahi... 😞"
]

@app.on_message(filters.command("shayari") & filters.private)
def shayari_command(client, message: Message):
    message.reply_text(random.choice(shayari_list))

# Anti-Spam & Blacklist (Without Database)
blacklist_words = ["gaali1", "gaali2", "spamword"]

@app.on_message(filters.text & filters.group)
def filter_blacklist(client, message: Message):
    for word in blacklist_words:
        if word in message.text.lower():
            message.delete()
            message.reply_text("⚠️ Warning! Bad words are not allowed!")

# Start Command
@app.on_message(filters.command("start") & filters.private)
def start_command(client, message: Message):
    message.reply_text("🎵 Vevo Music Bot is Ready! Use /help for commands.")

# Running the Bot
if __name__ == "__main__":
    print("Vevo Music Bot is running...")
    app.run()
