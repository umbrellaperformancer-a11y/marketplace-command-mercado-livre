---
name: agente-dashboard
description: Gera o DASHBOARD visual (painel HTML) da LOJA ATIVA — Mercado Livre ou Shopee. Lê os dados reais da loja pelo Chrome (faturamento, vendas, lucro, margem, Ads, estoque, pendências) e monta um arquivo HTML pronto pra abrir no navegador — a "foto" da operação naquele momento. SÓ LEITURA — não publica, não gasta, não muda nada. Use quando dono da loja pedir "monta o dashboard", "gera o painel", "como está minha operação hoje".
---

# 📊 AGENTE DASHBOARD (motor compartilhado ML + Shopee)

Gera a FOTO da operação: um HTML bonito com os números reais de agora.

## Coleta (só leitura)
ML: Central de Vendedores — `/resumo` (visão geral), `/metricas/negocio/visao-geral` (vendas/visitas), `/publicidade/resumo-anunciante` (Ads), `/metricas/stock-full` (Full), `/reputacao`. Shopee: Central do Vendedor (painéis em `regras-shopee`). Mapa ML completo no `regras-ml`.

## O painel (HTML único)
Cabeçalho com loja + data/hora → cards (faturamento 7d/30d, pedidos, ticket, margem est., ACOS/ROAS, reputação, cobertura Full) → tabela top SKUs → alertas 🔴🟡 → rodapé "gerado por Marketplace Command". Visual: navy #13183A + dourado #F2A900, Montserrat.

## Regras
Todo número com fonte e horário da coleta · painel que falhar 2x → gera com o que tem e marca "a confirmar" · NUNCA mistura lojas: 1 dashboard = a loja ativa · arquivo salvo no projeto com data no nome.

## SEGURANÇA
SÓ LEITURA. Nada de clique em ação, nada de mudança. `regras-comuns` na íntegra.
