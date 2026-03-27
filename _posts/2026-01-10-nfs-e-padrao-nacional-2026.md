---
layout: post
title: "NFS-e Padrão Nacional: o que mudou em 2026 e o impacto no ERP"
date: 2026-01-10
categoria: Fiscal
tags: [NFS-e, Fiscal, Protheus, IBS, CBS]
resumo: "Desde janeiro de 2026 a NFS-e nacional é obrigatória via LC 214/2025. Entenda os novos campos de IBS/CBS e como atualizar os parâmetros no Protheus."
---

Desde **1º de janeiro de 2026**, a NFS-e em padrão nacional passou a ser obrigatória para todos os municípios brasileiros, conforme a **Lei Complementar nº 214/2025**. Quem trabalha com ERP precisou agir rápido.

## Por que o padrão mudou?

Historicamente, cada município tinha seu próprio layout. A reforma tributária aproveitou para **unificar o modelo em nível nacional**, facilitando a fiscalização e preparando o terreno para os novos tributos IBS e CBS.

> **Atenção:** municípios que não aderirem ao padrão nacional até jan/2026 perdem transferências voluntárias da União.

## O que muda na nota fiscal?

- Layout padronizado em todo o território nacional
- Novos campos para **IBS** (Imposto sobre Bens e Serviços) e **CBS** (Contribuição sobre Bens e Serviços)
- Integração ao Ambiente de Dados Nacional (ADN)
- Para Simples Nacional e MEI: mudança técnica em 2026; impacto tributário só a partir de 2027

## Impacto no Protheus

No Protheus, a transição exige atualização dos parâmetros de emissão de NFS-e e, dependendo do município, mudança no webservice utilizado. Os campos de IBS e CBS precisam estar mapeados no dicionário de dados e nas configurações do módulo fiscal.

O ponto mais crítico é a **Nota Técnica nº 004**, que atualizou o layout da DPS (Declaração de Prestação de Serviços). A NT 005, publicada em novembro de 2025, traz mais mudanças com entrada em vigor futura.

## O que eu fiz na prática

O processo envolveu verificar o município de emissão, confirmar a adesão da prefeitura ao modelo nacional, atualizar os parâmetros do TSS e validar a emissão em ambiente de homologação antes de ir para produção.
