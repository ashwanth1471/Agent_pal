# Agent_pal
Agent Pal – Autonomous Coding Agent System


# 🚀 Agent Pal  
### Autonomous Multi-Agent Engineering System using LangGraph

Agent Pal is a structured multi-agent system that transforms a raw project prompt into a fully generated software project.

It orchestrates a **Planner → Architect → Coder** pipeline using LangGraph, enforces structured outputs with Pydantic, and implements tasks through a tool-enabled ReAct coding agent.

The system demonstrates controlled agent orchestration, structured reasoning, task decomposition, and safe autonomous file generation.

---

## ✨ Key Highlights

- 🧠 Multi-agent architecture (Planner, Architect, Coder)
- 📐 Structured engineering plan generation
- 🗂 Automatic task decomposition with dependency ordering
- 🔧 Tool-augmented coding agent using ReAct
- 🛡 Sandboxed file system execution
- 🔒 Safe path validation
- 🔁 Iterative execution loop until completion
- 💻 CLI-based execution
- 📊 Strict schema enforcement using Pydantic
- 🧩 Graph-based orchestration with conditional edges

---

## 🏗 System Architecture

### 🔄 Agent Pipeline

```
User Prompt
     ↓
Planner Agent
     ↓
Architect Agent
     ↓
Coder Agent (iterative execution loop)
     ↓
END
```

---

### 🧭 Execution Graph

Built using `StateGraph(dict)` from LangGraph.

- Entry point: `planner`
- Conditional edges allow the coder to loop until all tasks are completed
- Exit condition: `status == "DONE"`

---

## 🤖 Agent Responsibilities

### 🧠 Planner Agent

Transforms the raw user prompt into a structured engineering **Plan** containing:

- Application name  
- Description  
- Tech stack  
- Feature list  
- File structure (path + purpose)  

Structured output enforced via Pydantic schema.

---

### 🏗 Architect Agent

Converts the Plan into a detailed **TaskPlan**:

- Breaks project into ordered `ImplementationTask` steps  
- Defines:
  - Exact functions and classes  
  - Variable names  
  - Integration points  
  - Imports and dependencies  
- Ensures dependency-first execution order  

---

### 💻 Coder Agent

Implements tasks iteratively:

- Reads existing file content  
- Uses ReAct tool-based reasoning  
- Writes full file implementations  
- Maintains compatibility across modules  
- Continues execution until all steps are complete  

#### 🛠 Tools Available to the Coder

- `read_file`  
- `write_file`  
- `list_files`  
- `get_current_directory`  
- `run_cmd`  

---

## 🧰 Tech Stack

- Python  
- LangGraph  
- LangChain  
- Groq LLM (`openai/gpt-oss-120b`)  
- Pydantic  
- python-dotenv  

---

## 📁 Project Structure

```
agent_pal/
│
├── agent/
│   ├── __init__.py
│   ├── graph.py
│   ├── prompts.py
│   ├── states.py
│   └── tools.py
│
├── .env
├── main.py
└── requirements.txt
```

Generated files are written to:

```
generated_project/
```

All file operations are sandboxed inside this directory.

---

## 📦 Data Models

### 🗺 Plan

Defines project blueprint including:

- Name  
- Description  
- Tech stack  
- Features  
- Files  

---

### 🧩 TaskPlan

Ordered list of implementation steps.

---

### 🔄 CoderState

Tracks:

- TaskPlan  
- Current implementation step  
- Current file content  

All models are implemented using Pydantic with strict schema enforcement.

---

## 🛡 Safety & Controls

- File writes restricted to `generated_project/`  
- Safe path resolution prevents directory traversal  
- Structured outputs validated before execution  
- Controlled recursion limit via CLI  
- Explicit termination condition in execution graph  

---

## ⚙ Installation

### 1. Clone the Repository

```bash
git clone <repo-url>
```

### 2. Install Dependencies

```bash
pip install -r requirements.txt
```

### 3. Configure Environment

Create a `.env` file:

```
GROQ_API_KEY=your_api_key_here
```

---

## ▶ Usage

Run via CLI:

```bash
python main.py
```

Optional recursion limit:

```bash
python main.py --recursion-limit 100
```

You will be prompted:

```
Enter your project prompt:
```

### Example Prompt

```
Build a colourful, intuitive, modern task scheduler app in HTML, CSS and JS
```

The system will:

1. Generate a structured plan  
2. Decompose it into tasks  
3. Iteratively implement files  
4. Write results inside `generated_project/`  
5. Output the final execution state  

---

## 🧠 What This Project Demonstrates

- Advanced LangGraph orchestration  
- Structured multi-agent reasoning  
- Schema-driven LLM output control  
- ReAct-based tool invocation  
- Safe autonomous file generation  
- Iterative execution state tracking  
- Practical agent system design patterns  

---

## 📊 Execution Characteristics

- Debug and verbose logging enabled  
- Structured output validation at every stage  
- Graph-based deterministic flow control  
- Task-level state persistence  
- CLI-based user interaction  
