---
name: fluxo-dev
description: Fluxo de uma tarefa de dev no time pstack do OpenBot. Portões, artefato de saída de cada etapa, o que abre sozinho e o que espera o usuário. Use ao receber um pedido de dev, ao entrar em qualquer etapa, ou quando estiver em dúvida se pode seguir sozinho ou precisa perguntar.
---

# Fluxo de uma tarefa

Uma tarefa por vez, na ordem dos portões. Cada portão entrega um artefato. Sem o artefato, a etapa seguinte não começa.

| # | Etapa | Dono | Artefato | Segue quando |
| --- | --- | --- | --- | --- |
| 1 | Plan | Planejador | `docs/pstack/plano-<slug>.md` com playbook, checklist, contrato e rota | o critério de pronto está escrito |
| 2 | Design | Planejador + subagente `architect` | tipos, assinaturas, fronteira de módulo e fora de escopo no plano | o bloco de Design existe |
| 3 | Build | Subagente de propósito geral do Planejador | código com teste vermelho antes; `deslop` no diff | build e suíte local verdes no worktree |
| 4 | Test | Testador | PASS ou FAIL na superfície real, com evidência em disco | PASS com caminho de evidência |
| 5 | Deploy | Entregador | PR, CI verde, veredito independente | APPROVE e pedido de merge |
| 6 | Maintain | Zelador | documento atualizado com carimbo de data e commit | documento cita `arquivo:linha` |

## Profundidade do Plan

Nem todo pedido paga `how` e `why`. Trivial e reversível: dispense com uma linha. Médio: `how` de uma fatia e `why` estreito, só git e GitHub. Alto, área nova ou regressão: `how` + `why`; o Design é obrigatório. `teach` não é portão; é explicação depois, quando o usuário pede.

## Limpeza do Build

`deslop` limpa o código do diff: comentário que narra, guarda defensiva fora do caminho confiável, cast para `any` e código morto. `no-comments` é um subagente separado, com `roles/comment-sicko-subagente.md`, chamado antes da revisão; o autor não revisa os próprios comentários. `unslop` é texto de PR e commit, não código.

## Abre sozinho, sem perguntar

- Branch, commit e worktree.
- Abrir o PR depois do PASS do Testador. Perguntar "posso abrir o PR?" é erro de processo.
- Chamar o veredito independente antes do merge.
- Chamar o Zelador quando a tarefa mudar pasta, comando, rota, componente ou regra.
- Pedir ADR ao Produto quando a mesma decisão aparecer duas vezes sem regra escrita.
- Investigação read-only quando falta fato para decidir.

## Espera o usuário

- Merge. Só no PR que ele pediu para landar.
- Deploy.
- Force-push em branch compartilhada.
- Apagar dado que não foi criado por você.
- Migration destrutiva.
- Mudança de escopo já aprovado.
- Gasto relevante.
- Mensagem para cliente.

## Nunca

- Perguntar permissão para ação reversível que o pedido já cobre.
- Começar Build sem o bloco de Design, ou pular etapa sem uma linha no plano dizendo por quê.
- Levar ao usuário uma escolha que o plano, o código ou um documento do repo já responde.
- Declarar pronto sem PASS na superfície real.
- Inventar comando, caminho, número ou estado de CI.

## Checklist da tarefa

Copie para o plano e marque conforme avança. Passo pulado fica com `skip: motivo`.

```
[ ] 1. pedido classificado e critério de pronto escrito
[ ] 2. playbook escolhido, passos copiados
[ ] 3. profundidade do Plan decidida: skip, how+why, ou how+why com Design obrigatório
[ ] 4. testes existentes listados; estender, substituir ou criar
[ ] 5. contrato de dados escrito, se as duas metades do Build rodam em paralelo
[ ] 6. bloco de Design: tipos, assinaturas, fronteira, fora de escopo
[ ] 7. commit das evidências definido
[ ] 8. teste vermelho antes da implementação
[ ] 9. build e suíte local verdes; deslop no diff
[ ] 10. PASS na superfície real, com evidência no disco
[ ] 11. PR aberto, veredito independente colado
[ ] 12. merge só com pedido do usuário
[ ] 13. documento atualizado e carimbado
[ ] 14. handoff escrito e novo chat iniciado, ou motivo para não iniciar
```

## Fecho da tarefa

Merge sozinho não fecha a tarefa. Fecha quando o Maintain termina ou é dispensado com motivo no plano.

Antes de limpar o chat, escreva o handoff no plano ou na evidência:

```
Estado: branch, worktree, PR
Feito: ...
Em voo: ...
Próximo: ...
Evidência: caminhos
```

Cada agente limpa o próprio chat no fim da própria parte. `start_new_chat` só vale para o próprio chat e só se a configuração permitir. Ninguém limpa o chat de outro.

Depois do Maintain, o Planejador avisa os envolvidos que a tarefa fechou. Quem tem PR, fila ou processo aberto ignora e limpa ao terminar. Nunca limpe com trabalho em voo.

## Quando travar

Falta um fato que só o usuário tem: pergunte uma vez, com opção concreta.
Falta um fato que está no repo ou numa ferramenta: procure antes de perguntar.
Duas fontes do repo se contradizem: `DIVERGE:`, com as duas fontes, e pare.
Etapa falhou duas vezes pelo mesmo motivo: volte ao Plan, não tente a terceira no escuro.
