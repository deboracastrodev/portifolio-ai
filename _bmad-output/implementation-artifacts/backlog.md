# Product Backlog - DevMentor AI

## Epic 1: Foundation & Infrastructure (Weeks 1-2)
- [ ] **Story 1.1: Project Scaffolding** - Initialize monorepo structure with Next.js (frontend) and Node.js (backend).
- [ ] **Story 1.2: Database Setup** - Configure PostgreSQL with `pgvector` extension.
- [ ] **Story 1.3: Authentication** - Implement NextAuth/Clerk for user management.
- [ ] **Story 1.4: Base UI Layout** - Create the main dashboard layout with Sidebar and Theme support.

## Epic 2: Job Ingestion & Parser Agent (Weeks 3-4)
- [ ] **Story 2.1: Vacancy Upload** - Create interface and API for uploading `.md`, `.txt`, and links.
- [ ] **Story 2.2: Parser Agent Implementation** - Develop the first agent to extract skills and requirements using LLM.
- [ ] **Story 2.3: Vector Pipeline** - Implement embedding generation and storage in `pgvector`.
- [ ] **Story 2.4: Search & History** - Create functionality to search and view previous vacancy analyses.

## Epic 3: Multi-Agent Intelligence (Weeks 5-7)
- [ ] **Story 3.1: Core Agent Development** - Implement Researcher, Architect, Coder, Reviewer, Critic, Teacher, Documenter, and Metrics agents.
- [ ] **Story 3.2: Debate Protocol** - Implement the logic for agents to "debate" and reduce hallucinations.
- [ ] **Story 3.3: Real-time Streaming** - Implement Server-Sent Events (SSE) to stream agent outputs to the UI.
- [ ] **Story 3.4: RAG Integration** - Enhance agents with specific technical knowledge via RAG.

## Epic 4: Career Intelligence & Gap Analysis (Weeks 8-9)
- [ ] **Story 4.1: Dynamic Self-Assessment** - Generate a skill checklist based on analyzed vacancies.
- [ ] **Story 4.2: Gap Analysis Matrix** - Calculate and visualize the gap between user skills and market demand.
- [ ] **Story 4.3: Study & Portfolio Plans** - Generate personalized roadmap and project suggestions.
- [ ] **Story 4.4: Skill Radar Charts** - Implement visual representation of user evolution.

## Epic 5: Interactive Pair Programming (Weeks 10-11)
- [ ] **Story 5.1: WebSocket Setup** - Configure Socket.io for real-time code collaboration.
- [ ] **Story 5.2: Pair Programming Interface** - Create the code editor and chat interface.
- [ ] **Story 5.3: AI Coding Assistant** - Integrate agents into the pair programming session.
- [ ] **Story 5.4: Performance Evaluation** - Implement automated assessment of user performance during coding.

## Epic 6: Gamification & Polish (Weeks 11-12)
- [ ] **Story 6.1: Gamification System** - Implement XP, Levels, and Streaks.
- [ ] **Story 6.2: Performance Optimization** - Implement HNSW index and Redis caching.
- [ ] **Story 6.3: Beta Testing & Bug Fixing** - Final polish based on user feedback.
- [ ] **Story 6.4: Deployment** - Set up CI/CD and deploy to production (Vercel/Railway).
