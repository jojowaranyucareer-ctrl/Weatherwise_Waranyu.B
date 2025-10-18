# 🌦️ WeatherWise — Smart Weather Advisor

Welcome to **WeatherWise**, a smart weather advisor application that combines live weather data with AI-powered natural language responses.  
This project is based on the **WeatherWise Assignment Starter Template**, enhanced with custom logic, visualisations, and interface design developed by **Waranyu Bancherdvanich**.

---

![Build With AI](https://img.shields.io/badge/Built_with-AI-blueviolet?logo=openai)
![Python](https://img.shields.io/badge/Made_with-Python-3776AB?logo=python)
![Visualisation](https://img.shields.io/badge/Includes-Visualisations-orange?logo=plotly)

---
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
!pip install requests matplotlib ipywidgets fetch-my-weather pyinputplus hands-on-ai

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

## 🌤️ Main Functions

| Function | Purpose |
|-----------|----------|
| `openWeather_getWeather()` | Fetches 5-day forecast data. |
| `get_temps()` | Extracts daily temperature info. |
| `create_temperature_visualisation()` | Line chart for temperature trends. |
| `create_precipitation_visualisation()` | Bar chart for rainfall. |
| `parse_weather_question()` | Understands user questions. |
| `generate_weather_response()` | AI-generated weather advice. |

---

## 🧭 User Interface

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

