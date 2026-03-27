---
layout: post
title: "Como usar o APSDU para auditar dados no Protheus sem quebrar nada"
date: 2026-02-05
categoria: SQL
tags: [SQL, APSDU, Protheus, Auditoria]
resumo: "O APSDU é poderoso e pouco documentado. Mosro como usá-lo com segurança: consultas, validação de saldos e os erros que você precisa evitar."
---

O **APSDU** (Advanced Protheus System Data Utility) é a ferramenta de manipulação direta de dados do Protheus. É poderosa, pouco documentada e, se usada errado, pode causar danos sérios na base.

## Quando usar o APSDU?

- Conferir dados diretamente nas tabelas sem passar pela interface
- Validar inconsistências entre tabelas (ex: SB2 x SD3)
- Auditar registros excluídos ou modificados
- Corrigir dados em cenários autorizados pelo consultor TOTVS

> **Importante:** a TOTVS não presta suporte para manipulação direta no banco. Toda alteração via APSDU é de responsabilidade do analista. Nunca altere em produção sem backup.

## Consultando saldo de estoque (SB2)

```sql
SELECT B2_FILIAL, B2_COD, B2_LOCAL, B2_QATU, B2_CM1
FROM SB2010
WHERE B2_FILIAL = '01'
  AND B2_COD = 'PROD001'
  AND D_E_L_E_T_ = ' '
ORDER BY B2_LOCAL
```

## Cruzando SB2 com SD3 (movimentos)

```sql
SELECT D3_COD, D3_TM, D3_DOC, D3_QUANT, D3_EMISSAO
FROM SD3010
WHERE D3_FILIAL = '01'
  AND D3_COD = 'PROD001'
  AND D3_EMISSAO >= '20260101'
  AND D_E_L_E_T_ = ' '
ORDER BY D3_EMISSAO DESC
```

## Dica de ouro: sempre filtre o D_E_L_E_T_

No Protheus, registros excluídos **não saem fisicamente da tabela** — eles recebem o caractere `*` no campo **D_E_L_E_T_**. Se você esquecer esse filtro, seus resultados vão incluir dados que o sistema considera deletados, gerando confusão na análise.
