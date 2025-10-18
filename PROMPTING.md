📒 PROMPTING.md — Five Examples (Prompt → Technique → Why it helped + Before/After)

Below is one focused example that combines your prompt, the intentional prompting technique used, why it helped, and Before/After code. It also links back to assessment requirements (modular design, error handling, testing, visuals, documentation quality).

1) UI Planning and Advice Helper

Topic: Planning the ipywidgets UI and adding get_temperature_advice
Prompt: “I want a simple ipywidgets UI where users type a location and click buttons like Show Chart or Ask AI. How should I start?”
Technique: Restate the problem and identify inputs and outputs
Why it helped: It forced a clear component plan before code and avoided mixing UI with logic.

Before
# Idea only. No structure for widgets, no separation of UI vs logic.

AI Response (summary)

Create widgets: Text (location), Int (days), Buttons (Fetch, Temp Chart, Precip Chart, Ask AI, Quit), and an Output area.

Wire small handlers that call focused functions.

Add a helper get_temperature_advice(avg_c) for user guidance.

After
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


Measurable Impact: Faster development and fewer refactors later because UI elements and roles were fixed up front.
Requirement Links:

Modular design

Documentation quality (clear function purpose)

UX clarity
