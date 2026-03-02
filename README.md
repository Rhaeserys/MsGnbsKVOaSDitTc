# 🚀 Smart ₿itcoin Trading System: Hybrid DCA + ATR
A professional-grade, "Full Stack" algorithmic trading bot designed for 24/7 Bitcoin market participation. This system combines **Dollar Cost Averaging (DCA)** with a dynamic **Average True Range (ATR)** volatility-based stop-loss engine. It integrates multiple data sources and provides real-time alerts via Telegram and email.

## 🛠 Features
- **Hybrid Strategy:** Combines conservative DCA buying with volatility-aware risk management using ATR.

- **Multi-Source Data:** Pulls live market data from yfinance, with hooks for CoinMarketCap and Investing.com.

- **Dynamic Configuration:** Remotely manage trading parameters (budget, drop %, etc.) via Google Sheets or a local JSON cache.

- **Real-time Alerts:** Instant trade notifications via Telegram and a formatted weekly performance report via *Gmail.*

- **Resilient Design:** Implements robust error handling and silent fallbacks for API outages or missing configuration files.

## 📋 Prerequisites
Before running the bot, ensure you have **Python 3.10+** installed. You will also need to install the following core dependencies:
```bash
# Core data and technical analysis libraries
pip install yfinance pandas pandas_ta_classic numpy

# Automation and Communication
pip install schedule python-telegram-bot requests beautifulsoup4 python-dotenv

# Google Sheets Integration
pip install gspread oauth2client
```
## ⚙️ Configuration (.env setup)
The bot uses a <mark>.env</mark> file to manage sensitive credentials securely. **Never commit your actual* <mark>.env</mark> *file to GitHub.**

Create a file named <mark>.env</mark> in the root directory.

Copy the following template and fill in your details:
```Ini,TOML
# --- Google Cloud Platform ---
# Path to your Service Account JSON (Leave empty "" to use local config_cache.json)
GCP_SERVICE_ACCOUNT_FILE=""

# --- Telegram Bot API ---
# Get these from @BotFather and @IDBot on Telegram
TELEGRAM_BOT_TOKEN="your_bot_token_here"
TELEGRAM_CHAT_ID="your_chat_id_here"

# --- Email Reporting (Gmail) ---
# Use an "App Password" from Google Account Security settings
GMAIL_ADDRESS="your_email@gmail.com"
GMAIL_APP_PASSWORD="your_app_password_here"

# --- External APIs ---
# Get a free key from https://coinmarketcap.com/api/
CMC_API_KEY="your_cmc_key_here"
```
## 🚀 Getting Started
1. Local Configuration
The bot relies on a <mark>config_cache.json</mark> file as a fallback if Google Sheets is not used. Create this file in the root directory:
```JSON
{
  "BUDGET_USD": 10000,
  "DCA_DROP_PERCENT": 0.03,
  "DCA_AMOUNT": 500,
  "ATR_K_MULTIPLIER": 1.5
}
```
2. Running the Bot
Once your <mark>.env</mark> and <mark>config_cache.json</mark> files are ready, launch the bot:
```Bash
python bot_main.py
```
3. Understanding the Output
- **Initial Run:** The bot will execute an initial DCA buy to establish a portfolio position.

- **Loop:** Every 30 minutes, the bot "wakes up," checks for price drops (DCA), and recalculates the ATR stop-loss.

- **Notifications:** You will receive a Telegram message for every buy/sell and a Gmail summary every Monday morning.
## 📊 Project Structure
```Plaintext
├── bot_main.py           # Main trading engine and logic
├── .env                  # Private credentials (ignored by git)
├── .env.example          # Template for other users
├── config_cache.json     # Local trading parameters fallback
├── requirements.txt      # List of all python dependencies
└── README.md             # Project documentation
```
## ⚠️ Disclaimer
*This software is for educational purposes only. Do not trade money you cannot afford to lose. Crypto trading involves significant risk.*
