# Regras de Design System

## Auto Layout
- Hug contents → componentes baseados em conteúdo
- Fill container → elementos responsivos
- Fixed → apenas com justificativa documentada
- Nunca usar retângulos espaçadores
- Usar padding e gap no lugar de spacers
- Converter grupos estruturais em frames com Auto Layout

## Variantes
Usar apenas para:
- Type: Primary, Secondary, Tertiary, Destructive
- Size: Small, Medium, Large
- State: Default, Hover, Focus, Disabled, Loading
- Status: Neutral, Success, Warning, Error

Para textos, ícones e visibilidade usar:
- Text property
- Boolean property
- Instance swap property

## Tokens
- Cores → sempre via variables semânticas
- Spacing → sempre via variables de spacing
- Radius → sempre via variables de radius
- Typography → sempre via text styles
- Nunca hardcode de hex, px avulso ou font-family direto

## Componentes
- Criar em 02 — Components antes de usar nas telas
- Apresentar para aprovação antes de substituir
- Um componente por vez
- Screenshot antes e depois de cada substituição

---

## Como criar de verdade (não só descrever)

Os agentes desta skill **escrevem no Figma via MCP**. Descrever o que criar
em texto não basta — precisa chamar `use_figma`. Antes de qualquer escrita:

### Pré-requisito obrigatório
1. Carregar a skill `figma:figma-use` (instrução obrigatória do MCP Figma —
   pular causa falhas silenciosas e difíceis de debugar)
2. Para construir o design system, carregar também
   `figma:figma-generate-library` (ensina a ordem certa e os patterns de
   variants/variables)

### Ordem correta de construção
1. **Variables primitivas** primeiro
   (`Color/Primitive/Blue/500`, `Spacing/16`, `Radius/Medium`)
2. **Variables semânticas com aliases** apontando para as primitivas
   (`Color/Semantic/Action/Primary` → alias de `Color/Primitive/Blue/500`)
3. **Modos** quando aplicável (light/dark) configurados na collection
4. **Component** com Auto Layout, padding/gap usando spacing variables
5. **Variant set** (`Component Property` → criar variantes Type/Size/State)
6. **Bind das variables** nas propriedades do componente
   (fill, stroke, padding, corner radius — tudo via variable, nunca hex/px)
7. **Text/Boolean/Instance Swap properties** para conteúdo variável
8. **Publish** quando aprovado

### Diferença crítica
- **Style de cor solto ≠ Variable**. Variable suporta modos, aliases e
  binding programático em qualquer propriedade. Style não.
- **Frame nomeado "Button" ≠ Component**. Component vira instance
  reutilizável com overrides; frame não.
- **Múltiplos componentes "Button/Primary", "Button/Secondary" ≠ Variant
  set**. Variant set é um único componente com property Type — instâncias
  trocam variante sem perder overrides.

### Validação
Depois de criar, **inspecionar via MCP** e confirmar:
- `figma_variables` retorna as variables criadas (não só styles)
- O componente aparece como `COMPONENT_SET` (não `FRAME`)
- Propriedades do componente listam as variant properties esperadas
- As fills/strokes/padding referenciam variable IDs (não valores literais)

Se a validação falhar, **refazer** — não seguir pra próxima fase com
"componente" que na verdade é frame.
