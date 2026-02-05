---
stepsCompleted: ["step-01-init", "step-02-discovery", "step-03-success", "step-04-journeys", "step-05-domain", "step-06-innovation", "step-07-project-type", "step-08-scoping"]
inputDocuments: ["docs/brainstorming.md", "_bmad-output/planning-artifacts/research/tecnologias-rag-conhecimento-tecnico-research-2026-02-04.md"]
workflowType: 'prd'
documentCounts:
  briefCount: 0
  researchCount: 1
  brainstormingCount: 1
  projectDocsCount: 0
classification:
  projectType: Web Application (AI-Powered Career Acceleration - B2C)
  domain: Skill Validation & Evidence Generation
  complexity: Alta
  projectContext: greenfield
  features:
    - Interface web completa e robusta
    - Dashboard de métricas, visualização dos 8 agentes, chat pair programming
    - CLI como feature futura (v2.0+)
  techStack:
    - Backend: Node.js/Python
    - LLM: OpenAI/LLM local
    - Vector DB: pgvector
    - Frontend: React/Vue
  roadmap:
    - Validação → SaaS B2C quando validado
---  

# Product Requirements Document - portifolio-ai

**Author:** debora
**Date:** 2026-02-04

---

## Stakeholder Insights (via Stakeholder Round Table)

### User Segmentation

| Segmento | Tipo | Principal Preocupação | O que DevMentor Resolve |
|----------|------|----------------------|-------------------------|
| **Dev Júnior** | Primary User | "O que estudar? Como impressionar?" | Análise de vagas + pair programming + portfolio que impressiona |
| **Dev Sênior** | Secondary User | "IA vai atrapalhar? Tem qualidade?" | Aprender COM agentes que debatem entre si (reduz alucinações) |
| **Recrutador** | Consumer (não user direto) | "Não consigo ver qualidade real" | Evidências infalsificáveis + documentação multi-camada |

### Value Proposition

**Para Dev Júnior:**
> "Saiba exatamente o que estudar e construa um portfolio que impressiona recrutadores"

**Para Dev Sênior:**
> "Aprenda com multi-agentes que debatem entre si, reduzindo alucinações e aprofundando conhecimento"

**Para Recrutador:**
> "Veja evidências infalsificáveis de capacidade técnica: antes/depois, decisões técnicas, métricas de evolução"

### Key Risk Identification
- **Carlos (sênior cético)** representa o maior risco de adoção
- Precisamos demonstrar que os agentes *realmente* agregam valor
- O "debate entre agentes" é o diferencial que convence céticos

---

## Success Criteria

### User Success (Baseado em Dados Reais de Mercado)

