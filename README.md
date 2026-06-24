# 🌍 AI Autonomous Travel Planner

> **Multi-agent AI system that does in 2 minutes what a travel agent takes 2 days to do.**

---

## ❗ The Problem

Planning a trip today is **broken**:

| Pain Point | Reality |
|---|---|
| 🕐 **Time-consuming** | Switching between 10+ tabs — Google Flights, Booking.com, TripAdvisor, Visa portals, weather apps, currency converters… |
| 💸 **Expensive** | Travel agents charge 10–20% commission. Premium trip planners cost ₹2,000–₹10,000 per plan |
| 🤯 **Overwhelming** | Thousands of options for flights, hotels, activities — no single place to compare and decide |
| 📋 **No personalisation** | Generic tour packages ignore your budget, interests, travel style, and nationality |
| 🚫 **Missing critical info** | Travellers forget to check visa requirements, safety advisories, local emergency numbers, vaccination needs |
| 📵 **No post-plan support** | Once you have a plan, you still have to manually contact airlines, hotels, and figure out local transport |

**Result**: The average traveller spends **8–12 hours** researching before booking a trip — and still misses important things.

---

## ✅ What We Built

**AI Autonomous Travel Planner** is a **12-agent AI system** that automatically researches, plans, and delivers a complete travel itinerary — in under 2 minutes.

You enter: **Destination + Origin + Dates + Budget + Interests**

The system spins up **12 specialized AI agents** in parallel, each an expert in one domain:

```
User Input → LangGraph StateGraph → Planner (Router)
                                        │
            ┌───────────────────────────┼───────────────────────────┐
            ▼               ▼           ▼           ▼               ▼
      Research Agent   Weather Agent  Flight Agent  Train Agent  Cab Agent
      (search_web)    (OpenWeather)   (search_web) (search_web) (search_web)
            │               │           │
            └───────────────┼───────────┘
                            ▼
              Hotel → Activity → Visa → Safety → Budget → Itinerary → Booking
                            │
                            ▼
                  Complete Trip Plan (JSON)
                  + Email + WhatsApp Notification
```

### 🤖 The 12 Agents

| # | Agent | What It Does |
|---|-------|-------------|
| 1 | 🔍 **Research** | Scrapes the web for destination guides, tips, hidden gems, local culture |
| 2 | 🌤️ **Weather** | Live 5-day forecast from OpenWeatherMap + packing & clothing advice |
| 3 | ✈️ **Flight** | Searches real-time flights (Google Flights, Skyscanner, Kayak) with prices |
| 4 | 🚂 **Train** | Finds IRCTC / Eurail / Amtrak options with class-wise pricing |
| 5 | 🚖 **Cab** | Airport transfers, Ola/Uber/Grab local transport options with cost/km |
| 6 | 🏨 **Hotel** | Budget, mid-range & luxury picks from Booking.com, Hotels.com, Airbnb |
| 7 | 🎯 **Activity** | Categorised recommendations — adventure, culture, food, family, nightlife |
| 8 | 📋 **Visa** | Current official visa requirements, fees, processing time, required docs |
| 9 | 🛡️ **Safety** | Travel advisories, emergency numbers, scam alerts, health & vaccination tips |
| 10 | 💰 **Budget** | Full cost breakdown with daily budget, surplus/deficit flag, savings tips |
| 11 | 📅 **Itinerary** | Day-by-day plan with morning / afternoon / evening slots |
| 12 | 📱 **Booking** | Direct booking links, step-by-step instructions for flights, hotels, trains |

### 🛠️ Tech Stack

| Layer | Technology |
|-------|-----------|
| **UI** | Streamlit — Dark Glassmorphism theme |
| **LLM** | Groq `llama-3.3-70b-versatile` (ultra-fast inference) |
| **Agent Framework** | LangChain `create_agent` |
| **Orchestration** | LangGraph `StateGraph` |
| **Web Search** | Playwright MCP (Browser) + DuckDuckGo fallback |
| **Memory / RAG** | ChromaDB + Sentence Transformers |
| **Weather API** | OpenWeatherMap (live 5-day forecast) |
| **Currency API** | ExchangeRate API (live FX rates) |
| **Notifications** | Twilio WhatsApp + Gmail SMTP |
| **Caching** | MD5-keyed local JSON cache (instant repeat queries) |

