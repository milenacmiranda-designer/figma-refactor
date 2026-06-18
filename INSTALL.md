# Instalação — figma-refactor

## Pré-requisitos

- [Claude Code](https://claude.com/claude-code) instalado
- MCP do Figma ativo na sua instalação do Claude Code
  ([instruções oficiais](https://help.figma.com/hc/en-us/articles/32132100833559))
- Acesso de edição ao arquivo Figma que será refatorado

## 1. Clone o repositório

```bash
git clone https://github.com/milenacmiranda-designer/figma-refactor.git
```

## 2. Copie para a pasta de skills do Claude Code

Mova (ou faça symlink de) a pasta `figma-refactor/` para o diretório de skills da sua instalação do Claude Code:

**macOS / Linux**
```bash
mv figma-refactor ~/.claude/skills/
```

**Windows (PowerShell)**
```powershell
Move-Item figma-refactor $env:USERPROFILE\.claude\skills\
```

A estrutura final deve ficar assim:

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

## 3. Reinicie o Claude Code

Feche e abra o Claude Code novamente para que a skill seja carregada.

## 4. Como usar

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

## 5. Primeiro teste recomendado

Comece pequeno para entender o fluxo antes de rodar em um arquivo grande:

- Use uma página com **no máximo 6 frames**
- Execute apenas: `discovery → audit → plan → backup → organization → qa`
- Deixe `components`, `foundations` e `auto-layout` para um segundo experimento

## Problemas comuns

| Sintoma | Solução |
|---------|---------|
| Claude Code não reconhece a skill | Confirme que a pasta está em `~/.claude/skills/figma-refactor/` e que o `SKILL.md` está na raiz dela |
| Agente não consegue ler o Figma | Verifique se o MCP do Figma está ativo e se você tem acesso ao arquivo |
| Skill começa a refatorar sem perguntar | Reforce no prompt: "execute apenas discovery, não altere o arquivo" |
