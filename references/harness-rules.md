# Regras do Harness

## Modos de execução

### Read-only
Permitido: auditar, inventariar, criar plano, gerar relatório
Proibido: mover frames, criar páginas, alterar Auto Layout,
criar variables, criar componentes, renomear, excluir

### Write
Só ativar quando:
- plano aprovado existe
- escopo travado
- backup criado
- gate aprovado
- sem falha crítica

## Controle de escopo
Toda alteração fora de allowed_nodes = falha crítica imediata

## Gates
Uma fase só começa quando:
- fase anterior concluída
- critérios de saída atendidos
- relatório da etapa existe
- sem falha crítica
- usuário aprovou

## Backup obrigatório
- Antes de qualquer escrita
- Duplicar na página Archive
- Nomear: {nome} — Backup — {data}
- Registrar node_ids no state.yaml

## Rollback
Acionar quando:
- falha crítica detectada
- override perdido
- frame apagado acidentalmente
- protótipo quebrado
- alteração fora do escopo
