✈️ AI-Powered Travel Agent – n8n Workflow
This repository contains an intelligent, fully-automated travel agent workflow built using n8n. It uses OpenAI (Langchain), Google Gemini, SerpAPI, Tavily, and Retell AI to collect user travel preferences, generate travel plans, and initiate voice calls to customers with complete travel itineraries.

🔧 Features
📋 Collects user travel input via formTrigger

🌍 Converts cities to airport codes using Gemini & LangChain

📆 Validates future travel dates

🎯 Searches for:

🔍 Activities using Tavily

🏨 Hotels using SerpAPI (Google Hotels)

✈️ Flights using SerpAPI (Google Flights)

🤖 Generates a detailed travel plan summary using Langchain Agent

📞 Initiates a real phone call to the customer with the summary using Retell AI

🧠 Powered by:

Google Gemini via LangChain

Structured output parsing for clarity and voice-readability

⚙️ Workflow Structure
📥 Form Input (User Data)
Triggered via a public form with fields:

Name

Phone Number

Origin & Destination

Travel Dates

Traveler Count

Activities

🔄 Data Flow & Processing
Step	Node	Function
1	formTrigger	Accepts user input
2	Set Fields	Normalizes data
3	Airport Codes & Dates	Converts cities to IATA codes + validates dates
4	Activities1	Tavily API to fetch activity ideas
5	Resorts1	SerpAPI to fetch hotel options
6	Flights1	SerpAPI to fetch flight options
7	Travel Plan Generator	Compiles a detailed, structured summary
8	Retell AI Voice Call	Calls customer with the travel plan
9	Response1	(Optional) Logs voice call outcome

🧠 Tech Stack
Tool	Usage
n8n	Low-code workflow automation
LangChain	Prompt templates, output parsers
Google Gemini	Natural language understanding
Tavily API	Activity suggestions
SerpAPI	Hotels & Flights
Retell AI	Voice call with LLM-generated script
Webhook/FormTrigger	User input interface

🔐 Credentials Used
Set your credentials via n8n's Credentials Manager:

Google Gemini (via Langchain)

Tavily API – httpHeaderAuth

SerpAPI – httpQueryAuth

Retell AI – httpCustomAuth

📦 How to Use
Clone this repo:

bash
Copy
Edit
git clone https://github.com/harshsri873/Travel-agent-n8n.git
Import the workflow into your n8n instance.

Set up credentials in n8n:

Google Gemini (Palm API)

Tavily API

SerpAPI

Retell AI (Phone call API)

Deploy the formTrigger webhook publicly for input.

Submit a form → Get a call!

📄 Example Output
Fully structured trip summary

Suggested flights with times & pricing

Hotel names with amenities

Local activities based on user interests

Sent via Retell AI Voice Call

📞 Voice Agent Sample Prompt
“Hi there! This is TrueHorizon, your personal travel assistant. I’m calling with your requested vacation plan…”

✨ Future Improvements
Add multilingual support

Improve date/time formatting with user locale

Integrate Google Calendar event creation

Store trip plans in a Notion/Google Sheet backend

