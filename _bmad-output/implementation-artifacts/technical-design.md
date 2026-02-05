# Technical Design Document - DevMentor AI

## 1. System Architecture
The system will follow a monorepo approach or a clearly separated Frontend/Backend structure.

- **Frontend:** Next.js 14 (App Router)
  - Styling: Tailwind CSS + shadcn/ui
  - State Management: Zustand (Client) + React Query (Server)
  - Communication: REST API + WebSocket (Socket.io) + SSE
- **Backend:** Node.js with Express/Fastify (TypeScript)
  - LLM Orchestration: Custom Agent Framework (based on PRD requirements)
  - Search: pgvector for semantic search
  - Real-time: Socket.io for Pair Programming, SSE for Agent streaming
- **Database:** PostgreSQL 15+ with `pgvector` extension
- **Cache:** Redis (Active sessions, hot embeddings)

## 2. Database Schema (Draft)

### `users`
- `id`: UUID (Primary Key)
- `email`: String (Unique)
- `name`: String
- `created_at`: Timestamp

### `vacancies`
- `id`: UUID (Primary Key)
- `user_id`: UUID (Foreign Key)
- `raw_content`: Text
- `source_url`: String
- `processed_data`: JSONB (Structured skills, requirements)
- `created_at`: Timestamp

### `skills`
- `id`: UUID (Primary Key)
- `name`: String (Unique)
- `category`: Enum (Backend, Frontend, Cloud, etc.)
- `embedding`: Vector(1536) (OpenAI `text-embedding-3-small` dimensions)

### `user_skills`
- `user_id`: UUID
- `skill_id`: UUID
- `level`: Integer (1-5)
- `last_updated`: Timestamp

### `agent_sessions`
- `id`: UUID (Primary Key)
- `user_id`: UUID
- `vacancy_id`: UUID
- `status`: Enum (Processing, Debating, Completed)
- `history`: JSONB (Logs of agent interactions)

## 3. Agent Protocol
The "Debate Protocol" will be implemented as a state machine.

1. **Parser Agent:** Extracts skills.
2. **Researcher Agent:** Validates skills against a technical knowledge base (RAG).
3. **Critic Agent:** Challenges findings (detects hallucinations).
4. **Consensus:** If agents disagree, a "Lead Agent" (Architect) mediates until consensus or a timeout.

## 4. API Endpoints (Core)

- `POST /api/vacancies/upload`: Handles file/link ingestion.
- `GET /api/vacancies/:id`: Returns processed vacancy data.
- `POST /api/agents/process`: Triggers the multi-agent analysis.
- `GET /api/agents/stream/:session_id`: SSE endpoint for real-time updates.
- `POST /api/user/skills`: Updates user self-assessment.
- `GET /api/analysis/gap`: Returns the gap analysis matrix.
