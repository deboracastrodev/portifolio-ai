---
stepsCompleted: [1, 2]
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