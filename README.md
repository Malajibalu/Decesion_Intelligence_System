🧠 Decision Negotiation Agent
Multi-Agent Decision Intelligence System (Google AI Agents Intensive Capstone)
The Decision Negotiation Agent is a multi-agent decision support system designed to help users navigate complex dilemmas. Built as part of Google’s 5-Day AI Agents Intensive, this project models a miniature “internal committee” of four expert agents—Logic, Emotion, Long-Term, and Values—to simulate human-style reasoning and deliver transparent, auditable decisions.
Instead of relying on a single LLM, the system forces multiple specialized agents to debate, score trade-offs, provide written justifications, and finally vote on the best option. A Gemini-powered Supervisor (via ADK) consolidates all insights into one structured, explainable decision.
🌟 Key Capabilities
✔ Multi-Agent Debate Engine
Each agent evaluates the user’s dilemma using a unique lens:
🧠 LogicAgent — time, money, productivity, short-term optimization
❤️ EmotionAgent — stress, relief, emotional well-being
🕰 LongTermAgent — regret minimization, future upside
🎯 ValuesAgent — alignment with core life values (career, peace, relationships, finances, health)
✔ Supervisor LLM for Final Arbitration
The Supervisor LLM reviews all agent proposals and outputs strict JSON:
{
 "final_decision": "...",
 "reasoning": "...",
 "agent_votes": { ... }
}
✔ Interpretability & Analytics Layer
To make decisions transparent and trustworthy, the system includes:
Agent Conflict Analyzer – detects disagreements and computes a conflict score
Decision Stability Score – evaluates confidence in the final decision (0–100)
Option Battle Cards – consulting-style side-by-side comparison tables
Agent Personality Cards – strengths, weaknesses, and persona descriptions
✔ Test Harness for Edge Cases
Includes predefined ambiguous, complex, and high-conflict decision scenarios to ensure robustness and consistency.
🧩 System Architecture
1. Decision Input Layer
User provides:
the dilemma (question)
list of possible choices (options)
optional context such as stress level, financial pressure, personal priorities
2. Specialized Agent Modules
Each agent implements a decide() method that returns:
{
 "agent_name": "ValuesAgent",
 "preferred_option": "Option A",
 "scores": { "Option A": {...}, "Option B": {...} },
 "explanation": "Detailed reasoning here..."
}
3. Supervisor Arbitration (Gemini + ADK)
The Supervisor fuses all agent reports into:
one final choice
a synthesized explanation
a vote breakdown
optional override notes if agent disagreement is high
4. Evaluation Layer
This layer transforms raw agent outputs into:
conflict matrices
stability scoring
battle cards
formatted insights for dashboards
📝 Example Scenario
Question:
“Should I accept a promotion that doubles my hours but increases salary, or stay in my current flexible role?”
Process:
LogicAgent prioritizes earning potential
EmotionAgent warns about stress
LongTermAgent evaluates future regret
ValuesAgent checks alignment with long-term personal goals
Supervisor Output:
final decision
merged reasoning
vote counts
stability score
This flow demonstrates the system's ability to justify decisions in an interpretable, auditable way.
🧠 Why This Matters
Decision-making systems must be:
transparent (no black-box answers)
structured (consistent JSON)
interpretable (conflict and stability metrics)
human-aligned (values, emotions, long-term impact)
This project showcases a next-generation pattern in agentic AI:
LLMs that collaborate, argue, and negotiate — not just predict.
🛠 Tech Stack
Google Gemini
ADK (Agents Development Kit)
Python (orchestration, scoring, evaluation)
JSON for structured communication
📂 Project Structure
(Can be customized based on your repo)
/decision-negotiation-agent
│
├── agents/
│   ├── logic_agent.py
│   ├── emotion_agent.py
│   ├── longterm_agent.py
│   └── values_agent.py
│
├── supervisor/
│   └── supervisor_agent.py
│
├── evaluation/
│   ├── conflict_analyzer.py
│   ├── stability_score.py
│   └── battle_cards.py
│
├── tests/
│   ├── scenario_simple.json
│   ├── scenario_conflict.json
│   └── scenario_complex.json
│
└── decision_runner.ipynb
🚀 How to Run
Install dependencies
Configure ADK with Gemini API access
Run the notebook or decision runner script
Pass your question + options
View:
agent reasoning
supervisor final output
conflict + stability scores
📌 Summary
This project demonstrates:
Strong multi-agent architecture design
Real-world decision modeling
Interpretability & governance tooling
LLM-Ops style structured evaluation
Hands-on proficiency with Google’s ADK and Gemini models
It’s an ideal showcase of agent engineering, reasoning frameworks, and AI product design.
