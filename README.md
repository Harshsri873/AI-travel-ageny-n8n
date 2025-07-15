# ✈️ Travel Agent AI Workflow — n8n Automation

This is an **AI-powered Travel Agent** built using **n8n**, OpenAI, LangChain, SerpAPI, Tavily, and Gmail. It automatically receives user travel preferences, searches for flights, resorts, and activities, and then generates and sends a curated travel plan via email.

---

## 📌 Overview

This workflow handles a POST request with travel data, processes it using AI and APIs, and returns a full travel itinerary via email. It integrates:

- **OpenAI GPT-4o** and **Claude 3.5** for NLP
- **SerpAPI** for Google Flights & Hotels
- **Tavily** for activity recommendations
- **Gmail API** to send formatted travel plans via email

---

## 🧠 Workflow Logic

### 1. **Webhook Trigger**

- **Node:** `Webhook`
- **Endpoint:** `/travel`
- **Method:** `POST`
- **Input Fields:**  
  - `origin`, `destination`, `departure_date`, `return_date`, `travelers`, `activities`, `email`

---

### 2. **Field Assignment**

- **Node:** `Set Fields`  
  Extracts and assigns POST body fields to variables for downstream use.

---

### 3. **Airport Code + Date Validation via AI**

- **Node:** `Airport Codes & Dates`
- **Uses:** OpenAI GPT-4o
- **Function:** Converts city names to airport codes & ensures dates are future-valid.
- **Output Schema:** Validated `{ origin, destination, departure, return }`

---

### 4. **Activity Search**

- **Node:** `Activities`
- **API:** Tavily
- **Query:** `"activities in {destination}"`
- **Returns:** Top 3 activity recommendations.

---

### 5. **Hotel Search**

- **Node:** `Resorts`
- **API:** SerpAPI (Google Hotels Engine)
- **Params:** Based on validated destination and dates
- **Returns:** Resort name, price, image, link, and amenities.

---

### 6. **Flight Search**

- **Node:** `Flights`
- **API:** SerpAPI (Google Flights Engine)
- **Params:** Airport codes and travel dates
- **Returns:** Top 2 flight options with price, airline, duration, and features.

---

### 7. **Email Drafting via AI Agent**

- **Node:** `Email Agent`
- **Prompted With:** Flights, resorts, and activities
- **LLMs:** Uses both **GPT-4o** and **Claude 3.5**
- **Output Format:** HTML structured email with sections:
  - Introduction
  - Flights
  - Resorts
  - Activities
  - Sign-off

---

### 8. **Email Output Parsing**

- **Node:** `Subject & Email`
- **Schema:** Extracts `{subject, emailBody}` from AI agent output.

---

### 9. **Email Delivery**

- **Node:** `Send Plan`
- **Service:** Gmail API
- **To:** User email
- **Subject:** Travel itinerary subject
- **Body:** HTML email with links, images, and activities

---

### 10. **Webhook Response**

- **Node:** `Response + Respond to Webhook`
- **Returns:** Confirmation message back to the sender:
  ```
  "An email has been sent with the travel plan for: {subject}"
  ```

---

## 🗂 Input Example (POST Body)

```json
{
  "origin": "Delhi",
  "destination": "Paris",
  "departure_date": "2025-08-10",
  "return_date": "2025-08-20",
  "travelers": 2,
  "activities": "romantic dinner, museum, river cruise",
  "email": "user@example.com"
}
```

---

## 🧰 Tech Stack

| Tool | Purpose |
|------|---------|
| **n8n** | Automation platform |
| **OpenAI (GPT-4o)** | Natural Language Processing |
| **Claude 3.5** | Alternative AI model |
| **SerpAPI** | Flights and Hotels data |
| **Tavily** | Curated activity search |
| **Gmail API** | Email delivery |

---

## 📬 Output Sample

A fully formatted HTML email with:

- 🛫 **Flight options** (airline, time, duration, price)
- 🏨 **Top resorts** (images, pricing, nearby places)
- 🎯 **Activities** (with clickable links and summaries)

---

## ✅ Use Case

This automation is ideal for:

- Travel agencies
- AI personal assistant products
- Conversational IVRs (integrated with voice/webchat)
- Concierge services

---

## 🧪 Tips for Testing

- Use Postman or any HTTP client to test `POST` at:
  ```
  http://<n8n-instance>/webhook/travel
  ```
- Ensure all credentials (Gmail, OpenAI, SerpAPI, Tavily) are set in n8n.
- Use sandbox/testing email during development.

---

## ✨ Credits

Built by **TrueHorizon AI Team** using LLMs + automation — making travel simpler, smarter, and more magical ✨
