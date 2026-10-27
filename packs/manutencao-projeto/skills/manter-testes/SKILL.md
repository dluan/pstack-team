---
name: manter-testes
description: Mantém o mapa da suíte verdadeiro — como rodar, quantos testes existem por camada, o que está coberto e quais lacunas são conhecidas. Use quando teste, script ou cobertura mudar, ou antes de prometer que algo está provado.
---

# Manter testes

Documento alvo: `docs/TESTES.md`.

## Por que existe

Suíte verde que testa a coisa errada é pior que suíte ausente. O mapa precisa dizer o que cada comando realmente cobre, não o que se gostaria que cobrisse.

## O que o TESTES.md precisa ter

1. Comando por camada, com o que ele toca e o que ele **não** toca.
2. Contagem atual por camada e tempo aproximado, medidos nesta máquina.
3. Cobertura do que importa: qual arquivo de produção não tem teste nenhum.
4. Lacunas conhecidas, cada uma com `arquivo:linha`.
5. Testes que não provam nada, com o motivo: asserção em mecanismo morto, cópia de constante, cor literal.

## Verificação

Execute e conte:

```bash
npm run test:proxy 2>/dev/null | tail -20
npx playwright test --list 2>/dev/null | tail -5
find . -name "*.test.*" -o -name "*.spec.*" | grep -v node_modules | wc -l
```

Meça o tempo com `time`. Número não medido é `NÃO VERIFICADO`.

## Teste de mentira

Marque como lacuna, não como cobertura, quando a asserção:

- verifica `localStorage` nulo em app que não usa `localStorage`;
- compara o código com a própria constante importada dele;
- depende de cor, texto de ícone ou ordem de DOM sem relação com comportamento;
- testa um servidor que não é o de produção.

## Não faça

- Não conte teste de fixture como cobertura do app.
- Não escreva que "está coberto" sem nomear o arquivo de teste.
- Não proponha aumentar contagem; proponha fechar lacuna.
