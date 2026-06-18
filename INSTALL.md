# Instalação — figma-refactor

## Pré-requisitos

- [Claude Code](https://claude.com/claude-code) instalado
- MCP do Figma ativo na sua instalação do Claude Code
  ([instruções oficiais](https://help.figma.com/hc/en-us/articles/32132100833559))
- Acesso de edição ao arquivo Figma que será refatorado

---

## Opção A — instalação recomendada (1 comando)

Funciona em macOS, Linux e Windows:

```bash
npx skills add milenacmiranda-designer/figma-refactor
```

A CLI [`skills`](https://github.com/vercel-labs/skills) detecta o Claude Code, baixa a skill direto do GitHub e instala no diretório correto. Use a flag `-g` se quiser instalar globalmente:

```bash
npx skills add milenacmiranda-designer/figma-refactor -g
```

Depois, reinicie o Claude Code.

---

## Opção B — instalação manual (git clone)

Use esta opção se preferir clonar o repo e versionar a skill localmente.

### 1. Clone o repositório

```bash
git clone https://github.com/milenacmiranda-designer/figma-refactor.git
```

### 2. Mova para a pasta de skills do Claude Code

**macOS / Linux**
```bash
mv figma-refactor ~/.claude/skills/
```

**Windows (PowerShell)**
```powershell
Move-Item figma-refactor $env:USERPROFILE\.claude\skills\
```

A estrutura final deve ficar:

```
~/.claude/skills/figma-refactor/
├── SKILL.md
├── INSTALL.md
├── README.md
├── references/
├── templates/
├── agents/
└── harness/
```

### 3. Reinicie o Claude Code

---

## Como usar

No prompt do Claude Code:

```
Use o agente figma-harness-controller.
Arquivo Figma: [URL]
Execute apenas discovery.
```

A skill ativa automaticamente quando você escreve frases como:

- "quero refatorar esse Figma [URL]"
- "meu arquivo do Figma está bagunçado"
- "organizar as páginas desse Figma"
- "criar um design system nesse arquivo do Figma"
- "componentizar o Figma"

---

## Primeiro teste recomendado

Comece pequeno para entender o fluxo antes de rodar em um arquivo grande:

- Use uma página com **no máximo 6 frames**
- Execute apenas: `discovery → audit → plan → backup → organization → qa`
- Deixe `components`, `foundations` e `auto-layout` para um segundo experimento

---

## Problemas comuns

| Sintoma | Solução |
|---------|---------|
| Claude Code não reconhece a skill | Confirme que a pasta está em `~/.claude/skills/figma-refactor/` e que o `SKILL.md` está na raiz dela |
| Agente não consegue ler o Figma | Verifique se o MCP do Figma está ativo e se você tem acesso ao arquivo |
| Skill começa a refatorar sem perguntar | Reforce no prompt: "execute apenas discovery, não altere o arquivo" |
