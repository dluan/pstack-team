---
name: manter-contexto
description: Mantém o AGENTS.md do repositório verdadeiro — stack, comandos, layout, limites e armadilhas. Use quando pasta de topo, comando, dependência ou serviço mudar, ou quando um agente novo precisar de contexto confiável do repo.
---

# Manter contexto

Documento alvo: `AGENTS.md` na raiz do repositório. É o primeiro arquivo que qualquer agente lê. Se estiver errado, todo trabalho começa errado.

## O que ele precisa responder

1. O que é este repositório e qual é a entrada de produção.
2. Como rodar: instalar, dev, build, typecheck, teste, banco, variáveis.
3. Como o código está organizado, no máximo dez linhas de layout.
4. O que não pode ser feito: arquivos proibidos, migrations manuais, deploy direto.
5. Armadilhas reais: porta ocupada, cache que mente, comando que parece funcionar e não cobre nada.

## Verificação

Rode, não confie na memória:

```bash
cat package.json | sed -n '/scripts/,/}/p'
ls -d */ .[a-z]*/ 2>/dev/null
cat docker-compose.yml 2>/dev/null | head -40
git log -1 --format='%h %s'
```

Cada comando listado no documento precisa existir no `package.json` ou no `Makefile`. Comando que não existe é `DIVERGE`.

## Atualização

Só mexa na seção afetada. Se uma seção não tem fonte, marque `NÃO VERIFICADO: <o que falta>` em vez de adivinhar.

Não escreva tutorial. O documento serve para decidir rápido, não para ensinar. Máximo aproximado de 120 linhas; acima disso, o excesso pertence a `docs/`.

## Não faça

- Não copie README inteiro para o AGENTS.md.
- Não liste toda dependência, só a que muda decisão.
- Não registre senha, token ou caminho absoluto de máquina pessoal.
