# 🔬 ResearchMind — Multi-Agent AI Research System

> **Four specialized AI agents collaborate — searching, scraping, writing, and critiquing — to deliver a polished research report on any topic.**

---

## ✨ Overview

**ResearchMind** is a multi-agent AI research pipeline built with **LangChain**, **LangGraph**, and **Google Gemini**. It automates the full research workflow: from searching the web and scraping deep content, to writing a structured report and critically reviewing it — all in one seamless pipeline.

The system provides two interfaces:
- 🖥️ **Streamlit Web UI** (`app.py`) — A beautiful, dark-themed interactive dashboard
- 💻 **CLI Pipeline** (`pipeline.py`) — A terminal-based pipeline for quick programmatic use

---

## 🏗️ Architecture

```
User Input (Topic)
       │
       ▼
┌─────────────────┐
│  Search Agent   │  ← Uses Tavily to search the web (5 results)
└────────┬────────┘
         │ Search Results
         ▼
┌─────────────────┐
│  Reader Agent   │  ← Picks the best URL & scrapes deep content
└────────┬────────┘
         │ Scraped Content
         ▼
┌─────────────────┐
│  Writer Chain   │  ← Drafts a structured research report (LCEL)
└────────┬────────┘
         │ Draft Report
         ▼
┌─────────────────┐
│  Critic Chain   │  ← Reviews, scores, and gives feedback (LCEL)
└─────────────────┘
         │
         ▼
   Final Report + Score
```

---

## 🤖 Agents & Chains

| Component | Type | Role |
|-----------|------|------|
| **Search Agent** | LangChain Agent | Queries Tavily for the latest web info on a topic |
| **Reader Agent** | LangChain Agent | Picks the most relevant URL and scrapes its content |
| **Writer Chain** | LCEL Chain | Synthesizes research into a structured report |
| **Critic Chain** | LCEL Chain | Reviews the report and provides a score + feedback |

### Writer Report Structure
- Introduction  
- Key Findings (minimum 3 points)  
- Conclusion  
- Sources

### Critic Output Format
```
Score: X/10

Strengths:
- ...

Areas to Improve:
- ...

One line verdict:
...
```

---

## 🛠️ Tools

| Tool | Description |
|------|-------------|
| `web_search(query)` | Searches via Tavily API; returns titles, URLs, and snippets (top 5 results) |
| `scrape_url(url)` | Scrapes and cleans text content from any URL using `requests` + `BeautifulSoup` (up to 3000 chars) |

---

## 📁 Project Structure

```
Multiagen_sysytem/
│
├── app.py            # Streamlit web UI (main entry point for UI)
├── agents.py         # Agent and chain definitions (Search, Reader, Writer, Critic)
├── pipeline.py       # CLI pipeline runner
├── tools.py          # Custom LangChain tools (web_search, scrape_url)
├── requirements.txt  # Python dependencies
└── .env              # API keys (not committed to version control)
```

---

## ⚙️ Setup & Installation

### 1. Clone the repository

```bash
git clone <your-repo-url>
cd Multiagen_sysytem
```

### 2. Create a virtual environment

```bash
python -m venv .venv

# Windows
.venv\Scripts\activate

# macOS/Linux
source .venv/bin/activate
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

### 4. Configure API keys

Create a `.env` file in the project root:

```env
TAVILY_API_KEY=your_tavily_api_key_here
GEMINI_API_KEY=your_gemini_api_key_here
```

> **Get your keys:**
> - Tavily API: [https://app.tavily.com](https://app.tavily.com)
> - Gemini API: [https://aistudio.google.com/app/apikey](https://aistudio.google.com/app/apikey)

---

## 🚀 Running the Application

### Option 1: Streamlit Web UI (Recommended)

```bash
streamlit run app.py
```

Open your browser at `http://localhost:8501`. Enter a research topic, click **"⚡ Run Research Pipeline"**, and watch the four agents work in real time.

**Features of the Web UI:**
- Live pipeline step tracking (Waiting → Running → Done)
- Expandable raw outputs for Search & Reader agents
- Rendered Markdown final report
- **Download** the report as a `.md` file
- Critic feedback panel with score

### Option 2: CLI Pipeline

```bash
python pipeline.py
```

You'll be prompted to enter a research topic. The pipeline prints step-by-step output to the terminal.

---

## 📦 Dependencies

| Package | Purpose |
|---------|---------|
| `langchain` | Core LangChain framework |
| `langchain-core` | LCEL (LangChain Expression Language) |
| `langchain-google-genai` | Google Gemini LLM integration |
| `langgraph` | Agent orchestration & tool-calling |
| `langchain-tavily` / `tavily-python` | Tavily web search tool |
| `beautifulsoup4` + `requests` | Web scraping |
| `streamlit` | Web UI framework |
| `python-dotenv` | Environment variable management |
| `pydantic` | Data validation |
| `rich` | Enhanced terminal output |

---

## 💡 Example Topics to Try

- `LLM agents 2025`
- `CRISPR gene editing`
- `Fusion energy progress`
- `Quantum computing breakthroughs`
- `Climate change solutions`

---

## 🔒 Security Note

> ⚠️ **Never commit your `.env` file to version control.** Add it to `.gitignore` to keep your API keys safe.

```gitignore
.env
.venv/
__pycache__/
```

---

## 🧠 Powered By

- [LangChain](https://langchain.com/) — Agent & chain framework
- [Google Gemini](https://deepmind.google/technologies/gemini/) — LLM backbone (`gemini-2.0-flash`)
- [Tavily](https://tavily.com/) — AI-optimized web search
- [Streamlit](https://streamlit.io/) — Web UI

---

*ResearchMind · Multi-Agent AI System · Built with LangChain & Streamlit*
