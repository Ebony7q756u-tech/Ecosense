# Ecosense
An AI-powered personal carbon footprint tracker. Built for Hack2Skill PromptWars Challenge 3 using multimodal LLM prompting (Vision &amp; Audio) to calculate daily emission.



EcoSense: Personal Carbon Intelligence

EcoSense is an AI-powered carbon footprint tracker designed to make sustainability tracking frictionless. Instead of manually searching for emission factors, users can simply upload a picture of a receipt or speak naturally about their day, and the AI handles the data extraction and CO2 calculation.

Built for Hack2Skill: PromptWars (Challenge 3)

🚀 Why This Fits PromptWars

This project relies heavily on advanced prompt engineering and orchestration rather than a heavy backend:

Multimodal Vision Prompting: Extracts structured JSON data (item quantities, fuel types, exact kWh) directly from user-uploaded images of electricity bills or grocery receipts.

Audio/Text Parsing: Uses specific LLM system constraints to translate natural language ("I took a 15km bus ride and ate dal rice") into calculated carbon metrics.

AI Debate Mode & Coaching: Features custom system prompts that act as a climate scientist to debate users on their sustainability claims or offer targeted weekly coaching.

✨ Features

Zero-Friction Logging: Log daily transport, food, energy, and shopping data.

Photo / Receipt Scanner (Vision AI): Upload a bill and the AI auto-fills your log.

Voice Logging: Speak your daily activities to automatically calculate your footprint.

Dynamic Dashboard: Real-time visual tracking of your weekly average, planetary health meter, and streak.

Localised Data (India Mode): Adjusts calculations based on regional Indian city grids.

Shareable Assets: Generates social-ready carbon report cards and exportable PDF/HTML reports for blog submissions.

🛠️ Tech Stack

Frontend: Vanilla HTML, CSS, JavaScript (Zero dependencies, single-file architecture).

AI Engine: Google Gemini 2.5 Flash / Anthropic Claude 3.5 Sonnet (Bring Your Own Key architecture).

Storage: Browser localStorage (No database required for the prototype).

--> How to Run It (For Judges)

This app is a client-side prototype. It requires no installation, no server, and no npm packages.

Open the live GitHub Pages link (or download and open index.html in Chrome).

Click "Continue as Guest" or create a local test account.

Go to the Dashboard tab.

Paste a valid Gemini or Claude API Key into the "AI API KEYS" manager box and click "Validate & Save".

Head over to the Tools tab to test the Voice Logging or Receipt Scanner!

Security Note for Reviewers: Because this is a zero-dependency frontend prototype built for a hackathon, API calls are made directly from the browser. The "Bring Your Own Key" (BYOK) approach ensures user keys are only stored locally in the browser's localStorage and are never sent to a third-party backend.
