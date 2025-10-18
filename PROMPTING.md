# 📒 PROMPTING.md
Below are five focused examples that combine my actual prompts, the intentional prompting technique used, why it helped, and short **Before/After** code that shows measurable improvements in stability, correctness, readability, and UX. Each example also links back to the assessment requirements: modular design, error handling, testing, visuals, and documentation quality.


---

## 1) UI Planning and Advice Helper

**Topic:** Planning the `ipywidgets` UI and adding `get_temperature_advice`  
**Prompt:** “I want a simple ipywidgets UI where users type a location and click buttons like Show Chart or Ask AI. How should I start?”  
**Technique:** Restate the problem and identify inputs and outputs  
**Why it helped:** It forced a clear component plan before code and avoided mixing UI with logic.

### Before
```python
# Idea only. No structure for widgets, no separation of UI vs logic.
```
### AI Response (summary)
- Create widgets: Text (location), Int (days), Buttons (Fetch, Temp Chart, Precip Chart, Ask AI, Quit), and an Output area.  
- Wire small handlers that call focused functions.  
- Add a helper `get_temperature_advice(avg_c)` for user guidance.

### After
```python
location_input = widgets.Text(placeholder="e.g., Sydney")
days_input = widgets.IntText(value=5, min=1, max=6)
temp_chart_button = widgets.Button(description="Show Temperature Chart")
precip_chart_button = widgets.Button(description="Show Precipitation Chart")
ask_question_button = widgets.Button(description="Ask AI")
output_area = widgets.Output()

def get_temperature_advice(avg_c: float) -> str:
    if avg_c > 32: return "Very hot. Stay hydrated."
    if avg_c >= 27: return "Warm. Sunscreen recommended."
    if avg_c >= 23: return "Comfortable."
    if avg_c >= 17: return "A bit cool. Light layer."
    return "Cold. Dress warmly."
```
---
## 2) Chart Buttons with Caching and Guards

**Topic:** Handlers for temperature and precipitation charts  
**Prompt:** “How should the temperature and precipitation chart handlers reuse data and validate inputs?”  
**Technique:** Request modular design improvements and challenge edge cases  
**Why it helped:** Reduced API calls and improved responsiveness while preventing confusing errors.

### Before
```python
def on_temp_chart_button_clicked(b):
    data = get_weather_data(location_input.value)  # refetch on every click
    create_temperature_visualisation(data, num_days=5)
```
### AI Response (summary)
- Cache the last dataset and location.  
- Validate empty location.  
- If data is missing, show a clear message and exit early.

### After
```python
if not _LAST_WEATHER or _LAST_LOCATION != loc:
    _LAST_WEATHER = get_weather_data(loc, forecast_days=6)
    _LAST_LOCATION = loc

if not _LAST_WEATHER or not _LAST_WEATHER.get("list"):
    print("Weather data is not available. Please fetch weather first.")
    return

create_temperature_visualisation(_LAST_WEATHER, num_days=days_input.value)
```
---
