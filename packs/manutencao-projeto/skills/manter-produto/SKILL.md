---
name: manter-produto
description: Mantém o registro do produto verdadeiro — o que ele é, para quem, quais regras são invioláveis e por que cada decisão foi tomada. Use quando uma regra muda, uma feature nova altera o domínio, ou um ADR novo precisa substituir um antigo.
---

# Manter produto

Documento alvo: `docs/PRODUTO.md` para o estado atual, `docs/adr/` para decisões datadas.

## Regra de ouro

**ADR não se corrige, se supersede.** Um ADR registra uma decisão que existiu. Se ela foi revertida, escreva um novo com número maior, citando o antigo como substituído. Apagar o texto falsifica o histórico e deixa o próximo agente sem saber por que o código está do jeito que está.

## O que o PRODUTO.md precisa ter

1. Uma frase sobre o que o app faz e para quem.
2. As regras de domínio que o código não pode violar, cada uma com `arquivo:linha` de onde ela vive.
3. O que está fora de escopo, com a mesma clareza.
4. Índice de ADRs: número, título, estado (`vigente` ou `substituído por NNNN`).

## Verificação

Procure a regra no código antes de afirmar que ela existe:

```bash
grep -rn "clamp\|limit\|invariant\|regra" src server 2>/dev/null | head -30
ls docs/adr/ 2>/dev/null
```

Afirmação de produto sem lastro em código, teste ou ADR é `DIVERGE`.

## Sinais de que este documento está velho

- Cita tela, rota ou campo que não existe mais.
- Descreve um banco ou lib que o `package.json` não tem.
- Tem ADR vigente que o código contradiz.

## Não faça

- Não descreva implementação; descreva regra.
- Não transforme o PRODUTO.md em backlog.
- Não marque decisão como vigente sem dizer onde ela é aplicada.
