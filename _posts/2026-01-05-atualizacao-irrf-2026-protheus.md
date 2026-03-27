---
layout: post
title: "Atualização de tabelas IRRF 2026 no Protheus: passo a passo"
date: 2026-01-05
categoria: Fiscal
tags: [IRRF, Fiscal, Protheus, SIGAGPE]
resumo: "Documentei o processo completo de atualização das tabelas IRRF no Protheus para nunca mais precisar pesquisar no suporte toda virada de ano."
---

Todo início de ano a Receita Federal publica a nova tabela do IRRF e quem trabalha com Protheus precisa atualizar os parâmetros antes de rodar a primeira folha.

## O que muda todo ano?

As **faixas de alíquotas** e os **valores de dedução por dependente** são atualizados anualmente. Se os parâmetros não forem atualizados, os cálculos de retenção ficam errados — gerando problemas trabalhistas e fiscais.

## Onde fica no Protheus?

1. Acesse **SIGAGPE → Atualizações → Definições de Cálculo → Tabelas de Impostos**
2. Localize a tabela de IRRF e verifique as faixas vigentes
3. Compare com os valores publicados pela Receita Federal para o ano corrente
4. Atualize os valores mantendo o histórico das tabelas anteriores

## Validação após atualização

Sempre faço um cálculo manual antes de liberar para produção. Pegue um colaborador com salário em cada faixa e confira se o IRRF calculado bate com o esperado segundo a tabela oficial da Receita.

> **Atenção:** se sua empresa usa o TSS para obrigações fiscais, verifique também a atualização de parâmetros nesse ambiente — a tabela pode precisar ser atualizada em mais de um lugar.

## Registre sempre quem fez e quando

Documente a data da atualização, a versão da tabela aplicada e quem executou. Isso é fundamental para auditoria e para rastrear divergências futuras.
