---
layout: post
title: "5 queries SQL essenciais para analistas de Protheus"
date: 2026-03-01
categoria: SQL
tags: [SQL, SIGAEST, SIGAFIN, SIGACOM, Protheus]
resumo: "Saldo em estoque, pedidos em aberto, títulos vencidos — consultas que viraram rotina e economizam horas de trabalho manual."
---

Depois de anos rodando consultas no Protheus, algumas queries viraram padrão no meu dia a dia. Aqui estão as 5 que mais uso — comentadas e prontas para adaptar ao seu ambiente.

> **Lembrete:** os nomes de tabela variam por empresa/filial (ex: SB2010, SB2020...). Ajuste o sufixo para o seu ambiente.

## 1. Títulos em aberto no SIGAFIN (SE2)

```sql
SELECT E2_FILIAL, E2_FORNEC, E2_NUM, E2_VALOR,
       E2_VENCTO, E2_SALDO
FROM SE2010
WHERE E2_FILIAL = '01'
  AND E2_SALDO > 0
  AND E2_VENCTO <= CONVERT(VARCHAR,GETDATE(),112)
  AND D_E_L_E_T_ = ' '
ORDER BY E2_VENCTO
```

## 2. Pedidos de compra em aberto (SC7)

```sql
SELECT C7_NUM, C7_PRODUTO, C7_DESCRI,
       C7_QUANT, C7_QUJE,
       (C7_QUANT - C7_QUJE) AS SALDO_ABERTO
FROM SC7010
WHERE C7_FILIAL = '01'
  AND C7_QUANT > C7_QUJE
  AND D_E_L_E_T_ = ' '
ORDER BY C7_NUM
```

## 3. Saldo de estoque disponível (SB2 + SB1)

```sql
SELECT B2_COD, B1_DESC, B2_LOCAL,
       B2_QATU AS SALDO_FISICO,
       B2_RESERVA,
       (B2_QATU - B2_RESERVA) AS DISPONIVEL
FROM SB2010 SB2
JOIN SB1010 SB1 ON SB1.B1_COD = SB2.B2_COD
WHERE SB2.B2_FILIAL = '01'
  AND SB2.B2_QATU > 0
  AND SB2.D_E_L_E_T_ = ' '
  AND SB1.D_E_L_E_T_ = ' '
```

## 4. Notas de entrada recentes (SF1 + SD1)

```sql
SELECT F1_DOC, F1_FORNECE, F1_EMISSAO,
       D1_COD, D1_QUANT, D1_TOTAL
FROM SF1010 SF1
JOIN SD1010 SD1 ON SD1.D1_DOC = SF1.F1_DOC
  AND SD1.D1_FORNECE = SF1.F1_FORNECE
WHERE SF1.F1_FILIAL = '01'
  AND SF1.F1_EMISSAO >= '20260101'
  AND SF1.D_E_L_E_T_ = ' '
  AND SD1.D_E_L_E_T_ = ' '
ORDER BY SF1.F1_EMISSAO DESC
```

## 5. Detectar inconsistência de saldo (SB2 vs SD3)

```sql
SELECT SB2.B2_COD,
       SB2.B2_QATU AS SALDO_ATUAL,
       SUM(CASE WHEN D3_TP='E' THEN D3_QUANT
                WHEN D3_TP='S' THEN -D3_QUANT
                ELSE 0 END) AS SALDO_CALCULADO
FROM SB2010 SB2
LEFT JOIN SD3010 SD3 ON SD3.D3_COD = SB2.B2_COD
  AND SD3.D_E_L_E_T_ = ' '
WHERE SB2.B2_FILIAL = '01' AND SB2.D_E_L_E_T_ = ' '
GROUP BY SB2.B2_COD, SB2.B2_QATU
HAVING SB2.B2_QATU != SUM(CASE WHEN D3_TP='E' THEN D3_QUANT
  WHEN D3_TP='S' THEN -D3_QUANT ELSE 0 END)
```
