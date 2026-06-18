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
