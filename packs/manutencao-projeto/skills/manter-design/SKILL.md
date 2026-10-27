---
name: manter-design
description: Mantém o design system verdadeiro — tokens, componentes base, estados e padrões visuais. Use quando token, componente, tema ou layout base mudar, ou quando uma tela nova precisar seguir o padrão existente.
---

# Manter design

Documento alvo: `docs/DESIGN.md`. Se o projeto tiver um arquivo de tokens, ele continua sendo a fonte; o documento aponta para lá.

## O que o DESIGN.md precisa ter

1. Tokens reais: cor, espaçamento, raio, tipografia, com os valores que estão no código.
2. Componentes base: nome, caminho, variantes, estados (`hover`, `focus`, `disabled`, `loading`, `empty`, `error`).
3. Padrões de layout: largura de conteúdo, breakpoints, comportamento mobile.
4. O que é proibido: cor solta no componente, `!important`, estilo inline para layout.

## Verificação

```bash
grep -rn "\-\-[a-z-]*:" src/*.css src/**/*.css 2>/dev/null | head -40
cat tailwind.config.* 2>/dev/null | head -60
ls src/components 2>/dev/null
```

Valor no documento que não existe no token ou no componente é `DIVERGE`.

## Componente sem estado documentado

Estado que não está no documento é o que quebra na mão do usuário: botão sem `disabled`, lista sem `empty`, formulário sem `error`. Se o componente não implementa o estado, registre como lacuna em vez de descrever o que deveria ser.

## Não faça

- Não invente token que o projeto não tem.
- Não descreva tela inteira; descreva padrão.
- Não troque valor no documento para "ficar bonito"; o código manda.
