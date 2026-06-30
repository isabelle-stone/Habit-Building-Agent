# Habit-Building-Agent

A conversational AI agent that helps users build sustainable habits through personalized ramp-up schedules, contextual nudging, and reflective self-correction.

**Built by:** Suvin Jeon & Isabelle Stone

## Architecture
 
The agent runs a ReAct-style reasoning loop wrapped in a Reflection (Critic/Reviser) pattern:
 
1. **User Input** (e.g. morning/evening check-in) → checked for enough info to proceed; if not, the agent asks follow-up questions.
2. **ReAct Loop** (Reason → Act → Observe) — the agent reasons about what it needs, then calls tools:
   - Habit Log DB (Supabase/Postgres)
   - Metric computation
   - RAG knowledge base (pgvector) for coaching strategies
   - Ramp-up schedule generator
   The loop repeats until it has enough context.
3. **Strategy Selection** (LLM call) → picks a response strategy based on user state (on track, struggling, etc.)
4. **Draft Response** (LLM call)
5. **Reflection** (separate LLM call, Critic) → evaluates the draft against criteria; if it fails, the draft is revised and re-checked until it passes.
6. **Final Output** → returned to the user.
## Tech Stack
 
- **Orchestration:** LangGraph / LangChain
- **LLM:** GPT-4o-mini via OpenRouter
- **Database:** Supabase (PostgreSQL)
- **Vector store / RAG:** pgvector
- **Dev environment:** Google Colab (Jupyter notebook)