---

## 💰 The Profit (Value Created)

### For Users

| Metric | Traditional | AI Travel Planner |
|--------|-------------|-------------------|
| ⏱️ **Time to get a full plan** | 8–12 hours | **< 2 minutes** |
| 💸 **Cost of planning** | ₹2,000–₹10,000 (agent fee) | **₹0** |
| 🌐 **Sources checked** | 3–5 sites manually | **Live web scraping across 10+ platforms** |
| 📋 **Coverage** | Flights + Hotel (usually) | **12 categories end-to-end** |
| 🚨 **Visa & Safety info** | Often missed | **Always included** |
| 📲 **Delivery** | PDF / WhatsApp forward | **WhatsApp + Email + JSON + ICS Calendar** |

### Market Opportunity

- 🌏 **1.4 billion** international trips taken annually (UNWTO 2024)
- 📱 **65%** of travellers research on mobile before booking
- 💼 Global online travel market: **$1.2 trillion** (projected 2027)
- 🤖 AI travel tech market growing at **28% CAGR**

### Business Model Options

| Model | Revenue |
|-------|---------|
| **SaaS Subscription** | ₹199–₹999/month per user |
| **Affiliate Commissions** | 2–8% on every flight/hotel booking routed through the app |
| **B2B API** | Sell the planning engine to travel agencies & OTAs |
| **White-label** | License to airlines, banks (credit card travel perks) |
| **Freemium** | Free basic plan; paid for WhatsApp alerts + priority agents |

---

## ⚡ Quick Start

```bash
# 1. Setup environment
python -m venv venv
source venv/bin/activate
pip install -r requirements.txt
playwright install

# 2. Install Browser MCP
npm install

# 3. Add your API keys
cp .env.example .env   # edit with your keys

# 4. Terminal 1 — start Browser MCP
npm run mcp

# 5. Terminal 2 — start the app
streamlit run main.py
```

> **Open** → http://localhost:8501

---

## 🔑 API Keys Required

| Key | Where to Get | Cost |
|-----|-------------|------|
| `GROQ_API_KEY` | [console.groq.com](https://console.groq.com) | Free tier available |
| `OPENWEATHER_API_KEY` | [openweathermap.org/api](https://openweathermap.org/api) | Free (1,000 calls/day) |
| `EXCHANGERATE_API_KEY` | [exchangerate-api.com](https://www.exchangerate-api.com) | Free (1,500 calls/month) |
| `TWILIO_*` | [twilio.com](https://twilio.com) | Free trial credits |
| `EMAIL_ADDRESS` + `EMAIL_PASSWORD` | [Gmail App Password](https://myaccount.google.com/apppasswords) | Free |

---

## 📂 Project Structure

```
AI Autonomous Travel Planner/
├── agents.py          # 12 agents — create_agent + @tool definitions
├── workflow.py        # LangGraph StateGraph orchestrator
├── main.py            # Streamlit UI (Premium Dark Glassmorphism)
├── mcp_client.py      # Browser MCP + DuckDuckGo fallback
├── config.py          # Environment config loader
├── utils.py           # JSON parsing, currency, date helpers
├── notifications.py   # WhatsApp (Twilio) + Email (SMTP) notifications
├── config.json        # MCP server definitions
├── package.json       # Node dependencies (Browser MCP)
├── requirements.txt   # Python dependencies
└── .env               # Your API keys (never commit this)
```

---

## 🙏 Built With

- [Groq](https://groq.com) — World's fastest LLM inference
- [LangChain](https://langchain.com) — Agent framework
- [LangGraph](https://langchain-ai.github.io/langgraph) — Multi-agent orchestration
- [Streamlit](https://streamlit.io) — Rapid UI
- [Playwright](https://playwright.dev) — Browser automation
- [ChromaDB](https://www.trychroma.com) — Vector memory

---

*Built by Harsh Singh · AI Autonomous Travel Planner · 2026*