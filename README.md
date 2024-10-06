import logging
from telegram import Update
from telegram.ext import Application, CommandHandler, ContextTypes

# Your bot token
TOKEN = " "

# Enable logging for easier debugging
logging.basicConfig(
    format='%(asctime)s - %(name)s - %(levelname)s - %(message)s',
    level=logging.INFO
)
logger = logging.getLogger(__name__)


# Define the start command handler
async def start(update: Update, context: ContextTypes.DEFAULT_TYPE):
    await update.message.reply_text(
        """
        Welcome! You can use the following commands:

        /start -> Information about buying and selling BGMI IDs
        /buy -> Get the Instagram account for buying BGMI IDs
        /sell -> Get the Instagram account for selling BGMI IDs
        /contact -> Contact us for further queries
        """
    )


# Define the buy command handler
async def buy(update: Update, context: ContextTypes.DEFAULT_TYPE):
    await update.message.reply_text(
        "Instagram Account to buy: @igaccount"
    )


# Define the sell command handler
async def sell(update: Update, context: ContextTypes.DEFAULT_TYPE):
    await update.message.reply_text(
        "Instagram Account to sell: @igaccount"
    )


# Define the contact command handler
async def contact(update: Update, context: ContextTypes.DEFAULT_TYPE):
    await update.message.reply_text(
        "Instagram Account to contact: @igaccount"
    )


# Main function to start the bot
async def main():
    # Create the Application and pass the bot's token
    application = Application.builder().token(TOKEN).build()

    # Add command handlers to the application
    application.add_handler(CommandHandler("start", start))
    application.add_handler(CommandHandler("buy", buy))
    application.add_handler(CommandHandler("sell", sell))
    application.add_handler(CommandHandler("contact", contact))

    # Start the bot and keep it running
    logger.info("Bot is running...")
    await application.start_polling()
    await application.idle()


# Run the bot
if __name__ == "__main__":
    import asyncio

    asyncio.run(main()
