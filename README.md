# ✈️ AI-Powered Travel Agent – n8n Workflow

This repository contains an intelligent, fully-automated travel agent workflow built using [n8n](https://n8n.io). It uses OpenAI (Langchain), Google Gemini, SerpAPI, Tavily, and Retell AI to collect user travel preferences, generate travel plans, and initiate voice calls to customers with complete travel itineraries.

---

## 🔧 Features

- 📋 Collects user travel input via **formTrigger**
- 🌍 Converts cities to **airport codes** using Gemini & LangChain
- 📆 Validates **future travel dates**
- 🎯 Searches for:
  - 🔍 **Activities** using **Tavily**
  - 🏨 **Hotels** using **SerpAPI (Google Hotels)**
  - ✈️ **Flights** using **SerpAPI (Google Flights)**
- 🤖 Generates a detailed **travel plan summary** using Langchain Agent
- 📞 Initiates a real **phone call** to the customer with the summary using **Retell AI**
- 🧠 Powered by:
  - Google Gemini via LangChain
  - Structured output parsing for clarity and voice-readability

---

## ⚙️ Workflow Structure

### 📥 Form Input (User Data)

Triggered via a public form with fields:
- Name
- Phone Number
- Origin & Destination
- Travel Dates
- Traveler Count
- Activities

### 🔄 Data Flow & Processing

| Step | Node | Function |
|------|------|----------|
| 1 | `formTrigger` | Accepts user input |
| 2 | `Set Fields` | Normalizes data |
| 3 | `Airport Codes & Dates` | Converts cities to IATA codes + validates dates |
| 4 | `Activities1` | Tavily API to fetch activity ideas |
| 5 | `Resorts1` | SerpAPI to fetch hotel options |
| 6 | `Flights1` | SerpAPI to fetch flight options |
| 7 | `Travel Plan Generator` | Compiles a detailed, structured summary |
| 8 | `Retell AI Voice Call` | Calls customer with the travel plan |
| 9 | `Response1` | (Optional) Logs voice call outcome |

---

## 🧠 Tech Stack

| Tool | Usage |
|------|-------|
| **n8n** | Low-code workflow automation |
| **LangChain** | Prompt templates, output parsers |
| **Google Gemini** | Natural language understanding |
| **Tavily API** | Activity suggestions |
| **SerpAPI** | Hotels & Flights |
| **Retell AI** | Voice call with LLM-generated script |
| **Webhook/FormTrigger** | User input interface |

---

## 🔐 Credentials Used

> Set your credentials via `n8n`'s **Credentials Manager**:

- Google Gemini (via Langchain)
- Tavily API – `httpHeaderAuth`
- SerpAPI – `httpQueryAuth`
- Retell AI – `httpCustomAuth`

---

## 📦 How to Use

1. **Clone this repo**:
   ```bash
   git clone https://github.com/your-username/AI-travel-agent-n8n.git
