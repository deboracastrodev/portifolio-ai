---
stepsCompleted: ["step-01-init", "step-02-discovery"]
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

