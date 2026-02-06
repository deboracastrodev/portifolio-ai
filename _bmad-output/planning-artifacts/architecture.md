---
stepsCompleted: [1, 2, 3, 4, 5, 6, 7]
inputDocuments: ["_bmad-output/planning-artifacts/prd.md", "docs/ux-spec-timeline.md", "docs/brainstorming.md", "_bmad-output/planning-artifacts/research/tecnologias-rag-conhecimento-tecnico-research-2026-02-04.md"]
workflowType: 'architecture'
project_name: 'portifolio-ai'
user_name: 'debora'
date: '2026-02-05'
---

# Architecture Decision Document

_This document builds collaboratively through step-by-step discovery. Sections are appended as we work through each architectural decision together._

## Project Context Analysis

### Requirements Overview

**Functional Requirements:**
Análise e processamento de vagas de emprego através de um ecossistema de 8 agentes especializados. Inclui extração de skills, gap analysis, planos de estudo personalizados e sessões interativas de pair programming.

**Non-Functional Requirements:**
- **Performance:** Parser <500ms (p50), primeiro token dos agentes <1s, suporte a 100 usuários simultâneos no MVP.
- **Scalability:** Escalabilidade horizontal para backend e IA workers; pgvector otimizado para 1M+ registros.
- **Security:** Conformidade com LGPD/GDPR, criptografia AES-256 e Rate Limiting por usuário.
- **Accessibility:** WCAG 2.1 Level AA obrigatório.

**Scale & Complexity:**
- Projeto de alta complexidade devido à orquestração agentica e requisitos de tempo real, mas com um modelo de negócio B2C que exige foco em UX e personalização.

- Primary domain: AI-Powered Web Application (Career Development)
- Complexity level: Alta
- Estimated architectural components: ~10 (Frontend, Backend API, 8 Agent Workers, Vector DB, Redis Cache, WebSocket Server)

### Technical Constraints & Dependencies

- Dependência crítica de APIs de LLM (OpenAI inicialmente, migrando para LLaMA local).
- Necessidade de PostgreSQL 15+ com extensão pgvector.
- Uso de SSE para streaming e Socket.io para pair programming.

### Cross-Cutting Concerns Identified

- **Orquestração de Agentes:** Protocolo de debate para consistência e redução de alucinações (foco em papéis claros, memória local e modularidade).
- **Observabilidade:** Tracing detalhado do fluxo de decisão de cada agente (logs abrangentes).
- **Custo e Performance:** Estratégia de cache (Redis) para embeddings e respostas recorrentes; roteamento inteligente de LLMs (modelos menores para tarefas simples, maiores para complexas).

### Architecture Decision Record: Real-time Communication

**Decision:** Hybrid approach using Server-Sent Events (SSE) for agent output streaming and WebSockets (Socket.io) for interactive Pair Programming sessions.

**Rationale:**
- SSE é mais eficiente em recursos para o fluxo de dados unidirecional e de alto volume da argumentação dos agentes, otimizando escalabilidade e load balancing.
- WebSockets fornecem a baixa latência e o gerenciamento de estado bidirecional necessários para a edição colaborativa de código.
- Esta separação de preocupações permite melhor escalabilidade horizontal do motor de análise e alivia a carga do servidor para comunicações mais simples.

### Technical Risk Mitigation (Pre-mortem Insights)

- **Hallucination Prevention:** Implementação de "Critic Agent" com acesso a RAG de alta fidelidade e métricas de consistência entre agentes. Reforçado pela necessidade de papéis claros e design modular nos sistemas multi-agentes.
- **Latency Optimization:** Priorização de arquitetura assíncrona com streaming SSE; paralelização de agentes e cache de embeddings em Redis. A pesquisa valida a eficiência do SSE para o streaming.
- **Cost Management:** Roteamento inteligente de LLMs (Small Models para extração, Large Models para debate/decisão) para otimizar custos, conforme boas práticas de arquiteturas híbridas de LLM.

## Starter Template Evaluation

### Primary Technology Domain
Identificado como **Web Application (Full-stack) com foco em AI**.

### Selected Starters: Next.js (Frontend) e Fastify (Backend)

**Rationale for Selection:**
A combinação de `create-next-app` e um boilerplate com Fastify oferece uma base sólida, atualizada e performática, permitindo a flexibilidade necessária para a orquestração de agentes.

