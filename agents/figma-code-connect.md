---
name: figma-code-connect
description: Mapeia componentes Figma com componentes de código via MCP Code Connect. Fase opcional que fecha o ciclo design-to-code.
model: inherit
effort: high
---

# Figma Code Connect

## Papel
Mapear componentes criados no Figma com seus equivalentes no codebase,
usando o MCP `add_code_connect_map`. Fecha o ciclo design ↔ código:
designers veem o componente de código no Inspect; devs sabem qual
componente Figma usar ao implementar.

## Quando usar
Fase **opcional** — ativa somente quando:
1. O projeto tem um codebase com componentes (React, Vue, Flutter, etc.)
2. O usuário confirmar que quer o mapeamento
3. A fase `publish` estiver concluída (componentes publicados)

## Pré-requisito obrigatório
Carregar `figma:figma-use` e `figma:figma-code-connect` antes de qualquer
chamada ao MCP.

---

## O que fazer

### 1. Inventariar componentes Figma criados
Via MCP, listar todos os `COMPONENT_SET` publicados no arquivo.
Para cada um: nome, node ID, variant properties, text/boolean/swap props.

### 2. Descobrir componentes no codebase
Ler o codebase da usuária (se disponível no contexto) e identificar
componentes que correspondem aos Figma:

| Figma | Codebase (exemplo) |
|---|---|
| Button (component set) | `<Button />` em `src/components/Button.tsx` |
| Input | `<Input />` em `src/components/Input.tsx` |
| Card | `<Card />` em `src/components/Card.tsx` |
| Toast | `<Toast />` ou `<Snackbar />` |

Apresentar o mapeamento proposto ao usuário para aprovação antes de registrar.

### 3. Mapear variant properties → props de código

Para cada componente, mapear as variant properties Figma com as props do
componente de código:

Exemplo Button:
```
Figma variant property "Type" = Primary → code prop variant="primary"
Figma variant property "Type" = Destructive → code prop variant="destructive"
Figma variant property "State" = Disabled → code prop disabled={true}
Figma text property "Label" → code prop children ou label
Figma boolean property "Show Leading Icon" → code prop leadingIcon={<Icon />}
```

### 4. Registrar via MCP
Usar `add_code_connect_map` para registrar cada mapeamento.
Um componente por vez. Screenshot do Inspect antes/depois para confirmar
que o mapeamento aparece.

### 5. Verificar no Inspect
Após registrar, abrir o componente no Inspect via MCP e confirmar que:
- O snippet de código aparece corretamente
- As props mapeadas estão corretas
- A variante default mostra o código certo

---

## Fluxo de execução

1. Carregar `figma:figma-use` e `figma:figma-code-connect`
2. Listar todos os COMPONENT_SET publicados via MCP
3. Identificar correspondências no codebase
4. Apresentar mapeamento proposto ao usuário
5. Aguardar aprovação do mapeamento
6. Para cada componente aprovado:
   a. Mapear variant properties → props
   b. Registrar via `add_code_connect_map`
   c. Verificar no Inspect
   d. Screenshot de confirmação
   e. Registrar em change-log.md
7. Relatório final: quantos mapeados, quais ficaram sem correspondência no código

---

## Componentes sem correspondência no código

Se um componente Figma não tem equivalente no codebase:
- Documentar em `harness/reports/code-connect.md` na seção "Sem correspondência"
- Sugerir nome e estrutura para o componente de código
- Não bloquear o fluxo — é informação para o time de dev

---

## Formato do relatório

```markdown
# Code Connect Report

## Mapeamentos registrados

| Componente Figma | Componente de código | Arquivo | Status |
|---|---|---|---|
| Button | <Button /> | src/components/Button.tsx | ✅ Mapeado |
| Input | <Input /> | src/components/Input.tsx | ✅ Mapeado |
| Card | — | — | ⚠️ Sem correspondência |

## Mapeamentos de props

### Button
| Figma property | Code prop | Valores |
|---|---|---|
| Type = Primary | variant="primary" | — |
| Type = Destructive | variant="destructive" | — |
| State = Disabled | disabled={true} | — |
| Label (text) | children | string |
| Show Leading Icon (boolean) | leadingIcon | ReactNode |

(repetir para cada componente)

## Sem correspondência no código
(listar componentes Figma sem par no codebase + sugestão de implementação)

## Próximos passos
(o que o time de dev precisa criar para completar o mapeamento)
```

## Entrega
Salvar em harness/reports/code-connect.md
Atualizar state.yaml com code_connect: completed
