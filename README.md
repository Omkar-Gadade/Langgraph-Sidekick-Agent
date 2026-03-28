# 🧠 LangGraph Sidekick Agent

A multi-step autonomous AI assistant built using LangGraph, Gradio, and tool-augmented LLMs.  
This Sidekick acts like a personal co-worker that iteratively works on tasks, evaluates its own output, and improves until the success criteria are met.

---

## 🚀 Features

- 🔁 Iterative reasoning loop (Worker → Evaluator → Retry)
- 🧰 Tool-augmented LLM agent
  - Web browsing (Playwright)
  - Python execution
  - File management
  - Wikipedia & web search
- 🧠 Self-evaluation mechanism
- 💬 Conversational UI using Gradio
- 💾 Memory persistence via LangGraph checkpoints
- 🔄 Multi-step execution ("supersteps")

---

## 🏗️ Architecture Overview
- User Input
↓
- Worker (LLM + Tools)
↓
- [Tool Calls if needed]
↓
- Evaluator (LLM Judge)
↓
- ├── ✅ Success → End
- ├── ❓ Needs Input → End
- └── 🔁 Retry → Worker


---

## 📂 Project Structure
- ├── app.py # Gradio UI
- ├── sidekick.py # Core LangGraph agent logic
- ├── sidekick_tools.py # Tool integrations
- └── sandbox/ # File operations directory


---

## ⚙️ Installation

### 1. Clone the repository

```bash
git clone <your-repo-url>
cd <repo-name>
```
### 2. UV Sync 

```bash
uv sync
```