**Initialization Commands:**
```bash
# Frontend (Next.js 14, TypeScript, Tailwind CSS, App Router)
npx create-next-app@latest frontend --typescript --tailwind --app --src-dir

# Backend (Node.js, Fastify, TypeScript)
# A ser iniciado com um boilerplate minimalista.
```

## Engineering Standards & Documentation Framework

### MVP of Templates
Como parte do Epic 1, um conjunto inicial de templates será criado para estabelecer padrões:
- **Backend CRUD Example:** Um exemplo completo (Controller, Service, Repository, Schema, Tests).
- **Frontend CRUD Example:** Um exemplo com hooks React Query e componentes de UI.
- **Storybook:** Configuração inicial com 5 componentes base.

### Continuous Documentation Framework
A "Definição de Done" para todas as features incluirá:
- **Quality Checklist:** Um `CHECKLIST.md` em cada template para validar testes, schemas, segurança e padrões.
- **Post-Feature Documentation:** Um processo de duas camadas com documentação técnica (no código, para devs) e documentação de negócio (centralizada, para o time).

## Core Architectural Decisions

### Decision Priority Analysis

**Critical Decisions (Block Implementation):**
- Data Validation Strategy (Zod)
- Database Migration Tool (Prisma)
- Authentication Provider (NextAuth.js)
- API Design Pattern (tRPC)

**Important Decisions (Shape Architecture):**
- Authorization Pattern (RBAC)
- State Management (React Query + Zustand)
- Infrastructure Providers (Vercel + Railway)

### Data Architecture

**Database Strategy:**
- **Decision:** Hybrid Model (PostgreSQL + Redis)
- **Rationale:** PostgreSQL (via Railway) handles relational data (users, vacancies) and semi-structured data (agent history via `JSONB`). Redis handles high-speed caching and session data.
- **Tools:** PostgreSQL 15+ (with `pgvector`), Redis 7+.

**Validation & Modeling:**
- **Decision:** Shared Schemas with Zod + Prisma ORM
- **Rationale:** Zod provides end-to-end type safety (frontend forms <-> backend API). Prisma manages schema migrations securely and offers a fully typed database client.
- **Tools:** Zod v3+, Prisma v5+.

### Authentication & Security

**Authentication:**
- **Decision:** NextAuth.js (v5)
- **Rationale:** Offers full control, supports strategic providers like LinkedIn natively, and incurs no extra cost.
- **Provider:** LinkedIn (Strategic for career data).

**Authorization:**
- **Decision:** Simple Role-Based Access Control (RBAC)
- **Rationale:** Pragmatic for MVP. A simple `role` column in the User table ('USER', 'ADMIN') covers all initial needs.

### API & Communication Patterns

**Internal API:**
- **Decision:** tRPC (TypeScript Remote Procedure Call)
- **Rationale:** Guarantees end-to-end type safety, accelerates development, and eliminates a class of client-server bugs.
- **Architecture:** Hexagonal Architecture allows adding a REST adapter later (e.g., for Mobile App) without changing business logic.

### Frontend Architecture

**State Management:**
- **Decision:** Dual Strategy (React Query + Zustand)
- **Rationale:** React Query manages server state (caching, revalidation) efficiently. Zustand manages client UI state with minimal boilerplate.

### Infrastructure & Deployment

**Hosting Strategy:**
- **Frontend:** Vercel (Hobby Tier) - Native Next.js support, zero cost for MVP.
- **Backend/DB:** Railway (Hobby/Pro) - Developer-friendly, native support for `pgvector` and Redis.
- **Cost Estimate:** ~$10-25 USD/month (Safety margin included).

**Deployment Pipeline:**
- **Decision:** Independent Automatic Deploys (Push-to-Deploy)
- **Rationale:** Simple and fast for MVP. Quality checks (lint/test) configured via Turborepo/GitHub Actions before merge.

## Implementation Patterns & Consistency Rules

### Pattern Categories Defined

**Critical Conflict Points Identified:**
Nomenclatura de arquivos, Estratégia de Testes, Tratamento de Erros e Padronização de Forms são as áreas de maior risco de inconsistência entre agentes.

### Naming Patterns

**Database Naming Conventions (Prisma):**
- **Models:** `PascalCase` e Singular (ex: `User`, `Vacancy`).
- **Fields:** `camelCase` (ex: `firstName`, `createdAt`).
- **Tables (Map):** `snake_case` e Plural (ex: `users`, `vacancies`).

