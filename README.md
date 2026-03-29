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
## 🔑 Environment Variables
```env
Create a .env file in the root directory:

OPENAI_API_KEY=your_openai_key
SERPER_API_KEY=your_serper_key

# Optional (for push notifications)
PUSHOVER_TOKEN=your_token
PUSHOVER_USER=your_user
```
## ▶️ Running the App
```powershell
uv run app.py
```
This will launch a Gradio interface in your browser.\

## 💡 How It Works
1. User Input
You provide: Task + Success criteria

2. Worker Agent
Uses LLM + tools
Can:
Search web
Execute Python
Browse websites
Create files

3. Evaluator Agent
Checks:
Whether success criteria are met
If more input is needed

4. Loop
If not successful → retry with feedback
Stops when:
Task is complete
More user input is required

## 🔁 Example

- Input:
```
Task: Find top 3 AI research papers in 2024  
Criteria: Include links and short summaries
```
- Process:

Worker searches and gathers results
Evaluator checks quality
If incomplete → Worker retries
Final response returned

## 🧠 Core Concepts

- State Management
```
class State(TypedDict):
    messages: List[Any]
    success_criteria: str
    feedback_on_work: Optional[str]
    success_criteria_met: bool
    user_input_needed: bool
```

- Worker
-- Executes tasks using tools
-- Iteratively improves based on evaluator feedback

- Evaluator
-- Provides structured feedback
-- Decides:
--- Success
--- Retry
--- Need user input
  
- Memory
-- Uses LangGraph MemorySaver
-- Maintains state across steps using thread_id

## 🧰 Tools Included
- Browser automation (Playwright)
- Google search (Serper API)
- Python REPL execution
- File management (sandbox directory)
- Wikipedia search
- Push notifications (optional)
