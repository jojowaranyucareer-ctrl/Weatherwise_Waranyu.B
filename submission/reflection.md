# 🪞 Project Reflection

---

## 🤖 AI Tools Used

I used **ChatGPT** as my sole AI tool during development. I treated it as a **design partner** — clarifying requirements, drafting pseudocode, stress-testing edge cases, and iterating on structure.  

ChatGPT’s biggest value was helping me **think aloud**: I could restate goals, propose a plan, and get immediate feedback before touching code.  

Outside of ChatGPT, the project also relied on several key tools and libraries:
- **OpenWeather REST API** – to retrieve real-time forecast data  
- **ipywidgets** – for building an interactive notebook interface  
- **matplotlib** – for creating temperature and rainfall visualisations  

---

## 💬 Prompting Techniques

I applied several **intentional prompting strategies** throughout development:

1. **Restating the problem** in my own words to confirm inputs, outputs, and constraints  
   > Example: “5-day forecast, 3-hour intervals, metric units.”  
2. **Requesting pseudocode** before implementation to keep each function single-purpose and avoid rewrites.  
3. **Testing edge cases** deliberately — such as invalid city names, missing API keys, empty lists, and interpreting “tomorrow” from 3-hour intervals.  
4. **Refactoring modularly**, ensuring retrieval, processing, visualisation, and conversation logic were decoupled.  
5. **Asking for line-by-line explanations** of complex code segments (for example, parsing `dt_txt` timestamps) to deepen understanding.  
6. **Iterating deliberately**: propose → implement minimal version → test with real data → refine based on outcomes.

These techniques made my collaboration with ChatGPT structured and goal-oriented, improving both accuracy and learning.

---

## ✅ What Worked Well

The **architecture** is what I am most proud of.  
Separation of concerns kept the system understandable and easy to test.

- `openWeather_getWeather()` focuses on **data retrieval** and **error handling**.  
- **Processing functions** transform raw 3-hour readings into logical daily groupings.  
- **Visualisation functions** are pure consumers of processed data — simple to test independently.  
- The **AI conversation layer** turns structured weather data into clear, human-readable responses.

This modular structure made **debugging straightforward**.  
I verified JSON shapes and keys, confirmed grouping logic, tested small (3-day) charts before 5-day ones, and ran full end-to-end tests with realistic user questions.  

Small quality touches enhanced usability, such as:
- **Caching** the last location and dataset for responsiveness.  
- A **temperature-advice helper** that turns numeric data into friendly guidance (“It’s warm enough for outdoor exercise”).  

---

## 🔄 What I Would Do Differently

If I had more time, I would focus on **improving natural-language parsing**.  
The current approach uses simple capitalization and keyword heuristics — acceptable for a demo but brittle with:
- Multi-word cities (“New York”)  
- Ambiguous phrasing  
- Relative date expressions (“the day after tomorrow”)

A lightweight **NLP layer** or compact **rules engine** could improve reliability.  

I would also make several structural and performance enhancements:
- Add **response validation and guardrails** in the AI layer:  
  - Unit normalization (°C/°F)  
  - Consistent rounding  
  - Clear “insufficient data” messages  
- Implement **short-TTL caching** and **asynchronous I/O** for faster API calls.  
- Introduce **schema validation** (e.g., with *Pydantic*) to detect malformed data early.  
- Expand **unit tests** using mocked payloads for:  
  - Error scenarios  
  - Rate limits  
  - Unexpected API responses  
- Move all configuration to a **`.env` file** and improve setup documentation with a **troubleshooting section** for common network or key errors.

These improvements would make WeatherWise more robust, scalable, and maintainable for real-world use.

---

## 💭 Final Thoughts

This project reinforced a **productive workflow for collaborating with AI tools**:  
> Restate the goal → Ask for structure → Challenge edge cases → Build the smallest viable version → Test with real data → Refine iteratively.  

ChatGPT served as a **thinking partner**, not just a code generator — helping me structure ideas, foresee design challenges, and validate assumptions before coding.  

The result is a **compact, maintainable weather application** that not only presents weather data but also **explains it clearly and conversationally**.  
It demonstrates how AI can enhance software design thinking, accelerate learning, and improve development quality through guided iteration.
