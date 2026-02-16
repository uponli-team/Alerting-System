# 📈 n8n Telegram Stock Alert Bot

Automated Telegram alerting system built with **n8n** for:

- 🔥 Market Catalysts (FDA, partnerships, earnings news, profit headlines)
- 📅 Upcoming Earnings Alerts
- 🚀 Technical Breakout Alerts  
- 🌙 Quiet Hours Filtering

---

## 🧠 Overview

This workflow connects a Telegram bot with financial data APIs to automatically:

- Fetch stock news and detect major catalysts  
- Scan for breakout signals  
- Monitor upcoming earnings  
- Filter alerts based on custom rules  
- Respect quiet hours before sending notifications  

All alerts are delivered directly to Telegram in formatted Markdown messages.

---

## 🛠 Tech Stack

- n8n
- Telegram Bot API
- Finnhub API
- Financial Modeling Prep API
- TradingView

---

## 🔌 APIs Used

### 1️⃣ Finnhub
- General News  
- Earnings Calendar  
- Technical Scan  

### 2️⃣ Financial Modeling Prep
- Earnings Calendar Data  

---

## 🔄 Workflow Architecture

```
Telegram Trigger
      ↓
Extract Message Data
      ↓
Workflow Configuration
      ↓
 ┌───────────────┬────────────────┬─────────────────┐
 ↓               ↓                ↓
Fetch News   Fetch Breakouts   Fetch Earnings
 ↓               ↓                ↓
Filter        Filter          Revenue/EPS Filter
 ↓               ↓                ↓
      Merge All Alert Data
               ↓
      Check Quiet Hours
               ↓
      Route by Alert Type
     ┌────────┬────────┬─────────┐
     ↓        ↓        ↓
 Potential  Earnings  Breakout
   News      Alert      Alert
     ↓        ↓        ↓
 Telegram  Telegram  Telegram
```

---

## 🚨 Alert Types

### 🔥 Potential Market Catalyst

Triggered when headlines contain:
- `fda`
- `partnership`
- `earnings`
- `profit`

Includes:
- Headline
- Source
- Published time
- Summary preview
- TradingView link

---

### 📅 Earnings Alert

Triggered when:
- Revenue Estimate > 500M
- EPS Estimate > 0
- Earnings within 3–7 days

Includes:
- Symbol
- Revenue estimate
- EPS estimate
- Earnings date
- Quarter info

---

### 🚀 Breakout Alert

Triggered when:
- Headline equals "breakout"

Includes:
- Symbol
- Signal info
- Time
- TradingView link

---

## 🌙 Quiet Hours Logic

Configured inside `Workflow Configuration` node:

```
quietHoursStart = 22
quietHoursEnd = 7
```

If current hour:
- Less than 7  
OR  
- Greater than or equal to 22  

➡ Alerts are blocked.

---

## ⚙️ Configuration Example

Inside the Workflow Configuration node:

```json
{
  "quietHoursStart": 22,
  "quietHoursEnd": 7,
  "telegramChatId": "YOUR_CHAT_ID",
  "catalystApiUrl": "https://financialmodelingprep.com/api/v3/earning_calendar",
  "breakoutApiUrl": "https://finnhub.io/api/v1/scan/technical"
}
```

---

## 🔐 Setup Instructions

### 1️⃣ Create Telegram Bot
- Open Telegram  
- Search `@BotFather`
- Create bot  
- Copy Bot Token  

### 2️⃣ Configure n8n
- Add Telegram Trigger node
- Add Telegram credentials
- Paste bot token
- Activate workflow

### 3️⃣ Add API Keys

Replace:

```
token=YOUR_FINNHUB_API_KEY
```

Add your:
- Finnhub API key
- FinancialModelingPrep API key

---

## 📦 How It Works

1. User sends message to Telegram bot  
2. Workflow fetches:
   - News
   - Earnings
   - Breakouts  
3. Data is filtered  
4. Alerts are merged  
5. Quiet hours checked  
6. Alert routed  
7. Message sent to Telegram  

---

## 🚀 Future Improvements

- Watchlist per user
- User subscription preferences
- Database storage (Postgres)
- Volume + RSI breakout confirmation
- Rate limiting
- Multi-user support
- Web dashboard

---

## 🧩 Importing Workflow

1. Open n8n  
2. Click **Import**  
3. Paste workflow JSON  
4. Save  
5. Add credentials  
6. Activate  

---

## 📜 License

MIT License
