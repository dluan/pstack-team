---
name: manutencao-projeto
description: Mantém os documentos vivos do projeto verdadeiros conforme o código cresce — contexto geral, produto, testes, navegação e design. Use quando código muda e um documento pode ter ficado para trás, quando pedirem auditoria de documentação, ou quando uma skill de etapa precisar do contexto do repositório.
---

# Manutenção do projeto

A etapa Maintain não tem skill no pack original. Estas cinco existem para que o conhecimento do repositório more em documento, e não na cabeça de um agente.

## Mapa dos documentos

| Skill | Documento padrão | Cobre |
| --- | --- | --- |
| `manter-contexto` | `AGENTS.md` | stack, comandos, layout, limites, armadilhas |
| `manter-produto` | `docs/PRODUTO.md` + `docs/adr/` | o que o produto é, regras, decisões e porquê |
| `manter-testes` | `docs/TESTES.md` | comando, camadas, contagem, lacunas |
| `manter-navegacao` | `docs/NAVEGACAO.md` | telas, rotas, jornadas, estados |
| `manter-design` | `docs/DESIGN.md` | tokens, componentes, padrões visuais |

Se o documento não existir, crie com o esqueleto mínimo da skill e diga que criou. Não crie os cinco de uma vez: só o que o pedido justifica.

## Contrato comum

Toda skill desta família obedece a seis regras.

1. **Verdade é afirmação verificável.** Cada linha do documento aponta para código, comando ou decisão registrada. O que não for verificável é marcado como intenção.
2. **Diff mínimo.** Atualize só o que mudou. Reescrever o documento inteiro apaga contexto que alguém escreveu de propósito.
3. **Origem citada.** Toda alteração leva a fonte no formato `arquivo:linha`, ou o comando e o resultado.
4. **Carimbo.** Termine com `<!-- atualizado em AAAA-MM-DD @ sha-curto -->`.
5. **Divergência explícita.** Se o documento afirma algo que o código desmente, não conserte em silêncio: registre `DIVERGE:` com o que o código diz e onde.
6. **Não inventar.** Sem acesso para verificar, escreva `NÃO VERIFICADO` e o comando que falta. Nunca preencha lacuna com suposição.

Se a correção exigir reescrever mais de um terço do documento, pare e proponha o novo texto antes de aplicar.

## Quando rodar

- Antes de abrir PR que muda estrutura, rota, regra ou token.
- Na auditoria semanal, procurando documento com carimbo velho.
- Quando um agente novo entra e precisa de contexto que não está em lugar nenhum.

## Saída

Uma linha por documento tocado: caminho, o que mudou, fonte. Depois, a lista de `DIVERGE` e `NÃO VERIFICADO` que sobraram, com o comando para fechar cada um.
