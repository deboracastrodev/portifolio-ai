---
stepsCompleted: [1, 2]
lastStep: 2
inputDocuments: ["_bmad-output/planning-artifacts/prd.md", "_bmad-output/planning-artifacts/prd-validation-report.md", "_bmad-output/planning-artifacts/architecture.md", "docs/brainstorming.md", "docs/ux-spec-timeline.md"]
project_name: 'portifolio-ai'
user_name: 'debora'
date: '2026-02-06'
communication_language: 'portugues brasil'
document_output_language: 'portugues brasil'
---

# UX Design Specification - portifolio-ai

**Author:** debora
**Date:** 2026-02-06

---

<!-- UX design content will be appended sequentially through collaborative workflow steps -->

## Executive Summary

### Project Vision

**DevMentor AI** é um ecossistema de 8 agentes especializados em Inteligência Artificial que analisam vagas de emprego, identificam gaps de habilidades através de RAG (Retrieval-Augmented Generation), e realizam pair programming interativo para acelerar a carreira de desenvolvedores.

**Conceito Diferencial:** *"Self-Building Portfolio"* - os agentes que ajudam a desenvolver o projeto SÃO parte do projeto, criando um sistema auto-evolutivo que aprende com cada interação.

### Target Users

| Persona | Tipo | Principal Dor | O Que DevMentor Resolve |
|---------|------|---------------|-------------------------|
| **Julia** (24 anos) | Dev Júnior - Primary User | "O que estudar? Como impressionar recrutadores?" | Análise de vagas + direção clara + planos tangíveis |
| **Carlos** (35 anos) | Dev Sênior - O Cético | "IA vai atrapalhar? Código gerado tem qualidade?" | Debate entre agentes visível + pair programming real |
| **Recrutador** | Consumer (não user direto) | "Não consigo ver qualidade real dos candidatos" | Evidências infalsificáveis + documentação multi-camada |

### Key Design Challenges

**1. Latência de LLM com Performance Percebida**
- **Problema:** 8 agentes processando pode levar 3-5 segundos
- **Solução UX:** *"Thinking Stream" Timeline* com SSE streaming - transforma "tempo de espera" em "tempo de insight"

**2. Transparência para Céticos (Jornada Carlos)**
- **Problema:** Desenvolvedores seniores precisam VER que os agentes agregam valor real
- **Solução UX:** Toggle *"View Raw Debate"* mostrando o raciocínio entre agentes

**3. Visualização de Dados Complexos**
- **Problema:** Gap analysis, radar charts, matrizes de skills podem ser confusos
- **Solução UX:** Visualizações progressivas e intuitivas com revelação gradual de informação

### Design Opportunities

**1. Pattern "Thinking Stream"**
- Timeline interativa vertical onde agentes aparecem sequencialmente
- Streaming de texto com efeito "typewriter"
- Transforma latência em engajamento

**2. Documentação Multi-Camada**
- Conteúdo adaptado para três níveis: leigos, juniors e seniores
- Evidências infalsificáveis de capacidade técnica

**3. Gamificação Inteligente**
- Streaks, XP e levels baseados em progresso real (não só tempo de estudo)
- Métricas tangíveis: redução de gap, aumento de interview rate

**4. Pair Programming em Tempo Real**
- Editor colaborativo com feedback instantâneo dos agentes
- Avaliação real durante sessão (não auto-avaliação)
