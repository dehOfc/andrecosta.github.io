---
layout: post
title: "Novo Fluxo de Compras (NFC) no Protheus: o que mudou e como se adaptar"
date: 2026-03-15
categoria: ERP
tags: [Protheus, SIGACOM, PO-UI, NFC]
resumo: "A TOTVS descontinuou MATA131, MATA150, MATA160 e MATA161 a partir da release 12.1.2410. Entenda o NFC (PGCA010) com PO-UI e como documentar o processo para guiar sua equipe."
---

Se você trabalha com o módulo de Compras no Protheus, já deve ter se deparado com a migração para o **Novo Fluxo de Compras (NFC)**, acessado pela rotina **PGCA010** com interface PO-UI. Neste artigo, explico o que mudou, o que foi descontinuado e como documentei esse processo na prática.

## O que foi descontinuado?

A TOTVS comunicou a descontinuação das seguintes rotinas a partir da release **12.1.2410**:

- **MATA131** — Geração de Cotação
- **MATA150** — Atualização da Cotação
- **MATA160 / MATA161** — Análise da Cotação

A partir da release 12.1.2510, essas rotinas simplesmente não estarão mais disponíveis. Quem ainda não migrou precisa correr.

## O que é o NFC (PGCA010)?

O NFC é o novo fluxo de compras baseado na interface **PO-UI**. Ele centraliza todo o processo de cotação em uma única tela, com envio de formulários por e-mail para fornecedores e workflow de aprovação integrado.

> **Pré-requisitos técnicos:** LIB do Framework ≥ 27/02/2023 · Pacote da Expedição Contínua do Compras · Atualização do dicionário de dados (UPDDISTR) · Rotina PGCA010 adicionada ao menu via SIGACFG.

## Fluxo básico do processo

1. Criação da Necessidade de Compra
2. Geração da Cotação no PGCA010
3. Envio automático de formulários para fornecedores por e-mail via Workflow
4. Retorno e análise das propostas na mesma tela
5. Geração do Pedido de Compra aprovado

## Ponto de atenção: TES no cadastro de produto

A TES (Tipo de Entrada e Saída) amarrada no cadastro de produto **não é preenchida automaticamente** no NFC em todos os cenários. Se isso acontecer, verifique o parâmetro e a configuração do produto antes de acionar o suporte.

## Como documentei para minha equipe

Criar um passo a passo com prints de cada etapa, indicando o que cada campo faz e os pontos de atenção, foi fundamental para que o time operacional conseguisse usar o NFC sem depender do TI a cada operação.
