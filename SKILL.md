---
name: figma-refactor
description: >
  Sistema completo de refatoração de arquivos Figma via MCP Figma com
  Harness Controller, agentes especializados, backup automático, controle
  de escopo, gates por fase, logs e rollback.
  Use SEMPRE que o usuário mencionar organizar, refatorar, limpar,
  estruturar ou arrumar qualquer arquivo Figma — mobile, web ou híbrido.
  Ativa com frases como: "quero refatorar esse Figma", "meu arquivo está
  bagunçado", "organizar as páginas", "criar design system", "componentizar
  o Figma", "tenho esse arquivo do Figma e quero refatorar".
  Requer Claude Code com MCP Figma ativo.
compatibility:
  tools: [mcp_figma]
  environment: claude-code
---

# figma-refactor

Sistema controlado de refatoração de arquivos Figma.
Funciona para qualquer projeto: mobile, web ou híbrido.

---

## Como funciona

```
Usuário fala: "quero refatorar esse Figma [URL]"
↓
Harness Controller assume o controle
↓
Detecta tipo de projeto e confirma com o usuário
↓
Executa fases em sequência com aprovação obrigatória
↓
Backup antes de qualquer alteração
↓
Rollback automático se algo der errado
```

---

## Agentes disponíveis

| Agente | Arquivo | Responsabilidade |
|--------|---------|-----------------|
| Harness Controller | agents/figma-harness-controller.md | Controla tudo |
| Auditor | agents/figma-auditor.md | Lê e analisa |
| File Organizer | agents/figma-file-organizer.md | Organiza canvas |
| Foundations | agents/figma-foundations.md | Cria tokens |
| System Builder | agents/figma-system-builder.md | Components e Auto Layout |
| QA | agents/figma-qa.md | Valida resultado |

---

## Fases obrigatórias

```
DISCOVERY → AUDIT → PLAN → BACKUP →
FOUNDATIONS → ORGANIZATION → AUTO_LAYOUT →
COMPONENTS → QA → APPROVAL → DONE
```

Uma fase só começa quando:
- a anterior estiver concluída
- o gate estiver aprovado
- não houver falha crítica
- o usuário tiver confirmado

---

## Como iniciar

Cole no prompt do Claude Code:

```
Use o agente figma-harness-controller.

Arquivo Figma: [URL]

Execute apenas discovery:
1. verificar MCP
2. inicializar state
3. definir read_only
4. identificar escopo
5. criar inventário
6. não alterar o Figma
7. apresentar próximo gate
```

---

## Referências

- references/global-rules.md → regras de proteção
- references/naming-rules.md → nomenclatura
- references/design-system-rules.md → sistema de design
- references/matriz-structure.md → estrutura de páginas
- references/harness-rules.md → regras do harness
- harness/config.yaml → configuração
- harness/state.yaml → estado atual
- harness/workflow.yaml → fluxo de fases
