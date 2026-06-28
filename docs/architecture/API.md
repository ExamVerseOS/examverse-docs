ExamVerseOS API

Version 1.0 — AI-Native, Model-Agnostic Learning API

⸻

Philosophy

ExamVerseOS API is not just a backend.

It is a universal intelligence interface for education systems and AI models.

It is designed to be:

* Model-agnostic (GPT, Claude, Gemini, Llama)
* Tool-native (function calling first)
* Knowledge-grounded (RAG-based)
* Exam-structured (not generic AI chat)
* Platform-independent (web, mobile, agents)

⸻

Core Principle

Every AI response must be grounded in structured knowledge.

No hallucinated facts.

No unverified content.

Only:

* Exam syllabus
* PYQs
* Structured topics
* Verified resources
* Knowledge graph

⸻

Base URL

https://api.examverseos.com/v1

⸻

API Layers

ExamVerseOS API is divided into 4 layers:

1. Core Data Layer     → Exams, Topics, PYQs
2. Search Layer        → Semantic + Hybrid search
3. AI Layer            → Chat, Explain, Quiz, Plan
4. Tools Layer         → Universal LLM functions

⸻

AUTHENTICATION

Bearer Token

Authorization: Bearer <token>

⸻

1. CORE DATA API

⸻

Exams

List Exams

GET /exams

⸻

Get Exam

GET /exams/{exam_id}

⸻

Get Syllabus

GET /exams/{exam_id}/syllabus

⸻

Subjects & Topics

Subjects

GET /exams/{exam_id}/subjects

⸻

Topics

GET /subjects/{subject_id}/topics

⸻

Topic Details

GET /topics/{topic_id}

⸻

2. SEARCH API (Hybrid Intelligence)

⸻

Search Everything

POST /search

Request:

{
  "query": "fundamental rights article 21",
  "exam_id": "upsc",
  "mode": "hybrid"
}

Response:

{
  "topics": [],
  "pyqs": [],
  "concepts": [],
  "confidence": 0.92
}

⸻

3. AI LAYER (CORE INTELLIGENCE SYSTEM)

⸻

AI Chat (Hybrid Mode)

POST /ai/chat

Request:

{
  "message": "Explain fundamental rights in simple terms",
  "exam_id": "upsc",
  "mode": "hybrid",
  "context_depth": "medium"
}

Response:

{
  "response": "Fundamental Rights are basic rights guaranteed by the Constitution...",
  "sources": [
    "topic:fundamental_rights",
    "syllabus:gs2"
  ],
  "followups": [
    "Difference between FR and DPSP",
    "Article 19 explanation"
  ]
}

⸻

Explain Topic (Structured AI)

POST /ai/explain

Request:

{
  "topic_id": "fundamental_rights",
  "level": "exam_ready",
  "format": "structured"
}

⸻

Generate Quiz

POST /ai/quiz

Request:

{
  "topic_id": "economy",
  "difficulty": "hard",
  "count": 10
}

⸻

Study Plan Generator

POST /ai/plan

Request:

{
  "exam_id": "upsc",
  "hours_per_day": 6,
  "target_date": "2026-06-01"
}

⸻

Answer Evaluation

POST /ai/evaluate

Request:

{
  "question": "Explain parliamentary sovereignty",
  "answer": "User answer text..."
}

Response:

{
  "score": 8.2,
  "feedback": "Good structure, needs constitutional references",
  "improvements": [
    "Add Article references",
    "Include landmark cases"
  ]
}

⸻

4. TOOLS LAYER (UNIVERSAL LLM INTERFACE)

This is the most important part for Claude, GPT, Gemini, and all future models.

⸻

List Tools

GET /tools

⸻

Execute Tool

POST /tools/execute

Request:

{
  "tool": "explain_topic",
  "input": {
    "topic_id": "fundamental_rights",
    "exam_id": "upsc",
    "level": "intermediate"
  },
  "context": {
    "user_id": "u123",
    "session_id": "s456"
  }
}

Response:

{
  "output": {
    "explanation": "...",
    "examples": [],
    "pyqs": []
  }
}

⸻

Tool Types

Tool	Purpose
explain_topic	Explain syllabus concepts
generate_quiz	Create questions
search	Semantic search
create_plan	Study planning
evaluate_answer	Check answers
get_pyqs	Past questions

⸻

5. PYQ API

⸻

Get PYQs

GET /pyqs?exam_id=upsc&topic_id=xyz

⸻

6. PROGRESS API

⸻

Get Progress

GET /users/{user_id}/progress

⸻

Update Progress

POST /progress/update

⸻

7. ANALYTICS API

⸻

Learning Analytics

GET /analytics/user/{user_id}

Response:

{
  "accuracy": 74,
  "study_hours": 210,
  "weak_topics": ["economy", "ethics"],
  "readiness_score": 0.68
}

⸻

ERROR FORMAT

{
  "error": {
    "code": "INVALID_REQUEST",
    "message": "Missing exam_id"
  }
}

⸻

RATE LIMITS

Tier	Limit
Free	60 req/min
Pro	600 req/min
AI endpoints	separate quota

⸻

VERSIONING

v1 → Stable
v2 → Future expansion

⸻

SECURITY MODEL

* All AI endpoints require authentication
* Tools are permission-controlled
* Ingestion is internal-only
* No direct DB access
* Context is user-isolated

⸻

UNIVERSAL AI COMPATIBILITY

ExamVerseOS API is designed to work with:

GPT-style models

* Function calling
* Tool execution

Claude-style models

* Structured tool schemas

Gemini-style models

* JSON tool execution

Local LLMs

* Open tool protocol

⸻

FINAL ARCHITECTURE PRINCIPLE

This API is not built for one AI model.

It is built for ALL AI models.

⸻

END GOAL

Any system should be able to:

1. Call ExamVerseOS API
2. Fetch structured knowledge
3. Use tools
4. Generate grounded educational intelligence

Without knowing internal implementation.