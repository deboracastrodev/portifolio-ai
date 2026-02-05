---
stepsCompleted: ["step-01-init", "step-02-discovery", "step-03-success", "step-04-journeys", "step-05-domain"]
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