| Métrica | Sem DevMentor | Com DevMentor | Melhoria | Fonte |
|---------|--------------|---------------|----------|-------|
| **Análise de 50 vagas** | 1-2 dias | **1-2 horas** | **90%+ mais rápido** | [Market Research](https://www.linkedin.com/pulse/270-applications-7-months-interviewing-land-job-new-grad-vincent-yeh) |
| **Plano tangível** | 2-4 semanas | **1 semana** | **75% mais rápido** | [Job Search Time](https://www.linkedin.com/pulse/average-job-search-time-tech-roles-us-20242025-antonio-montano-qehve) |
| **Job search completo** | 5-7 meses | **3.5-5 meses** | **20-30% mais rápido** | [Average Time Tech](https://standout-cv.com/stats/job-interview-statistics) |
| **Interview rate** | 3-15% | **5-20%** | **~67% melhoria** | [Interview Stats](https://blog.theinterviewguys.com/how-many-applications-it-takes-to-get-hired-in-2025/) |
| **Overall success** | 1-2% | **3-5%** | **50-250% melhoria** | [Success Rate](https://www.reddit.com/r/ExperiencedDevs/comments/16i5yot/whats_your_interview_to_application_ratio_right/) |

**Momento "AHA!":**
- Dev analisa vaga → Entende requisitos → Vê plano tangível → Sente-se preparado para propor soluções

**Caminho Tangível:**
- Compilado de stacks + Plano de estudos + Pair programming (disponível, opcional para o usuário)

### Business Success (Fase de Validação)

| Métrica | Target (3 meses) | Fonte de Validação |
|---------|------------------|-------------------|
| **Usuários ativos** | 50-100 usuários únicos | Analytics |
| **Engajamento** | ≥70% analisam ≥5 vagas | Product metrics |
| **Retenção** | ≥40% retornam em 7 dias | Retention analytics |
| **Valor percebido** | ≥20% dizem "obtive valor" | Survey/NPS |
| **Casos de sucesso** | 5-10 devs conseguiram emprego | Testimonials |

### Technical Success (CRÍTICO - sem isso não funciona)

| Componente | Métrica | Threshold | Justificativa |
|------------|---------|-----------|---------------|
| **Parser de Vagas** | Skills extraídas corretamente | **≥80%** | Se errar, plano é errado |
| **Debate Agentes** | Redução de alucinações | **≥50%** | Se alucinar, perde confiança |
| **Alinhamento** | Consistência entre agentes | **≥90%** | Se contradizerem, parece quebrado |
| **Latency** | Tempo de resposta | **<2s p50, <5s p95** | UX aceitável |

### Measurable Outcomes

- **User Success:** Dev Júnior analisa 50 vagas em 1-2 horas (vs 1-2 dias), tem plano tangível em 1 semana (vs 2-4 semanas)
- **Business Success:** 50-100 usuários ativos em 3 meses, ≥70% engajamento, ≥40% retenção 7 dias
- **Technical Success:** Parser ≥80% acurácia, Debate ≥50% redução alucinações, Alinhamento ≥90% consistência

---

## Product Scope

### MVP - O MÍNIMO para Validar

- ✅ Parser de Vagas (OBRIGATÓRIO - input inicial)
- ✅ 8 Agentes Especializados
- ✅ Planos de Estudo/Estratégia de Portfolio
- ✅ Dashboard Visual (agentes, métricas, progresso)
- ✅ Debate entre Agentes (diferencial competitivo)
- ✅ Pair Programming (DISPONÍVEL - usuário escolhe se usa)

**Fluxo MVP:**
```
Vaga → Parser → Agentes analisam → Plano de Estudo ─→ [OU] Pair Programming
                                                       └→ [OU] Só com o plano
```

### Growth Features (Post-MVP)

- Devs conseguindo realocação
- Cases de sucesso "queria X, consegui X"
- Taxa de sucesso acima da média do mercado (3-5% vs 1-2%)
- Word-of-mouth e indicações orgânicas
- Métricas de sucesso comprovadas

### Vision (Future)

- Comunidade de DevMentor (devs trocando experiências)
- Cases de sucesso documentados e inspiradores
- Referência em carreira tech ("Quer crescer? Usa DevMentor")
- Recrutadores buscando candidatos validados pelo DevMentor
- Ecosistema de aprendizado contínuo

---

## Research Sources

- [Job Application Statistics 2025](https://blog.theinterviewguys.com/how-many-applications-it-takes-to-get-hired-in-2025/)
- [270 Applications Case Study](https://www.linkedin.com/pulse/270-applications-7-months-interviewing-land-job-new-grad-vincent-yeh)
- [Interview Rate Reddit](https://www.reddit.com/r/ExperiencedDevs/comments/16i5yot/whats_your_interview_to_application_ratio_right/)
- [Job Interview Statistics](https://standout-cv.com/stats/job-interview-statistics)
- [Average Job Search Time](https://www.linkedin.com/pulse/average-job-search-time-tech-roles-us-20242025-antonio-montano-qehve)
- [Tulla Bootcamp Results](https://tullabr.com/)
- [Coodesh Processo Tech](https://coodesh.com/blog/rh-tech/recrutamento/processo-de-recrutamento-e-selecao-tech/)

---

## User Journeys

### Journey 1: Julia - Dev Júnior (Primary User - Happy Path)

**Persona:**
- **Nome:** Julia, 24 anos
- **Situação:** Formada bootcamp há 6 meses, 150+ candidaturas, 0 respostas
- **Dor:** "Estudo tanto mas não sei se é o certo. Vagas pedem mil coisas."
- **Gol:** Emprego júnior em empresa tech respeitável

**Fluxo Completo:**

1. **Input das Vagas:** Upload de 20 vagas em arquivos .md/.txt ou links do LinkedIn
2. **Parser Inicial - TODAS as Skills:** Agentes analisam e retornam lista completa de skills encontradas
3. **Auto-avaliação Dinâmica:** Lista gerada baseada nas skills encontradas nas vagas
4. **Matriz de Intersecção:** Gap analysis mostrando skills mais solicitadas (80%+) vs o que ela sabe
5. **Pair Programming:** Sessão para construir case sugerido (TODO app com Zustand + Vitest)
6. **Evolução:** Radar chart atualizado mostrando progresso

**Momento AHA!:** Durante pair programming, agente Critic aponta gap real: *"Você esqueceu de tratar o loading state."* Julia pensa: *"Caramba, isso acontece na prática! Tô aprendendo de verdade."*

**Emoções:** Curiosa → Surpresa → Esperançosa → Engajada → Motivada

---

### Journey 2: Carlos - Dev Sênior (Secondary User - O Cético)

**Persona:**
- **Nome:** Carlos, 35 anos, 10+ anos de experiência
- **Situação:** Sênior estabelecido, curioso sobre IA
- **Dor:** "IA vai atrapalhar? Código gerado não tem qualidade."
- **Gol:** Aprender coisas novas sem perder qualidade

**Fluxo Completo:**

1. **Ceticismo Inicial:** Ouve sobre DevMentor de um júnior - *"Mais uma IA que gera código ruim..."*
2. **Teste com Vagas Sênior:** Upload de 5 vagas sênior/arquiteto
3. **Parser Avançado:** Skills como "System Design", "Microservices", "Event-Driven"
4. **Pair Programming Test:** Decide testar: *"Vou ver se esses agentes sabem algo"*
5. **Momento Surpresa:** Agente Architect sugere CQRS com event sourcing - *"Puts, nem tinha considerado..."*
6. **Conversão:** Percebe que agentes fazem ele PENSAR melhor, não só gerar código

**Momento AHA!:** *"Esses agentes realmente agregam valor - me fazem pensar sobre arquitetura de forma nova."*

**Emoções:** Cético → Curioso → Surpreso → Respeitoso → Poder User

---

### Journey 3: Admin - Operações (Gerenciar Sistema)

**Persona:**
- **Nome:** Pat, 28 anos, SRE/DevOps
- **Situação:** Responsável por manter DevMentor funcionando

**Fluxo Completo:**

1. **Dashboard Admin:** Monitoramento em tempo real - 50 usuários ativos
2. **Métricas de Saúde:** Parser 82% acurácia, Debate 52% redução alucinações
3. **Alerta:** Latency subiu para 4s p95 - investigar
4. **Investigação:** Logs mostram bottleneck no LLM local
5. **Fix:** Implementa cache no embedding service
6. **Resolução:** Latency volta para <2s p50, <5s p95

**Requisitos:** Dashboard de métricas, Monitoramento real-time, Alertas, Logs, Debug tools

---

### Journey 4: Support - Troubleshooting (Edge Case)

**Persona:**
- **Nome:** Sam, 30 anos, Customer Success

**Fluxo Completo:**

1. **Ticket:** Usuário reclama "Parser está errado!"
2. **Investigação:** Verifica vaga original - skill estava em "Requirements ocultos"
3. **Ação:** Ajusta configuração do Parser Agent para ler seções inteiras
4. **Validação:** Re-roda parser na vaga do usuário
5. **Resolução:** Parser agora identifica skill corretamente

**Requisitos:** Sistema de tickets, Re-run parser, Ajustes de configuração, Histórico de sessões

---

### Journey Requirements Summary

**Capabilities Reveladas pelas Jornadas:**

| Journey | Requisitos Chave |
|---------|------------------|
| **Julia** | Upload vagas (.md/.txt/links), Parser multi-skills, Auto-avaliação dinâmica, Matriz de intersecção, Pair programming, Radar chart evolução |
| **Carlos** | Parser vagas sênior, Pair programming avançado, Debate agentes visível, Arquitetura patterns |
| **Admin** | Dashboard métricas, Monitoramento real-time, Alertas, Logs, Debug tools |
| **Support** | Sistema tickets, Re-run parser, Ajustes configuração, Histórico sessões |

---

## Gamification Research Sources

- [Gamification in Career Development: A 2026 Imperative](https://www.linkedin.com/posts/nataliabielczyk_simulatedannealing-activity-7412120531560296449-j_64)
- [Gamification in Learning 2026](https://www.gocadmium.com/resources/gamification-in-learning)
- [Gamified Learning in 2026: Enhance Engagement](https://www.infoprolearning.com/blog/how-gamification-in-learning-boosts-engagement-and-improves-knowledge-retention/)
- [Gamification in 2026: Going Beyond Stars, Badges](https://tesseractlearning.com/blogs/view/gamification-in-2026-going-beyond-stars-badges-and-points)
- [Duolingo Engagement Analysis](https://uxdesign.cc/duolingo-analyzing-all-engagement-and-retention-techniques-3e73b79120cf)
- [Duolingo's Gamification Secrets](https://www.orizon.co/blog/duolingos-gamification-secrets)
- [Duolingo Streak System Design](https://medium.com/@salamprem49/duolingo-streak-system-detailed-breakdown-design-flow-886f591c953f)

---

## Innovation & Novel Patterns

### Detected Innovation Areas

**1. Career Intelligence com IA (Turbinar Carreira com Tendências de Mercado)**
- **O que é:** IA que analisa tendências de mercado e direciona preparação de carreira em tempo real
- **Inovação:** Carreira orientada por DADOS, não por "achismo" ou tendências passageiras
- **Diferencial:** Vagas são analisadas continuamente → currículo evolui proativamente antecipando demanda
- **Paradigma shift:** De "reagir a vagas" para "antecipar oportunidades de carreira"
- **Validação:** Parser + RAG identificam skills emergentes antes que se tornem mainstream

**2. Sistema de Métricas com Learning Loop (Cases de Sucesso/Erro da Comunidade)**
- **O que é:** Aprender com casos reais de sucesso e erro da comunidade de usuários
- **Inovação:** Crowdsourced learning - todos contribuem para a inteligência coletiva
- **Diferencial:** Não é só "seu progresso isolado", é "aprendizado da comunidade evolui o produto"
- **Paradigma shift:** De "learning isolado e egoísta" para "knowledge graph coletivo"
- **Validação:** Metrics dashboard mostra evolução comunitária + individual

**3. Stack Composition em Contexto Real (Ecossistemas Corporativos)**
- **O que é:** Entender não só tecnologias isoladas, mas como compõem ecossistemas corporativos reais
- **Inovação:** Análise de composição de stacks (ex: React + State Management + Testing + CI/CD = Frontend Production Stack)
- **Diferencial:** Prepara para "sistemas completos", não só "ferramentas isoladas"
- **Paradigma shift:** De "dominar ferramentas" para "entender arquitetura de sistemas em contexto"
- **Validação:** Parser identifica interseções e relações entre skills

**4. Pair Programming Direcionado a Oportunidades Específicas (Gap-Driven Learning)**
- **O que é:** Treinar com casos derivados de vagas reais do mercado atual
- **Inovação:** Gap-driven learning - aprender exatamente o que falta para aumentar odds de emprego
- **Diferencial:** Treino orientado a RESULTADO (conseguir a vaga), não só "conteúdo interessante"
- **Paradigma shift:** De "aprender random things" para "aprender o que move a agulha na carreira"
- **Validação:** Cases sugeridos são derivados de análise de 20+ vagas reais

---

### Market Context & Competitive Landscape

**Soluções Tradicionais vs DevMentor AI:**

| Aspecto | Soluções Tradicionais | DevMentor AI (Diferencial) |
|--------|----------------------|------------------------------|
| **Análise de vagas** | Manual, lenta, 1-2 dias para 20 vagas | IA automática, 1-2 horas, análise contínua |
| **Direção de estudos** | Baseada em "o que é popular/hype" | Baseado em "o que o mercado está pedindo AGORA" |
| **Conteúdo de estudo** | Projetos random (todo app, calculator, weather) | Cases derivados de vagas reais |
| **Métricas de progresso** | "Eu estudei X horas" (subjetivo) | "Reduzi gap em Y%, aumentei interview rate em Z%" (objetivo) |
| **Validação de skills** | Auto-avaliação subjetiva | Avaliação REAL durante pair programming |
| **Fonte de verdade** | Opinião própria ou de mentor | Dados do mercado + debate entre agentes |

**Concorrentes Diretos:**
- **Portfolio platforms:** (LinkedIn, Behance, GitHub) - Não têm IA/Análise de vagas
- **Learning platforms:** (Udemy, Coursera, Alura) - Não têm análise de vagas/métricas de carreira
- **Job boards:** (LinkedIn, Gupy, Glassdoor) - Não têm preparação direcionada
- **Code review tools:** (GitHub Copilot, CodeClimate) - Não têm carreira focus
- **Mentoria platforms:** (ADP, Mentoria Rocket) - Não têm IA/Análise automatizada

**Espaço Único:**
- Ninguém combina: Análise de vagas + Multi-agent RAG com debate + Pair Programming + Métricas objetivas de carreira

---

### Validation Approach

**Validação Técnica:**
- **Parser:** ≥80% acurácia em extração de skills (testado com dataset de vagas)
- **Debate Agentes:** ≥50% redução de alucinações (comparação sem/com protocolo de debate)
- **Engagement:** ≥70% analisam ≥5 vagas (comportamento de uso)
- **Latency:** <2s p50, <5s p95 (UX aceitável para IA)

**Validação de Mercado:**
- **Conversão de céticos:** Carlos (sênior) → power user valida que agentes agregam valor real
- **Resultado último:** Devs conseguindo emprego através de DevMentor
- **Promoção orgânica:** NPS ≥40 indica recomendação espontânea
- **Retenção:** ≥40% retornam em 7 dias mostra produto é "sticky"

**Validação de Inovação:**
- **First-mover advantage:** "AI-driven career intelligence" é espaço pouco explorado
- **Patenteável:** "Sistema multi-agentes para carreira tech com protocolo de debate entre agentes"
- **Publicações técnicas:** Papers/Blog posts sobre arquitetura建立 autoridade no domínio
- **Open-source strategy:** Comunidade + código aberto = moat defensível contra concorrentes

---

### Risk Mitigation

| Risco | Probabilidade | Impacto | Mitigação |
|-------|--------------|---------|-----------|
| **Alucinação IA sugere caminho errado** | Alta | Crítico | Debate entre agentes + validação humana no pair programming |
| **Mercado muda rápido, skills ficam obsoletas** | Média | Alto | Análise contínua de vagas → sistema se adapta em tempo real |
| **Dev usa só auto-avaliação, evita pair programming** | Média | Alto | Pair programming é disponível mas não obrigatório - valor dele é evidente |
| **Muita concorrência no futuro (copia o conceito)** | Média | Médio | Open-source first + comunidade forte = moat defensivo |
| **Complexidade técnica assusta usuários júnior** | Média | Alto | UX intuitiva, onboarding guiado, casos sugeridos claros |
| **Usuário se torna dependente do sistema** | Baixa | Baixo | Sistema gera autonomia e skills - usuário se torna mais capaz |
| **LLM API custa caro para escalar** | Alta | Alto | Open-source first (LLM local) + otimizações (cache, batching) |

---

## Research Sources - Innovation

- [Multi-Agent RAG Systems](https://rahulkolekar.com/building-agentic-rag-systems-with-langgraph/)
- [Career Intelligence Trends 2026](https://www.gem.com/blog/10-takeaways-from-the-2025-recruiting-benchmarks-report)
- [AI-Powered Career Development](https://www.infoprolearning.com/blog/how-gamification-in-learning-boosts-engagement-and-improvements-knowledge-retention/)

---

## Web Application Specific Requirements

### Project-Type Overview

**DevMentor AI** é uma **Single Page Application (SPA)** B2C que oferece carreira tech acelerada através de IA multi-agentes. A aplicação combina dashboard interativo com visualizações gamificadas, parser de vagas, sistema de pair programming e multi-agentes RAG com debate protocol.

**Arquitetura:** SPA moderna com backend separado, comunicação via REST API + WebSocket para features real-time.

---

### Architecture Decision Records (Multi-Architect Debate)

#### ADR-001: Frontend Architecture - Hybrid SSR/SPA

| Aspect | Decision | Trade-off |
|--------|----------|-----------|
| **Architecture** | Hybrid (Next.js) | SEO complexity vs UX fluid |
| **Public pages** | SSR | Landing, features, blog, success stories |
| **Private app** | SPA | Dashboard, parser, pair programming |
| **Complexity** | Accept | Worth trade-off for dual optimization |

**Rejected:** Pure MPA (poor UX), Pure SPA (poor SEO)

#### ADR-002: Frontend Framework

**Decision:** React 18 + Next.js 14 (App Router) + shadcn/ui + Tailwind CSS

**Rejected:**
- Vue, Svelte, Angular - Smaller community/talent pool
- Reason: React ecosystem maturity, talent pool availability

#### ADR-003: Real-time Strategy

| Feature | Technology | Why |
|----------|-----------|-----|
| Pair programming | WebSocket (Socket.io) | Bidirectional, low latency |
| Agent processing status | Server-Sent Events | Unidirectional, simpler |
| Dashboard updates | Short polling (30s) + cache | Reduces server load |
| Notifications | Web Push API | Browser native |

#### ADR-004: Vector Database

**Decision:** pgvector + PostgreSQL (self-hosted)

**Rejected:** Pinecone, Qdrant (90% more expensive)

**Cost:** ~$20/mo vs $100+/mo (SaaS)

#### ADR-005: LLM Strategy

**Decision:** Hybrid - OpenAI gpt-4 (MVP) → LLaMA 3 70B local (Growth)

**Cost at scale:**
- MVP (100 users): ~$200/mo (OpenAI)
- Growth (1000 users): ~$50/mo (LLaMA local)
- Savings: 97% cheaper

#### ADR-006: State Management

**Decision:** Zustand (client) + React Query (server)

**Rejected:** Redux Toolkit (more boilerplate, larger bundle)

---

### Technical Architecture Stack

```yaml
frontend:
  framework: React 18 + Next.js 14 (App Router)
  ui: shadcn/ui + Tailwind CSS
  state:
    client: Zustand  # 3KB, minimal boilerplate
    server: React Query  # caching, revalidation
  real-time:
    pair_programming: Socket.io (WebSocket)
    agent_status: Server-Sent Events
    dashboard: Short polling (30s) + cache
    notifications: Web Push API

backend:
  api: Node.js/TypeScript + REST
  real-time: Socket.io server + Redis pub/sub
  llm:
    mvp: OpenAI gpt-4 (validation)
    growth: LLaMA 3 70B local (Ollama + LocalAI)
    router: Cost-aware routing
  vector_db:
    primary: pgvector + PostgreSQL 15
    cache: Redis (embeddings hot)

infrastructure:
  cdn: Cloudflare/Vercel Edge (static assets)
  hosting: Vercel (frontend) + Railway/DigitalOcean (backend)
  monitoring: Sentry (errors) + Vercel Analytics
```

---

### Browser Matrix

**Navegadores Suportados (MVP):**

| Navegador | Versão Mínima | Estratégia | Observação |
|-----------|---------------|------------|------------|
| **Chrome** | Últimas 2 versões (~120+) | Primário | ~65% market share dev audience |
| **Edge** | Últimas 2 versões (~120+) | Primário | Chromium-based, parity com Chrome |
| **Firefox** | Últimas 2 versões (~115+) | Secundário | ~15% dev audience |
| **Safari** | Últimas 2 versões (~17+) | Secundário | ~10% dev audience (mais no iOS) |
| **Mobile** | iOS Safari 17+, Chrome Android 120+ | Otimizado | Responsivo, features reduzidas |

**Non-Supported:** Internet Explorer, Chrome <90, Firefox <85, Safari <15 (mensagem de upgrade)

---

### Responsive Design

**Breakpoints (Mobile-First):**

| Dispositivo | Largura | Layout | Features |
|-------------|---------|--------|----------|
| **Mobile** | < 640px | Single column | Navigation drawer, simplified dashboard |
| **Tablet** | 640px - 1024px | Adaptive | Dashboard otimizado, split view |
| **Desktop** | > 1024px | Multi-column | Full dashboard, multi-pane pair programming |

**Touch-Optimized:**
- Botões mínimos 44x44px
- Gestures swipe para navegação mobile
- Pull-to-refresh em listas

---

### Performance Targets (Revised - Post-Profiling)

#### Backend API Performance:

| Operation | Target | Strategy |
|-----------|--------|----------|
| **Parser (single vaga)** | **<500ms** | pgvector HNSW index |
| **8 Agents + Debate** | **<3s** (streamed) | Streaming results |
| **Auto-avaliação save** | **<200ms** | Redis cache |
| **Dashboard load** | **<500ms** | Pre-computed + cache |
| **Pair programming msg** | **<100ms** | WebSocket + Redis pub/sub |

#### Frontend Core Web Vitals:

| Metric | Target | Strategy |
|--------|--------|----------|
| **LCP** | **<1.5s** | Code splitting, CDN |
| **FID** | **<50ms** | Reduce JS bundle |
| **CLS** | **<0.05** | Image dimensions, skeleton |
| **TTI** | **<2s** | Lazy loading, SSR |

---

### SEO Strategy (Hybrid Approach)

**Abordagem Híbrida SSR/SPA:**

**Páginas Públicas (SSR - Next.js):**
- Landing page (`/`) - Marketing, value prop, CTA
- Features (`/features`) - Detalhes de funcionalidades
- Pricing (`/pricing`) - Planos futuros (SaaS)
- Blog (`/blog/*`) - Conteúdo sobre carreira tech
- Cases de sucesso (`/success-stories/*`) - Histórias de usuários

**Páginas Privadas (SPA - Client-only):**
- Dashboard (`/dashboard`) - Área autenticada
- Parser (`/parser`) - Upload e análise de vagas
- Pair Programming (`/pair`) - Sessões de código
- Profile (`/profile`) - Configurações do usuário
- Admin (`/admin`) - Painel administrativo

---

### Accessibility Level (WCAG 2.1 AA)

**Target: WCAG 2.1 Level AA (Non-Negotiable)**

| Feature | Accessibility Strategy |
|---------|------------------------|
| **Radar charts** | Data table alternative below |
| **Confetti** | Respect `prefers-reduced-motion` |
| **Colors** | axe DevTools validation (4.5:1 contrast) |
| **Keyboard nav** | Full keyboard support (no mouse-required) |
| **Screen readers** | Semantic HTML + ARIA labels |

**Checklist:**
- ✅ Semantic HTML (`<nav>`, `<main>`, `<article>`)
- ✅ ARIA labels on all icons
- ✅ Keyboard navigation (Tab, Enter, Escape)
- ✅ Focus indicators (2px solid outline)
- ✅ Color contrast validated (4.5:1 minimum)
- ✅ Screen reader tested (NVDA, VoiceOver)
- ✅ `prefers-reduced-motion` respected

---

### Critical Performance Bottlenecks & Solutions

#### Bottleneck #1: pgvector Similarity Search

**Problem:** Full table scan on 50K+ skills = Parser takes 5-8s

**Solution:** Add HNSW index (50-100x improvement)

```sql
CREATE INDEX CONCURRENTLY skills_embedding_hnsw
ON skills USING hnsw (embedding vector_cosine_ops)
WITH (m = 16, ef_construction = 64);
```

#### Bottleneck #2: No Streaming Results

**Problem:** User waits 5-8s with spinner = perceived slowness

**Solution:** Server-Sent Events streaming (perceived latency 8s → 1s)

#### Bottleneck #3: Large Initial Bundle

**Problem:** 450KB JS bundle = 3.5s Time to Interactive

**Solution:** Code splitting + dynamic imports (60% reduction)

#### Bottleneck #4: No Embedding Cache

**Problem:** Repeated LLM API calls for similar vagas

**Solution:** Redis cache with 1-hour TTL (95% cache hit rate)

---

### Cache Strategy Hierarchy

```
Request Flow:
User → CDN (static) → Browser Cache (API) → Redis (data) → DB (source)

Cache Targets:
- CDN: >95% hit rate (static assets)
- Browser: 40% hit rate (API responses, 5min TTL)
- Redis: 90% hit rate (DB queries, 5min TTL)
- Redis: 95% hit rate (embeddings, 1hour TTL)
- DB: Only 10% of requests hit database
```

---

### Performance Optimization Roadmap

#### Phase 1: Quick Wins (Week 1)
- ✅ Add HNSW index to pgvector
- ✅ Implement Redis caching for embeddings
- ✅ Add CDN for static assets
- **Expected impact:** 5-10x faster parser

#### Phase 2: Streaming (Week 2)
- ✅ Implement streaming results for agent processing
- ✅ Add progressive loading UI
- ✅ Add optimistic updates
- **Expected impact:** 5x perceived performance improvement

#### Phase 3: Bundle Optimization (Week 3)
- ✅ Code splitting by route
- ✅ Dynamic imports for heavy components
- ✅ Tree shaking unused code
- **Expected impact:** 60% smaller bundle

#### Phase 4: Monitoring (Week 4)
- ✅ Set up performance monitoring (Sentry, Vercel Analytics)
- ✅ Add Core Web Vitals tracking
- ✅ Alert on performance regression
- **Expected impact:** Data-driven optimization

---

### Implementation Considerations

**1. State Management Strategy:**
- Zustand for client state (user session, UI state)
- React Query for server state (skills, gaps, progress)
- React Context for theme/i18n (rarely changes)

**2. Progressive Web App (PWA):**
- Manifest.json for installability
- Service Worker for offline cache of assets
- Push notifications for engagement (streak reminders)

**3. Security:**
- CORS configured for API domain
- CSRF tokens in mutations
- Content Security Policy headers
- XSS protection (React default + sanitization)

**4. Monitoring & Analytics:**
- Error tracking (Sentry)
- Performance monitoring (Web Vitals, Lighthouse CI)
- User analytics (PostHog/Plausible - privacy-friendly)
- Feature flags (LaunchDarkly/O Flags)

---

### Technical Success Metrics (Updated)

| Component | Metric | Target | Justificativa |
|------------|--------|--------|---------------|
| **Parser de Vagas** | Skills extraídas corretamente | **≥80%** | Se errar, plano é errado |
| **Debate Agentes** | Redução de alucinações | **≥50%** | Se alucinar, perde confiança |
| **Alinhamento** | Consistência entre agentes | **≥90%** | Se contradizerem, parece quebrado |
| **Latency - Parser** | Tempo de resposta | **<500ms p50** | pgvector HNSW index |
| **Latency - Agents** | Primeiro resultado | **<1s p50** | Streaming starts immediately |
| **Latency - Complete** | Todos agentes | **<3s p95** | All agents + debate done |
| **Core Web Vitals** | LCP/FID/CLS | "Good" threshold | UX aceitável |

