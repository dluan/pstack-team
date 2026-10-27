# Workflow por ciclo de vida

O time é organizado por etapa, não por cargo. Cada etapa tem um artefato e um portão.

## Matriz de etapas

| Etapa | Sub-fluxo | Skills | Onde vem |
| --- | --- | --- | --- |
| Plan | how → why, quando o risco pede | `how`, `why` | pstack |
| Plan | figure-it-out → show-me-your-work | `figure-it-out`, `show-me-your-work` | pstack |
| Design | architect → arena → interrogate | `architect`, `arena`, `interrogate` | pstack |
| Build | tdd → typescript-best-practices | `tdd`, `typescript-best-practices` | pstack |
| Build | deslop → no-comments | `deslop`, `no-comments` | cursor-team-kit |
| Test | create-verification-skill → swarm | `create-verification-skill`, `swarm` | pstack |
| Test | blast-radius e benchmark-checklist | `blast-radius`, `benchmark-checklist` | pstack |
| Test | interrogate e thermo-nuclear | `interrogate`, `thermo-nuclear-code-quality-review` | pstack / cursor-team-kit |
| Deploy | PR, CI, conflito e review | `make-pr-easy-to-review`, `fix-ci`, `loop-on-ci`, `get-pr-comments`, `fix-merge-conflicts` | cursor-team-kit |
| Deploy | babysit | playbook do `poteto-mode` | pstack |
| Maintain | contexto, produto, testes, navegação, design | `manutencao-projeto` (5 skills) | este repo |

As setas são encadeamentos possíveis, não uma ordem fixa. O dono da etapa escolhe a lente pelo tipo de mudança.

## Build: construir e limpar

As duas linhas de Build são sequenciais:

1. `tdd` e `typescript-best-practices` constroem o diff.
2. `deslop` limpa o código: comentário que narra, guarda defensiva fora do caminho confiável, cast para `any` e código morto.
3. `no-comments` entrega os comentários a um revisor que não os escreveu. No OpenBot, use `general` com `roles/comment-sicko-subagente.md`.
4. `unslop` limpa o texto do PR e da mensagem de commit, não o código.

O que pode rodar em paralelo são fatias independentes de Build, cada uma no seu worktree.

## Test: cobertura e lentes

- `create-verification-skill` cria a skill `verify-<app>`; sem ela, não há prova de superfície.
- `swarm` divide uma passada completa pelas features do mapa, com SHA e método por worker.
- `blast-radius` procura o que quebra fora do diff e prova o fato único que torna a mudança segura.
- `benchmark-checklist` veta qualquer número de performance antes de reportar.
- `interrogate` é pressão adversarial multi-modelo.
- `thermo-nuclear-code-quality-review` é revisão estrutural dura: code judo, arquivo passando de 1k, spaghetti.

## Deploy: até merge-ready

O Entregador abre o PR depois do PASS, sem pedir permissão. O veredito do diff é de um subagente em contexto novo, com `roles/revisor-subagente.md`.

`babysit` é playbook, não skill: leva um PR ou pilha até merge-ready, em modos `drive`, `background`, `threads-only` ou `check`. Merge é `shipping`, e só com pedido explícito do usuário.

## Maintain: documentos vivos

| Skill | Documento | Gatilho |
| --- | --- | --- |
| `manter-contexto` | `AGENTS.md`: stack, comandos, arquitetura, limites | pasta ou comando muda |
| `manter-produto` | regras de produto e ADRs | decisão de produto tomada |
| `manter-testes` | pirâmide, como rodar, cobertura e lacunas | suíte muda |
| `manter-navegacao` | telas, rotas e jornadas | rota ou tela muda |
| `manter-design` | design system, tokens, componentes | componente ou token muda |

Contrato comum: só atualiza o que mudou, cita `arquivo:linha`, carimba data e commit, e falha alto quando o documento contradiz o código.

## O que não é portão

`teach` é comunicação, não etapa. Use quando o usuário quiser entender uma mudança, não como checklist de Plan.
