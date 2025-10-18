# 📒 PROMPTING.md

Below is one focused example that combines your prompt, the intentional prompting technique used, why it helped, and **Before/After** code. It also links back to assessment requirements (modular design, error handling, testing, visuals, documentation quality).

---

## 1) UI Planning and Advice Helper

**Topic:** Planning the `ipywidgets` UI and adding `get_temperature_advice`  
**Prompt:** “I want a simple ipywidgets UI where users type a location and click buttons like Show Chart or Ask AI. How should I start?”  
**Technique:** Restate the problem and identify inputs and outputs  
**Why it helped:** It forced a clear component plan before code and avoided mixing UI with logic.

### Before
```python
# Idea only. No structure for widgets, no separation of UI vs logic.


Documentation quality (clear function purpose)

UX clarity
