## 📖 Project Overview
This repository contains a browser-based article summarization tool built using the Gemini 2.0 Flash API. Developed for Lab 5 of COMP308, the application allows users to input long-form text and receive a concise AI-generated summary. It focuses on summarizing recent articles related to the environmental impact of generative AI.


## 🎯 Project Objectives
Build a working summarizer using Gemini API.

Analyze articles discussing the environmental cost of generative AI.

Provide references and a one-page summary using a large language model (LLM).

## 🛠️ How to Run

### 1. Clone the Repository

```bash
git clone https://github.com/MattBarhou/Lab5_COMP308.git
cd Lab5_COMP308
```


### 2. Open `index.html`

You can double-click `index.html` to open it in your browser, or run:

```bash
open index.html
```

### 3. Replace the API Key

Inside the `<script>` tag in `index.html`, replace:

```js
const API_KEY = "YOUR_API_KEY_HERE";
```

with your own [Gemini API key](https://ai.google.dev/).

---

## 🖼️ How It Works

1. Paste your article into the textarea.
2. Click **"Summarize"**.
3. View a concise AI-generated summary in the output box.

---

## 📄 Code Overview

```html
<textarea
  id="articleText"
  rows="12"
  cols="80"
  placeholder="Paste your article text here..."
></textarea>
<button onclick="summarizeArticle()">Summarize</button>

<script>
  const API_KEY = "YOUR_API_KEY";

  async function summarizeArticle() {
    const input = document.getElementById("articleText").value;
    const output = document.getElementById("summary");

    if (!input.trim()) {
      output.innerText = "Please paste an article to summarize.";
      return;
    }

    output.innerText = "Summarizing...";

    try {
      const res = await fetch(
        `https://generativelanguage.googleapis.com/v1beta/models/gemini-2.0-flash:generateContent?key=${API_KEY}`,
        {
          method: "POST",
          headers: { "Content-Type": "application/json" },
          body: JSON.stringify({
            contents: [
              {
                parts: [
                  { text: `Summarize the following article:\n\n${input}` },
                ],
              },
            ],
          }),
        }
      );

      const data = await res.json();
      const summary =
        data?.candidates?.[0]?.content?.parts?.[0]?.text ||
        "No summary generated.";
      output.innerText = summary;
    } catch (err) {
      output.innerText = `❌ Error: ${err.message}`;
    }
  }
</script>
```

---

## 🧪 Testing & Article Selection

### Article Sources Used

- MIT Technology Review. (2025).  
  [Explained: Generative AI’s Environmental Impact](https://news.mit.edu/2025/explained-generative-ai-environmental-impact-0117)

- Wired. (2025).  
  [The True Cost of Generative AI](https://www.wired.com/story/true-cost-generative-ai-data-centers-energy)

### Testing Strategy

- Input from multiple domains: tech, environment, news
- Edge cases: empty input, long text, API failure
- Verified summary accuracy and formatting

---

## 🧠 One-Page Summary (via Gemini)

**Article:** MIT Tech Review — Environmental Impact of Generative AI  
**Generated Summary:**

> Generative AI models, while powerful, come with significant environmental costs. According to MIT's article, training large language models consumes substantial energy, largely due to the computing power needed for model development and inference. As AI models continue to scale, their carbon footprint increases, prompting the tech industry to search for more sustainable infrastructure. Companies are investing in renewable energy sources and optimizing model efficiency, but there’s still a long road ahead in making AI truly eco-friendly.

---
