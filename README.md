# Decision Negotiation Agent – Multi-Agent Decision Intelligence System

This project is our capstone for Google’s 5-Day AI Agents Intensive.  
It is a **multi-agent decision intelligence system** that helps a user make tough choices
(e.g., “accept a promotion vs keep a flexible role”) by letting multiple specialized
agents debate, then letting an LLM supervisor make a final call.

## Core Idea

Instead of asking a single LLM for advice, this system simulates a *mini internal committee*:

- 🧠 **LogicAgent** – optimizes time, money, and short-term productivity.
- ❤️ **EmotionAgent** – cares about stress, relief, and emotional well-being.
- 🕰 **LongTermAgent** – looks at future regret and long-term gain.
- 🎯 **ValuesAgent** – checks alignment with core life values (career, health, relationships, finances, peace).

Each agent scores the options, explains its reasoning, and casts a vote.
A **Supervisor LLM** then reads all proposals and returns a structured JSON
decision: final choice, reasoning, and a vote breakdown.

---

## System Architecture

1. **Decision Input Layer**
   - User provides:
     - `question` – the dilemma (e.g., *“Should I accept a promotion that doubles my hours?”*)
     - `options` – list of possible actions
     - optional `context` – stress level, financial pressure, priorities, etc.

2. **Specialized Agents**
   - Each agent implements a `decide(decision)` interface.
   - Returns:
     ```json
     {
       "agent_name": "...",
       "preferred_option": "...",
       "scores": { "Option A": {...}, "Option B": {...} },
       "explanation": "Natural language reasoning..."
     }
     ```

3. **LLM Supervisor (Gemini via ADK)**
   - Ingests all agent proposals.
   - Outputs **strict JSON**:
     ```json
     {
       "final_decision": "...",
       "reasoning": "...",
       "agent_votes": {
         "EmotionAgent": "...",
         "LogicAgent": "...",
         "LongTermAgent": "...",
         "ValuesAgent": "..."
       }
     }
     ```

4. **Evaluation & Observability**
   - Inspired by Day 4 of the AI Agents Intensive, the notebook includes:
     - Ambiguous / complex / edge-case test scenarios
     - Debug prints of agent proposals
     - Supervisor raw JSON
     - Structured evaluation objects for analysis

---

## Interpretability & Analytics Features

To make the agent system **explainable** and **auditable**, I added:

### ⚔️ Agent Conflict Analyzer
- Computes agreement/disagreement between agents.
- Outputs pairwise relationships and an overall **conflict score (0–1)**:
  - `0.0` → perfect agreement
  - higher values → more internal conflict

### 📈 Decision Stability Score (0–100)
- Aggregates:
  - agent consensus,
  - score variance across options,
  - supervisor–agent agreement.
- Produces a single **stability score**:
  - `> 85` → very stable decision
  - `70–85` → moderately stable
  - `< 50` → unstable / needs review

### ⚔️ Option Battle Card (Side-by-Side Comparison)
- Builds a table comparing each option across all agents:
  - emotional_relief / stress_risk
  - productivity / time_cost / money_impact
  - future_regret / future_gain
  - values alignment (career, relationships, health, finances, peace)
- Shows:
  - Agent-by-agent scores per option
  - Vote counts
  - Final winner option

This looks and feels like a **consulting-grade analysis dashboard** for decisions.

### 🎴 Agent Personality Cards
- Each agent has a defined **persona**:
  - tagline, strengths, weaknesses, and personality description.
- Cards make the system more interpretable and human-readable
  (e.g., *“LongTermAgent – forward-thinking, strategic, cautious about regret”*).

---

## Example Scenario

**Question:**  
> “Should I accept the promotion that doubles my work hours but increases salary,
> or stay in my current role with less pay but more flexibility?”

- All four agents independently analyze the trade-offs.
- The supervisor reviews their proposals and returns:
  - `final_decision`: *“Accept the promotion with doubled hours and higher salary”* (for this test context)
  - A natural language explanation merging emotional, logical, long-term, and values-based reasoning.
  - A full vote breakdown and stability score.

This demonstrates the system’s ability to:
- model trade-offs,
- surface internal disagreements,
- and justify its recommendation in an auditable way.

---

## Technical Highlights

- Built on **Gemini + ADK** patterns from Google’s 5-Day AI Agents Intensive.
- Uses:
  - custom scoring logic for each agent,
  - a supervisor LLM for final arbitration,
  - structured JSON outputs for downstream evaluation,
  - multi-scenario test harness (ambiguous / invalid / complex decisions),
  - interpretable analytics (conflict, stability, battle cards, personas).

This project shows my ability to:
- design **multi-agent LLM systems**,
- build **evaluation & observability tooling**,
- and present **complex AI behavior in a way that non-technical stakeholders can understand**.
