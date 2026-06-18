# figma-refactor

> Sistema controlado de refatoração de arquivos Figma — para quando seu arquivo está bagunçado e você quer organizar sem quebrar nada.

Uma skill para [Claude Code](https://claude.com/claude-code) que organiza, estrutura e componentiza arquivos Figma usando agentes especializados, com backup automático, gates por fase e rollback.

Funciona em arquivos **mobile, web ou híbrido**.

---

## Por que existe

Refatorar um arquivo Figma grande é arriscado. Você quer:

- Renomear páginas sem perder histórico
- Criar um design system sem quebrar telas existentes
- Componentizar repetições sem afetar protótipos
- Aplicar Auto Layout sem virar bagunça visual

Esta skill faz isso em **fases controladas**, com aprovação manual entre cada uma, backup automático antes de qualquer alteração e relatórios em cada etapa.

---

## Como funciona

```
Você fala: "quero refatorar esse Figma [URL]"
            ↓
   Harness Controller assume
            ↓
   Detecta tipo de projeto (mobile/web/híbrido)
            ↓
   Executa fases em sequência, com sua aprovação a cada gate
            ↓
   Backup antes de qualquer escrita
            ↓
   Rollback automático se algo der errado
```

### Fases

```
DISCOVERY → AUDIT → PLAN → BACKUP →
FOUNDATIONS → ORGANIZATION → AUTO_LAYOUT →
COMPONENTS → QA → APPROVAL → DONE
```

Uma fase só começa quando:
- a anterior estiver concluída
- o gate estiver aprovado
- não houver falha crítica
- você tiver confirmado

---

## Agentes incluídos

| Agente | Responsabilidade |
|--------|-----------------|
| **Harness Controller** | Orquestra tudo, controla fases e gates |
| **Auditor** | Lê e analisa estrutura, nomenclatura, inconsistências |
| **File Organizer** | Reorganiza canvas, páginas e seções |
| **Foundations** | Cria tokens (cores, tipografia, espaçamento) |
| **System Builder** | Cria components, variants e Auto Layout |
| **QA** | Valida o resultado contra checklist |

---

## Instalação

Um comando, em qualquer SO:

```bash
npx skills add milenacmiranda-designer/figma-refactor
```

Depois é só reiniciar o Claude Code.

**Requisitos:** [Claude Code](https://claude.com/claude-code) + MCP do Figma ativo.

> Prefere instalar manualmente (git clone)? Veja [INSTALL.md](INSTALL.md).

---

## Uso rápido

No prompt do Claude Code:

```
Use o agente figma-harness-controller.
Arquivo Figma: https://figma.com/file/...
Execute apenas discovery.
```

Ou, em linguagem natural, frases como:

- "quero refatorar esse Figma [URL]"
- "meu arquivo do Figma está bagunçado"
- "criar um design system nesse arquivo"
- "componentizar essas telas"

---

## Estrutura do projeto

```
figma-refactor/
├── SKILL.md                 # Manifesto da skill (lido pelo Claude Code)
├── INSTALL.md
├── README.md
├── LICENSE
├── references/              # Regras de design system, naming, harness
├── templates/               # Modelos de relatório (audit, plan, qa, incident)
├── agents/                  # 6 agentes especializados
└── harness/                 # Config, state, workflow, gates, tests, logs
```

---

## Princípios

- **Nunca alterar sem aprovação.** Toda fase com escrita exige confirmação explícita.
- **Backup antes de tudo.** Página `Archive` com cópia integral antes de qualquer escrita.
- **Escopo restrito.** Refatora só o que foi pedido — nada de "limpeza generalizada".
- **Logs e rollback.** Tudo é registrado; reverter é uma fase do workflow.
- **Pequeno antes de grande.** Recomenda-se começar por uma seção com até 6 frames.

---

## Status

`v0.1` — funcional, em uso real. Issues e PRs bem-vindos.

---

## Licença

MIT — veja [LICENSE](LICENSE).

Criado por [Milena Miranda](https://github.com/milenacmiranda-designer).
