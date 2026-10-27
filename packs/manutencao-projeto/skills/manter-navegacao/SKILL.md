---
name: manter-navegacao
description: Mantém o mapa de navegação verdadeiro — telas, rotas, jornadas do usuário e estados vazios ou de erro. Use quando rota, tela, menu ou redirecionamento mudar, ou quando alguém perguntar onde fica determinada função no app.
---

# Manter navegação

Documento alvo: `docs/NAVEGACAO.md`.

## O que ele precisa ter

1. Tabela de rotas: caminho, tela, quem acessa (público, autenticado, dono), o que carrega.
2. Jornadas principais em passos numerados, da entrada ao resultado. Uma por parágrafo, não um fluxograma gigante.
3. Estados que quebram: vazio, erro, sem permissão, sessão expirada. Onde cada um aparece.
4. Redirects e rotas mortas que ainda existem.

## Verificação

```bash
grep -rn "path=\|router\|Route\|navigate(" src 2>/dev/null | head -40
grep -rn "\"/api/" server 2>/dev/null | head -20
```

Rota no documento que não aparece no código, ou rota no código que não aparece no documento, é `DIVERGE`.

## Jornada, não inventário

O documento serve para responder "onde o usuário faz X". Se uma jornada precisa de mais de oito passos, provavelmente são duas jornadas.

## Não faça

- Não documente componente; documente tela.
- Não descreva estilo visual aqui, isso é `manter-design`.
- Não copie screenshot sem caminho no repositório.
