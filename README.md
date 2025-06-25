# 🚀 WebPage Summarizer

A simple but powerful tool that summarizes the content of any public webpage into clean, readable Markdown using both OpenAI's hosted LLMs and local models via Ollama.

--- 
✅ Summary of the Code
Project Goal: Build a web summarization tool that takes a URL and returns a clean, readable Markdown summary using either OpenAI API (gpt-4o-mini) or local LLM via Ollama (llama3.2).

🔧 Key Components
Environment Check: Confirms that the right virtual environment (like llms or venv) is activated.

API Key Handling:

Loads .env from the project root.

Verifies the presence and format of OPENAI_API_KEY.

Website Class: Fetches and cleans up the page using requests + BeautifulSoup. Removes irrelevant tags (script, style, img, input) and extracts page text.

Model Interfaces:

OpenAI API: Uses openai Python SDK to generate summaries with gpt-4o-mini.

Ollama: Sends a POST request to local LLM server via http://localhost:11434/api/chat.

Prompt Handling:

System and user prompts are combined for summarization.

Display:

Summary is rendered directly in the notebook using IPython.display.Markdown.

---

## 🎯 Features

- 🌐 Input: Any URL (e.g. Wikipedia article, blog post)
- 🧠 LLMs:
  - OpenAI's `gpt-4o-mini` via API
  - Local `llama3.2` via [Ollama](https://ollama.com)
- 🧼 Clean HTML parsing using BeautifulSoup (removes noise like images/scripts)
- 🪄 Output: Concise Markdown summary
- ✅ Notebook-integrated display via `IPython.display.Markdown`

---

## 📦 Requirements

- Python 3.8+
- Jupyter Lab / Notebook
- Virtual environment activated (`llms` or `venv`)
- [.env](https://github.com/motdotla/dotenv) file containing:
  ```env
  OPENAI_API_KEY=sk-proj-...

```

## 🛠 Setup Instructions

### 📥 Clone Repo
```bash
git clone https://github.com/yourusername/webpage-summarizer.git
cd webpage-summarizer
```

### 🐍 Create and Activate Virtual Environment
```bash
conda create -n llms python=3.10
conda activate llms
```

### 📦 Install Dependencies
```bash
pip install -r requirements.txt
```

### 🔑 Set OpenAI API Key
Create a `.env` file in the **parent folder** of your notebook and add the following line:
```env
OPENAI_API_KEY=sk-proj-xxxxxxxxxxxxxxxxxxxxxxxxxxxx
```

### ⚙️ Start Ollama (for local model)
```bash
ollama run llama3
```

### 🚀 Run Jupyter Lab
```bash
jupyter lab
```

---

## 🧪 Example
```python
display_summary("https://en.wikipedia.org/wiki/OpenAI")
```
You’ll get a structured, clean Markdown summary of the given webpage.

---

## 🤖 Switching Between OpenAI and Ollama

### Using OpenAI:
```python
response = openai.chat.completions.create(
    model="gpt-4o",
    messages=[
        {"role": "system", "content": SYSTEM_PROMPT},
        {"role": "user", "content": USER_PROMPT}
    ]
)
```

### Using Local Ollama Model:
```python
response = requests.post(
    "http://localhost:11434/api/chat",
    json={
        "model": "llama3",
        "messages": [
            {"role": "system", "content": SYSTEM_PROMPT},
            {"role": "user", "content": USER_PROMPT}
        ]
    }
)
```


