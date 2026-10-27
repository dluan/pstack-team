# Mapa do time

## Organização no painel

```mermaid
flowchart TB
  subgraph EN["Engenharia"]
    PLA[Planejador<br/>Plan e rota]
    TES[Testador<br/>Test]
    ENT[Entregador<br/>Deploy]
    ZEL[Zelador<br/>Maintain]
  end
  subgraph PR["Produto"]
    PROD[Produto<br/>regras e ADR]
  end
  ARC["Arquivo<br/>papéis antigos<br/>apagar no painel"]
  style ARC stroke-dasharray: 5 5
```

O Build não aparece: é subagente. O Arquiteto, o Revisor independente e o Comment Sicko também são subagentes e não ocupam a sidebar.

## Fluxo por etapa

```mermaid
flowchart LR
  U[Pedido] --> PLA

  PLA --> DES["portão de Design<br/>subagente architect"]
  DES -->|contrato escrito| BLD["Build<br/>subagente general"]
  BLD --> TES
  TES -->|"FAIL + repro"| PLA
  TES -->|"PASS + evidência"| ENT
  ENT -->|"subagente<br/>contexto novo"| REV[revisor independente]
  REV -->|REQUEST CHANGES| PLA
  REV -->|APPROVE| ENT
  ENT -->|merge| MS[(origin/master)]
  MS --> ZEL
  ZEL -->|documento atualizado| PLA

  PLA <-->|regra| PROD
  ENT <-->|conflito semântico| PROD
```

## O que cada portão exige

| Etapa | Entrada | Saída | Quem barra |
| --- | --- | --- | --- |
| Plan | pedido classificado | `plano-<slug>.md` com playbook e rota | Planejador |
| Design | plano | tipos, assinaturas, fronteira, fora de escopo | Planejador |
| Build | bloco de Design | código com teste vermelho antes | Subagente do Planejador |
| Test | Build verde | PASS com evidência no disco | Testador |
| Deploy | PASS | PR verde e merge | Entregador + revisor |
| Maintain | merge | documento com carimbo | Zelador |

## Camada de disco

| Caminho | O que guarda |
| --- | --- |
| `PLANO.md` | fonte de verdade do time |
| `roles/` | rubricas dos agentes e briefs dos subagentes |
| `packs/fluxo-dev` | skill que operacionaliza o fluxo de uma tarefa |
| `packs/manutencao-projeto` | cinco skills de Maintain |
| `<repo>/docs/pstack/plano-*.md` | plano do Planejador |
| `<repo>/docs/pstack/evidencia/` | prova do Testador |

## Pontos de atenção

- Um agente persistente por etapa; o Build é sempre subagente.
- O revisor independente não é bot: é contexto novo.
- Merge só com pedido do usuário.
- Documento sem carimbo é documento sem confiança.
