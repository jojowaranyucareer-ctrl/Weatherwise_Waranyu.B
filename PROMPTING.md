# 📒 PROMPTING.md
Below are five focused examples that combine my actual prompts, the intentional prompting technique used, why it helped, and short **Before/After** code that shows measurable improvements in stability, correctness, readability, and UX. Each example also links back to the assessment requirements: modular design, error handling, testing, visuals, and documentation quality.


---
## ✅ Demonstrates at Least 5 Intentional Prompting Techniques

1) **Restate the problem & clarify scope**  
   - *Example:* “I want a simple `ipywidgets` UI… How should I start?”  
   - *Impact:* Produced a clear component plan (inputs/outputs, widgets, handlers) before coding.  
   - *See:* Example 1 (UI planning and advice helper)

2) **Identify inputs/outputs explicitly**  
   - *Example:* “How should chart handlers reuse data and validate inputs?”  
   - *Impact:* Led to caching `_LAST_WEATHER`, validating `location_input`, and early exits with messages.  
   - *See:* Example 2 (Chart buttons with caching and guards)

3) **Request explanations to ensure understanding**  
   - *Example:* “Explain why `[8:16]` is used for tomorrow and how to compute averages/precip totals.”  
   - *Impact:* Corrected time-slice logic based on 3-hour cadence → accurate “tomorrow” summaries.  
   - *See:* Example 3 (Tomorrow indexing)

4) **Challenge edge cases & failure modes**  
   - *Example:* “Show me how to print keys, preview first list item, handle failures.”  
   - *Impact:* Added env-based API key, timeouts, try/except, and guards for missing `list`.  
   - *See:* Example 4 (Retrieval stability and live testing)

5) **Iterative improvement of initial solution**  
   - *Example:* “Ensure labels are readable and dates are sorted.”  
   - *Impact:* Sorted dates, rotated labels, `tight_layout()` → clearer charts without changing data logic.  
   - *See:* Example 5 (Visualisation readability)

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
## 3) Correct Tomorrow Indexing Using 3-Hour Cadence

**Topic:** Getting tomorrow’s summary from 3-hour forecasts  
**Prompt:** “Explain why [8:16] is used for tomorrow and show how to compute averages and precipitation totals.”  
**Technique:** Ask for code explanations to ensure understanding  
**Why it helped:** Locked in the correct mapping from 3-hour slots to a full day.

### Before
```python
tomorrow_points = weather_data["list"][0:8]  # incorrect for tomorrow
```
### AI Response (summary)
- There are **8 chunks per day** at **3 hours** each.  
- Use **[8:16]** for the next day, then compute **averages** and **totals** from that slice.

### After
```python
tomorrow_points = weather_data["list"][8:16]

avg_temp = sum(i["main"]["temp"] for i in tomorrow_points) / len(tomorrow_points)

precip = sum(
    i.get("rain", {}).get("3h", 0) + i.get("snow", {}).get("3h", 0)
    for i in tomorrow_points
)
```
---
## 4) Retrieval Stability and Live Testing

**Topic:** Testing `openWeather_getWeather` and `get_weather_data` and handling failures  
**Prompt:** “I want to test `openWeather_getWeather` and `get_weather_data` for London and Tokyo. Show me how to print keys, the first list item, and handle failures.”  
**Technique:** Identify inputs and outputs, then iterate based on tests  
**Why it helped:** Validated structure early, exposed missing keys and network issues, stabilized downstream logic.

### Before
```python
def openWeather_getWeather(city, units="metric"):
    return requests.get(url).json()  # no key check, no timeout, no try/except
```
### AI Response (summary)
- Read API key from environment, not from code.  
- Add a request timeout and wrap in `try/except`.  
- Print top-level keys and preview the first forecast entry.  
- Guard for a missing `list` in the response.

### After
```python
def openWeather_getWeather(city: str, units: str = "metric"):
    api_key = os.getenv("OPENWEATHER_API_KEY")
    if not api_key:
        return None
    try:
        url = (
            "https://api.openweathermap.org/data/2.5/forecast"
            f"?q={city}&appid={api_key}&units={units}"
        )
        resp = requests.get(url, timeout=15)
        return resp.json()
    except Exception as e:
        print(f"Error fetching weather data: {e}")
        return None

# Tests
if weather_raw_data:
    print(list(weather_raw_data.keys()))
    if weather_raw_data.get("list"):
        print(weather_raw_data["list"][0])
```
---
## 5) Visualisation Readability and Date Order

**Topic:** Temperature and precipitation charts for 3 days and 5 days  
**Prompt:** “Test both charts for 5 days and 3 days. Ensure labels are readable and dates are sorted.”  
**Technique:** Iterative improvement of initial solution  
**Why it helped:** Improved chart clarity without changing data logic.

### Before
```python
sliced_dates = list(daily_temps.keys())[:num_days]
plt.xticks(rotation=0)
```
### AI Response (summary)
- Sort the dates before slicing.  
- Rotate x labels and use `tight_layout()` to prevent overlap.

### After
```python
sorted_dates = sorted(daily_temps.keys())
sliced_dates = sorted_dates[:num_days]
plt.xticks(rotation=45)
plt.tight_layout()
```
---
## Conclusion — Benefits of Intentional Prompting

Intentional prompting made my development process faster, clearer, and more reliable. By deliberately shaping each AI exchange (restate the goal → ask for structure → probe edge cases → iterate with tests), I gained these concrete benefits:

- **Stability & Error Handling:** Prompts that targeted failure modes (missing API key, invalid city, absent `list`) led to robust guards, timeouts, and graceful fallbacks—preventing crashes in Colab and improving user-facing messages.
- **Correctness:** Asking for explanations (e.g., the 3-hour cadence and `[8:16]` slice) locked in accurate tomorrow summaries and consistent metrics across functions.
- **Readability & Modularity:** Requests for modular refactors produced small, single-purpose functions (retrieval, processing, visualisation, conversation), clearer names, and docstrings—easier to maintain and extend.
- **User Experience (UX):** Iterative prompts about charts and UI handlers improved label legibility, date ordering, and responsiveness (caching last dataset), which made the dashboard feel polished.
- **Testing Discipline:** Prompts that asked for test scaffolds and previews (keys, first list item) gave quick validation loops, revealing edge cases early and shrinking debugging time.
- **Assessment Alignment:** Each improvement maps to rubric items—**modular design**, **error handling**, **testing breadth**, **visualisation quality**, and **documentation quality**—with before/after code to demonstrate progress.


---

