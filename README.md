# 🌦️ WeatherWise — Smart Weather Advisor

Welcome to **WeatherWise**, a smart weather advisor application that combines live weather data with AI-powered natural language responses.  
This project is based on the **WeatherWise Assignment Starter Template**, enhanced with custom logic, visualisations, and interface design developed by **Waranyu Bancherdvanich**.

---

![Build With AI](https://img.shields.io/badge/Built_with-AI-blueviolet?logo=openai)
![Python](https://img.shields.io/badge/Made_with-Python-3776AB?logo=python)
![Visualisation](https://img.shields.io/badge/Includes-Visualisations-orange?logo=plotly)

---

## 🧩 Overview

**Features**
- 🌤️ Current weather and 5-day forecast  
- 📈 Temperature and rainfall charts  
- 💬 AI-driven weather questions  
- 🧠 Smart outdoor advice (“Should I go outside tomorrow?”)

**Core Components**
- API data retrieval and processing  
- Matplotlib visualisations  
- AI conversation features  
- Interactive UI with `ipywidgets`

---

## ⚙️ Setup

Install dependencies:
```bash
!pip install hands-on-ai
!pip install pyinputplus

---

## 🔑 Set API Keys

```python
import os

os.environ['HANDS_ON_AI_SERVER'] = 'https://ollama.serveur.au'
os.environ['HANDS_ON_AI_MODEL'] = 'llama3.2'
os.environ['HANDS_ON_AI_API_KEY'] = 'YOUR_HANDS_ON_AI_API_KEY'
os.environ['OPENWEATHER_API_KEY'] = 'YOUR_OPENWEATHER_API_KEY'
```

Get your keys from:
🌐 https://openweathermap.org/
🌐 https://ollama.com/

---

## ⚙️ How It Works

**WeatherWise** follows a simple **data → analysis → AI → user output** pipeline:

---

### 🌐 1. Fetch Weather Data
- The app calls the **OpenWeather API** using the selected city and units (°C/°F).  
- Data includes temperature, humidity, rainfall, and a 5-day forecast.

---

### 🧮 2. Process and Organise Data
- Functions like `get_temps()` extract relevant fields (min/max/average).  
- The data is cleaned and structured for visualisation and AI input.

---

### 📊 3. Visualise the Forecast
- `matplotlib` generates **line charts** (temperature) and **bar charts** (rainfall).  
- Users can easily understand weather patterns at a glance.

---

### 🤖 4. AI Interaction
- User questions (e.g., *“Will it rain tomorrow in Perth?”*) are parsed by `parse_weather_question()`.  
- `generate_weather_response()` combines AI analysis with forecast data to produce natural, contextual answers.

---

## 🧭 5. User Interface

**Interactive options (via `ipywidgets`):**

- 📍 Enter location & forecast days  
- ☀️ Fetch Today’s Weather  
- 📈 Show Charts  
- 🤖 Ask AI Question  
- 👋 Quit Session  

---

## 💡 Example

**Example Interaction**

| Step | Action | Result |
|------|---------|--------|
| 1 | Enter: `Perth` | Loads weather data |
| 2 | Click: ☀️ *Fetch Weather* | Shows temperature summary |
| 3 | Ask: “Will it rain tomorrow?” | AI gives personalised advice |

---

## 🎯 Project Purpose

**WeatherWise** integrates APIs, AI, and data visualisation to make weather information more interactive and insightful.  
It demonstrates how natural language and data analytics can support everyday decisions.

---

## 🧠 AI Conversations

All prompt logs are saved in `/ai-conversations/`.  
See resources for examples and prompting tips.

