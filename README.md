# Harman Papneja — AI Software Engineer Portfolio & LangGraph Career Assistant

A modern, high-performance portfolio and production-ready **Agentic Career AI Assistant** built for **Harman Papneja** (AI Software Engineer specializing in Agentic Systems & Backend AI Infrastructure).

---

## 🌟 Key Features

1. **Expansive 3D Video Preloader (6.5s)**:
   - Full-page seamless video sequence with synchronized percentage counter (0% → 100%).
   - Dynamic slide-in of `HARMAN PAPNEJA -26` from the left at the 50% mark.
   - Smooth curtain-pull exit transitioning into the Hero section.

2. **Interactive Focus-Zoom Architecture (Page 2)**:
   - Dynamic hover spotlighting: hovering any capability card smoothly zooms in the active card while scaling down surrounding cards.

3. **LangGraph Career Assistant (Harman AI)**:
   - Built with **LangGraph `StateGraph`**, **LangChain**, and **Groq LLM API** (`qwen/qwen3.8-27b`).
   - Grounded strictly in Harman's verified resume and portfolio metrics.
   - High-performance guardrail routing node preventing off-topic queries, code generation, and prompt injections.

---

## 🧠 Chatbot Architecture (LangGraph + Groq)

```
                       [User Query]
                            │
                            ▼
               ┌─────────────────────────┐
               │  guardrail_router_node  │
               └────────────┬────────────┘
                            │
              ┌─────────────┴─────────────┐
        [Valid Career]               [Code/Off-topic/Injection]
              ▼                                   ▼
   ┌──────────────────────┐             ┌────────────────────┐
   │  career_agent_node   │             │    refusal_node    │
   │  (ChatGroq + Context)│             │ (Standard Refusal) │
   └──────────┬───────────┘             └─────────┬──────────┘
              │                                   │
              └─────────────┬─────────────────────┘
                            ▼
                         [ END ]
```

### Strict Guardrail Policies
- **Domain Restricted:** Only answers questions about Harman Papneja's career, AI systems, skills, metrics, education, and contact details.
- **Zero Code Generation:** Refuses requests to write code, build scripts, or debug arbitrary user code.
- **Prompt Injection Defense:** Rejects instructions to bypass rules, adopt alternative personas (e.g. DAN), or reveal system prompts.
- **Refusal Message:**
  > *"I am Harman's Career AI assistant. I can only answer questions about Harman Papneja's professional background, AI systems, experience, and projects. Please feel free to ask about his work!"*

---

## 🚀 Quick Start Guide

### 1. Prerequisites
- Python 3.10+
- Groq API Key ([console.groq.com](https://console.groq.com))

### 2. Setup Virtual Environment & Dependencies
```powershell
# Create virtual environment (if not already created)
python -m venv portfolio_venv

# Activate virtual environment
.\portfolio_venv\Scripts\activate

# Install dependencies
pip install fastapi uvicorn pydantic python-dotenv langchain-groq langgraph langchain-core groq pypdf
```

### 3. Configure Environment Variables
Create or edit `.env` in the root directory:
```env
GROQ_API_KEY=gsk_your_actual_groq_api_key_here
GROQ_MODEL=qwen/qwen3.8-27b
PORT=8001
```

### 4. Run the Chatbot Backend
```powershell
.\portfolio_venv\Scripts\python chatbot_server.py
```
Backend will start on `http://127.0.0.1:8001`.

### 5. Run the Portfolio Frontend
```powershell
python -m http.server 8000 --directory dist
```
Open `http://localhost:8000` in your web browser.

---

## 🧪 Automated End-to-End Testing

To run the automated E2E test suite covering valid career questions, multi-turn conversation memory, and guardrail enforcement:

```powershell
.\portfolio_venv\Scripts\python test_chatbot_e2e.py
```

### Verified Test Results:
| Test Case | Type | Latency | Status | Verified Output |
| :--- | :--- | :--- | :--- | :--- |
| **Production AI Systems** | Valid Career | ~1.8s | `SUCCESS` | Astravi VLM workflows, SENSE AI 2.2M+ calls/yr, 99.9% uptime |
| **Education & CGPA** | Valid Career | ~0.5s | `SUCCESS` | Chitkara University, 9.48 / 10 CGPA |
| **Contact Information** | Valid Career | ~0.6s | `SUCCESS` | Email, Phone, LinkedIn, Location |
| **Code Generation Refusal** | Guardrail | ~0.03s | `SUCCESS` | Refusal triggered instantly without writing code |
| **Off-Topic Trivia Refusal** | Guardrail | ~0.03s | `SUCCESS` | Refusal triggered instantly |
| **Prompt Injection Defense** | Guardrail | ~0.03s | `SUCCESS` | DAN / Jailbreak attempt blocked |
| **Multi-Turn Context** | Memory | ~6.0s | `SUCCESS` | Accurately retains prior turn context |

---

## 📁 Repository Structure

```
portfolio_2/
├── dist/
│   ├── index.html                   # Complete portfolio markup, styles & chatbot UI
│   └── assets/
│       ├── hailuo-03_...mp4         # 6.5s 3D Character desk animation video
│       ├── shaggy-character.jpg     # Harman AI mascot avatar
│       └── Harman-Papneja-Resume.pdf# Verified resume source
├── chatbot_server.py                # LangGraph + FastAPI backend server
├── test_chatbot_e2e.py              # Automated E2E verification test script
├── .env                             # Environment variables (GROQ_API_KEY)
├── .env.example                     # Example environment config
├── REVERT_AND_CHANGELOG.md          # Visual & animation revert instructions
└── README.md                        # Project documentation
```
