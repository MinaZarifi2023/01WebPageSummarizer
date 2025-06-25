# WebPage Summarizer

## Summary

This project takes a URL and returns a Markdown summary using either OpenAI API (`gpt-4o-mini`) or a local model (`llama3.2`) through Ollama.

## Components

- **Environment Check**: Verifies that the appropriate virtual environment (e.g. `llms`, `venv`) is active.
- **API Key Handling**:
  - Loads `.env` file from the project root.
  - Checks that `OPENAI_API_KEY` exists and is correctly formatted.
- **Website Class**: Downloads and parses the webpage using `requests` and `BeautifulSoup`. Strips out unnecessary tags (`script`, `style`, `img`, `input`) and extracts the main text.
- **Model Interfaces**:
  - **OpenAI**: Uses the `openai` Python SDK and `gpt-4o-mini`.
  - **Ollama**: Sends a POST request to the local server at `http://localhost:11434/api/chat`.
- **Prompt Handling**: Combines system and user prompts for summarization.
- **Display**: Uses `IPython.display.Markdown` to show the output in a notebook.

## Features

- Accepts any public URL (e.g. articles, blog posts)
- Supports both cloud-based and local language models
- Extracts clean content from HTML
- Returns summary in Markdown format
- Displays results inside Jupyter Notebooks

## Requirements

- Python 3.8 or higher
- Jupyter Lab or Notebook
- Active virtual environment (`llms`, `venv`, etc.)
- `.env` file containing:

```env
OPENAI_API_KEY=sk-proj-...
```

## Setup

1. Clone the repository:
```bash
git clone https://github.com/yourusername/webpage-summarizer.git
cd webpage-summarizer
```

2. Create and activate a virtual environment:
```bash
python -m venv venv
source venv/bin/activate
conda activate llms
```

3. Install dependencies:
```bash
pip install -r requirements.txt
```

4. Add your OpenAI API key:  
Create a `.env` file in the parent directory of your notebook:
```env
conda env create -f environment.yml
OPENAI_API_KEY=sk-proj-xxxxxxxxxxxxxxxxxxxxxxxxxxxx
```

5. Start Ollama (for local models):
```bash
ollama run llama3.2
```

6. Run Jupyter Lab:
```bash
jupyter lab
```

## Example

```python
display_summary("https://en.wikipedia.org/wiki/OpenAI")
```

This will generate a Markdown summary of the provided URL.

## Switching Between OpenAI and Ollama

### Using OpenAI

```python
response = openai.chat.completions.create(
    model="gpt-4o",
    messages=[
        {"role": "system", "content": SYSTEM_PROMPT},
        {"role": "user", "content": USER_PROMPT}
    ]
)
```

### Using Ollama

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


