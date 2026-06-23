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

---

## Regra geral para qualquer componente

A regra abaixo vale pra **todo componente** que o System Builder identificar
— Button, Input, Card, Toast, Badge, Avatar, Navigation, Empty State,
Modal, Tooltip, qualquer outro. Não tem regra especial por tipo.

### Mapeamento universal

| O que muda no componente | Como modelar no Figma |
|---|---|
| **Estados** (Default, Hover, Focus, Disabled, Filled, Error, Loading, Success, Warning, Info, Active, Inactive…) | **Variant property `State`** — uma variante por estado |
| **Tipos/famílias** (Primary, Secondary, Tertiary, Destructive, Outlined, Ghost…) | **Variant property `Type`** |
| **Tamanhos** (Small, Medium, Large, XL…) | **Variant property `Size`** |
| **Cor de cada estado** (fundo, borda, texto, ícone) | **Variable semântica** consumida pelos fills/strokes da variante (`Action/Primary-Hover`, `Border/Focus`, `Feedback/Error`, `Surface/Disabled`…) |
| **Spacing/Radius por tamanho** | **Variable de spacing/radius** bindada em padding, gap, corner radius |
| **Conteúdo textual** (label, título, descrição, mensagem) | **Text property** |
| **Mostrar/esconder** (ícone, ação, badge, avatar) | **Boolean property** |
| **Trocar ícone, avatar ou sub-componente** | **Instance swap property** |

### Quais estados existem por componente
Não inventar — usar só o que o produto realmente precisa. Inventário comum:

- Button → Default, Hover, Focus, Disabled, Loading
- Input → Default, Focus, Filled, Error, Disabled
- Card → Default, Hover, Selected, Disabled
- Toast → Success, Warning, Error, Info (no `Type`, não `State`)
- Badge → Neutral, Success, Warning, Error (no `Type`)
- Navigation item → Default, Hover, Active, Disabled
- Avatar → variações de tamanho + boolean `Show Image`
- Empty/Error State → variantes por contexto + text/boolean properties

### Regra que NÃO se quebra
- **Nunca** criar variante só pra trocar texto, ícone ou cor.
  Texto = text property. Ícone = instance swap. Cor de estado = variable
  já bindada na variante existente.
- **Nunca** duplicar component master ("CardLarge", "CardSmall"). Size é
  variant property no mesmo component set.
- **Nunca** usar hex literal numa variante de estado. O que muda entre
  Default e Hover é **qual variable a fill referencia**, não o valor.

---

## Texto — três coisas que se confundem

"Texto" não é uma coisa só. Cada aspecto tem um lugar diferente:

### 1. Conteúdo (o que está escrito)
→ **Text property** no componente.

Button tem `Label`, Card tem `Title` + `Description`, Toast tem `Message`.
**Nunca** criar variante "Button/Salvar" e "Button/Cancelar" — isso é
text property.

### 2. Estilo tipográfico (família, peso, tamanho, line-height)
→ **Text Style** é o padrão (`Heading/Large`, `Body/Medium`, `Caption`).

Continuar usando text style pra maioria dos casos.

**Quando virar Variable em vez de Style:** apenas se o produto tem
**modos de tipografia** (ex.: escala mobile vs desktop, tema "compact" vs
"comfortable"). Figma suporta variables de font family, weight, size e
line-height — style não tem modos.

### 3. Cor do texto
→ **Variable semântica** (`Text/Primary`, `Text/Secondary`, `Text/Disabled`,
`Text/Inverse`), bindada no **fill da camada de texto**.

A cor **não** vai dentro do text style. Vai como fill bindado à variable.
Assim a mesma `Body/Medium` aparece Primary num card e Disabled num input
sem precisar criar `Body/Medium-Primary` e `Body/Medium-Disabled`.

### Mapeamento

| Aspecto do texto | Onde mora |
|---|---|
| O que está escrito | Text property |
| Família + peso + tamanho + line-height | Text Style (Variable só se houver modos) |
| Cor | Variable semântica (`Text/*`), bindada no fill |
| Estado (texto fica Disabled, Error) | A variante do componente troca a **variable** da cor, não o text style |
