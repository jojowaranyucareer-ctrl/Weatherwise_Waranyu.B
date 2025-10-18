# 🪞 Project Reflection

---

## 🤖 AI Tools Used

I used **ChatGPT** as my sole AI tool during development. I treated it as a **design partner** (clarifying requirements, drafting pseudocode, stress-testing edge cases, and iterating on structure).  

ChatGPT’s biggest value was helping me **think aloud**: I could restate goals, propose a plan, and get immediate feedback before touching code.  

Outside of ChatGPT, the project also relied on several key tools and libraries:
- **OpenWeather REST API** – to retrieve real-time forecast data  
- **ipywidgets** – for building an interactive notebook interface  
- **matplotlib** – for creating temperature and rainfall visualisations
- **hands-on-ai** - for using AI to answer the weather question  

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

The **Structure of Coding** is what I am most proud of.  
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

If I had more time to continue improving this project, I would focus on enhancing the **user interface and visual experience**. I really enjoyed designing the charts and would like to make them more interactive and colourful. For example, when the temperature is very high, the graph could automatically display **red tones** to highlight heat warnings, while cooler temperatures could appear in **blue**. This kind of visual feedback would make the weather data easier to understand and more engaging for users.

In the future, I would also like to add **interactive features** such as tooltips that show detailed values when hovering over data points, or buttons that allow users to switch between temperature and precipitation views without reloading the graph. Learning how to implement these dynamic elements will take more time, but I’m excited to explore them to make the WeatherWise interface more enjoyable and user-friendly.

---

## 💭 Final Thoughts

This project reinforced a **productive workflow for collaborating with AI tools**:  
> Restate the goal → Ask for structure → Challenge edge cases → Build the smallest viable version → Test with real data → Refine iteratively.  

ChatGPT served as a **thinking partner**, not just a code generator — helping me structure ideas, foresee design challenges, and validate assumptions before coding.  

The result is a **compact, maintainable weather application** that not only presents weather data but also **explains it clearly and conversationally**.  
It demonstrates how AI can enhance software design thinking, accelerate learning, and improve development quality through guided iteration.