**Code Naming Conventions:**
- **Variables/Functions:** `camelCase`.
- **React Components:** `PascalCase` (ex: `VacancyList`).
- **Files:**
    - Componentes: `PascalCase` (ex: `VacancyList.tsx`).
    - Non-Components: `kebab-case` (ex: `date-utils.ts`, `use-vacancy.ts`) para evitar conflitos de OS.

### Structure Patterns

**Project Organization:**
- **Feature-Sliced:** `src/features/{feature-name}/{components,hooks,services}`.
- **Shared UI:** `src/components/ui` (shadcn/ui).
- **Test Co-location:** Testes vivem ao lado do arquivo (ex: `VacancyList.test.tsx` ao lado de `VacancyList.tsx`).

### Communication & Process Patterns

**Centralized Error Handling:**
- **Backend:** Middleware global `onError` no tRPC para interceptar, logar e sanitizar erros antes de enviar ao cliente.
- **Frontend:** Callback global `onError` no `QueryClient` do React Query para disparar notificações (`Toaster`) automaticamente para falhas de API.

**Standardized Data Entry (Forms):**
- **Validation:** `react-hook-form` + `zod` resolver.
- **Components:** Uso de wrappers "Smart Inputs" (`CurrencyInput`, `DateInput`) que encapsulam máscaras de UI e normalização de dados (ex: string formatada -> number) automaticamente.
- **Response:** Sempre usar `TRPCError` com códigos semânticos.

### Enforcement Guidelines

**All AI Agents MUST:**
1.  Utilizar `kebab-case` para arquivos utilitários e `PascalCase` apenas para componentes React.
2.  Sempre implementar testes unitários co-locados (`.test.ts`) para nova lógica de negócio.
3.  Utilizar os wrappers de Input padronizados para qualquer entrada de dados, nunca o input HTML cru.

**Pattern Enforcement:**
- Validado via ESLint plugin (regras de nomenclatura).
- Validado via Code Review (humano e agente Reviewer).

## Project Structure & Boundaries

### Complete Project Directory Structure (Monorepo)

```
portifolio-ai/
├── README.md
├── package.json          # Turborepo root scripts
├── turbo.json           # Build pipeline config
├── .gitignore
├── .npmrc
├── apps/
│   ├── web/             # Frontend (Next.js 14)
│   │   ├── src/
│   │   │   ├── app/                 # App Router (Pages/Layouts)
│   │   │   ├── components/
│   │   │   │   ├── ui/              # shadcn/ui components
│   │   │   │   └── shared/          # Global implementation components
│   │   │   ├── features/            # Feature-Sliced Design
│   │   │   │   ├── auth/            # Login, Profile logic
│   │   │   │   ├── vacancy/         # Parser, Upload, Listing logic
│   │   │   │   ├── agents/          # Thinking Stream, Visualization logic
│   │   │   │   └── editor/          # Pair Programming Editor logic
│   │   │   ├── lib/                 # Utils, tRPC client, Env validation
│   │   │   ├── hooks/               # Global hooks
│   │   │   └── styles/              # Global CSS
│   │   ├── public/
│   │   ├── next.config.js
│   │   ├── tailwind.config.ts
│   │   └── tsconfig.json
│   └── server/          # Backend (Fastify)
│       ├── src/
│       │   ├── adapters/            # Hexagonal Adapters (In/Out)
│       │   │   ├── http/            # Fastify Routes (Webhooks, SSE)
│       │   │   └── trpc/            # tRPC Context & Router Implementation
│       │   ├── core/                # Hexagonal Core (Business Logic)
│       │   │   ├── agents/          # Multi-Agent System Logic
│       │   │   ├── vacancy/         # Parser Logic
│       │   │   └── editor/          # Code Execution Logic
│       │   ├── infra/               # Infrastructure Implementations
│       │   │   ├── db/              # Prisma Service
│       │   │   ├── redis/           # Cache Service
│       │   │   └── llm/             # OpenAI/LocalAI Client
│       │   └── app.ts               # Entry point
│       ├── tsconfig.json
│       └── package.json
└── packages/
    ├── db/              # Shared Database Module
    │   ├── prisma/
    │   │   └── schema.prisma
    │   └── src/         # Generated Client export
    ├── api/             # Shared tRPC Definition
    │   └── src/         # AppRouter type definition
    ├── config/          # Shared Configuration
    │   ├── eslint-preset.js
    │   └── tailwind-preset.js
    └── schemas/         # Shared Zod Schemas
        └── src/         # DTOs for Frontend & Backend
```

### Architectural Boundaries

