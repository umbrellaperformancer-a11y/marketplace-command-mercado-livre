---
name: regras-shopee
description: Regras específicas da Shopee para a sua loja. Use em qualquer tarefa de Shopee — define painéis da Central do Vendedor e as mecânicas próprias da Shopee (taxas por faixa, GMV Max, pontos de penalidade, SPX). Identidade da loja vem da config do projeto. Use APENAS para Shopee — NÃO use para Mercado Livre.
---

# 🟠 REGRAS — SHOPEE (motor compartilhado)

Valem para qualquer loja de Shopee do grupo. A identidade da loja (conta, nome, URL, concorrente, pastas, Chrome) vem da **config do projeto ativo**. As regras de aprovação, coleta via Chrome e diário estão em `regras-comuns`.

## PAINEL PRINCIPAL — CENTRAL DO VENDEDOR
Tudo na Shopee passa pela **Central do Vendedor** (seller.shopee.com.br). Áreas-chave:
- **Central de Marketing > Shopee Ads** — campanhas (GMV Max)
- **Marketing > Promoções / Ofertas / Vouchers / Combos** — promoções
- **Pedidos / Meus Produtos** — catálogo e vendas
- **Dados / Painel de Desempenho do Vendedor** — métricas e pontos de penalidade
- **Financeiro / Minha Carteira** — repasses e taxas
- **Envio (SPX / Shopee Envios)** — logística

## MECÂNICAS DA SHOPEE QUE TODO AGENTE PRECISA SABER

### Taxas (referência: março/2026 — a Shopee muda taxa com frequência)
> ⚠️ Em cálculo decisivo de margem, **confirme a taxa real do SKU na Central do Vendedor** (Meus Produtos / simulador de taxas). Se o painel divergir desta tabela, vale o painel.
- Comissão **variável por faixa de preço** (14% a 50%) + **tarifa fixa por item** (R$0 a R$26).
- Itens até R$79,99: **20%** (14% padrão + 6% Frete Grátis) + R$4 fixos.
- Itens < R$8: tarifa fixa = 50% do preço.
- **Programa de Frete Grátis obrigatório** (já embutido nos 6%).
- **Teto de R$100 removido** — produtos caros pagam comissão cheia.
- Campanha de Destaque: **+2,5%** durante o período.
- Cupom (via integração de frete): vendedor arca com **25%** do valor.
- **Subsídio PIX:** comprador vê "R$X no PIX", mas o valor cheio entra no repasse (Shopee subsidia).
- Comissão só é cobrada em **venda concluída** (cancelada/reembolsada não paga).
- CPF: > 450 pedidos em 90 dias = +R$3/item; faturamento anual ≥ R$81 mil → migrar pra CNPJ.

### Ads — GMV Max
- Modos: **GMV Max - Lance Automático** (novos produtos e campeões) e **GMV Max - Meta de ROAS** (produtos regulares).
- **Proteção de ROAS:** crédito grátis quando o ROAS real cai abaixo do alvo (só na Meta de ROAS, com conversão diária ≥ 5).
- ACOS = inverso do ROAS; ROAS-alvo definido por produto.

### Reputação — Pontos de Penalidade
- Cada infração vale uma pontuação; **acumula por semana**, validade **60 dias**.
- Sanções **progressivas e automáticas** por faixa: restrição de funcionalidades → suspensão/congelamento.
- Infrações comuns: cancelamento pelo vendedor, atraso de envio, produto fora de estoque, descrição incorreta, falsificado, atendimento ruim.
- Acompanhar no **Painel de Desempenho do Vendedor**; dá pra **apelar** com provas (ID do pedido, prints).

### Logística — SPX / Shopee Envios
- Programa de envio da Shopee (SPX). Prazo de despacho conta pontos se estourar.
- **Devolução Fácil:** R$0,49/pedido e a Shopee assume fretes de devolução.

## CONTEXTO QUE VEM DA CONFIG DO PROJETO (não fixar aqui)
Loja · conta Shopee · URL da loja · concorrente · nº de SKUs · CPF/CNPJ · pastas de saída · Chrome (deviceId).