**API Boundaries (tRPC + Adapters):**
- **Internal:** `packages/api` define o contrato estritamente tipado entre `web` e `server`.
- **External:** `apps/server/src/adapters/http` expõe endpoints REST/Webhooks se necessário (ex: Webhook de pagamento).

**Data Boundaries:**
- **Database:** Apenas `apps/server` importa `packages/db`. O frontend é agnóstico ao banco de dados.
- **Shared Schemas:** `packages/schemas` é a "Linguagem Ubíqua" do sistema, importada por todos (`web`, `server`, `db`).

### Requirements to Structure Mapping

**Epic 2: Parser de Vagas**
- **Upload UI:** `apps/web/src/features/vacancy/components/UploadForm.tsx`
- **Validation:** `packages/schemas/src/vacancy.ts`
- **Parser Logic:** `apps/server/src/core/vacancy/parser.service.ts`
- **Vector Storage:** `apps/server/src/infra/db/vector-store.ts`

**Epic 3: Multi-Agent System**
- **Orchestration:** `apps/server/src/core/agents/orchestrator.ts`
- **Thinking UI:** `apps/web/src/features/agents/components/ThinkingStream.tsx`
- **Real-time:** `apps/server/src/adapters/http/sse.ts` (Server-Sent Events)

**Epic 5: Pair Programming**
- **Editor UI:** `apps/web/src/features/editor/components/CodeEditor.tsx`
- **Collaboration:** `apps/server/src/adapters/ws/socket-server.ts` (Socket.io)

### Development Workflow Integration

**Monorepo Workflow:**
- **Build:** `turbo build` orquestra o build de `web`, `server` e `packages` em paralelo, respeitando dependências.
- **Dev:** `turbo dev` inicia todos os serviços simultaneamente.
- **Lint/Test:** `turbo lint test` garante qualidade em todo o monorepo com um comando.

**Code Formatting & Quality Methodology:**
- **Tools:** Prettier (Style) + ESLint (Quality).
- **Strategy:** Shared configuration via `packages/config` applied equally to Backend and Frontend.
- **Enforcement:**
  - **IDE:** Format on Save enabled.
  - **Git Hook:** `husky` triggers `lint-staged` on pre-commit to auto-format and validate staged files.
  - **CI:** Build fails if linting errors exist.
- **Key Plugins:** `prettier-plugin-tailwindcss` (CSS sorting), `eslint-plugin-simple-import-sort` (Import sorting).

## Architecture Validation Results

### Coherence Validation ✅
**Decision Compatibility:**
A stack (Next.js, Fastify, Prisma, tRPC, Zod) é altamente coesa, garantindo Type-Safety de ponta a ponta. A arquitetura Hexagonal isola a complexidade dos agentes das escolhas de framework.

**Structure Alignment:**
O Monorepo com Feature-Sliced Design suporta perfeitamente a modularidade exigida pelos 8 agentes e pelas múltiplas features de UI.

### Requirements Coverage Validation ✅
**Functional Requirements:**
Todos os Epics (Parser, Agentes, Pair Programming) têm componentes e serviços mapeados na estrutura.

**Non-Functional Requirements:**
Latência, segurança e escalabilidade são endereçadas por decisões explícitas (Redis, SSE, NextAuth, RBAC).

### Implementation Readiness Validation ✅
**Status:** READY FOR IMPLEMENTATION
**Confidence Level:** High

**Key Strengths:**
1.  **Type-Safety Absoluta:** Zod + tRPC + Prisma eliminam classes inteiras de bugs.
2.  **Isolamento de Domínio:** A lógica dos agentes está protegida no `core`, facilitando testes e evolução.
3.  **DX Superior:** Monorepo, hot-reloading e validação automática de código.

### Architecture Completeness Checklist

**✅ Requirements Analysis**
- [x] Contexto analisado e complexidade avaliada.
- [x] Restrições técnicas e riscos (Pre-mortem) identificados.

**✅ Architectural Decisions**
- [x] Stack tecnológico definido e versionado.
- [x] Padrões de dados, segurança e comunicação estabelecidos.

**✅ Implementation Patterns**
- [x] Nomenclatura, estrutura e tratamento de erros padronizados.
- [x] Metodologia de qualidade de código (Lint/Format) definida.

**✅ Project Structure**
- [x] Estrutura de diretórios completa (Monorepo) definida.
- [x] Fronteiras de componentes e integrações mapeadas.

### Implementation Handoff

**First Implementation Priority:**
Executar o scaffolding do Monorepo e configurar o "MVP de Templates" (Epic 1).