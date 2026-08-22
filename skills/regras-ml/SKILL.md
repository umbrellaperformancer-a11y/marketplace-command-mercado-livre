---
name: regras-ml
description: Regras específicas do Mercado Livre para a sua loja . Use em qualquer tarefa de Mercado Livre — define os painéis da CENTRAL DE VENDEDORES (o painel novo do ML) e parâmetros padrão da operação. Identidade da loja (advertiserId, conta, vitrine) vem da config do projeto. Use APENAS para Mercado Livre — NÃO use para Shopee.
---

# 📙 REGRAS MERCADO LIVRE (todas as lojas ML do grupo)

> Identidade da loja ativa (nome, conta, advertiserId, vitrine, metas) vem da FICHA do projeto. Estas regras valem pra qualquer loja ML.

## 🗺️ A CENTRAL DE VENDEDORES (o painel do ML desde a atualização de 2026)
O ML unificou o painel do vendedor na **Central de Vendedores**: `https://vendedores.mercadolivre.com.br`
Acesso: menu do usuário no site → "Ir para Central de vendedores". Menu horizontal no topo: **Métricas · Publicidade · Vendas · Resumo** (+ busca por título/SKU/# e "Monitor ao vivo"). Menu completo na barra lateral esquerda (ícones).

### MAPA DOS PAINÉIS (caminhos após vendedores.mercadolivre.com.br)
| Função | Caminho | Quem usa |
|---|---|---|
| Resumo (pendências, reputação, Full, vendas 7d) | `/resumo` | Comitê (plano do dia) |
| Métricas do negócio (visão geral) | `/metricas/negocio/visao-geral` | BI, Comitê |
| Desempenho em envios | `/metricas/desempenho-em-envios` | Reputação, Full |
| Estoque Full (métricas) | `/metricas/stock-full` | Full, Estoque |
| Análise de mercado (concorrentes) | `/metricas/concorrentes` | Estoque (vigilância), Diretor Comercial |
| Minha página (métricas da vitrine) | `/metricas/minha-pagina` | Anúncios |
| Publicidade — Mercado Ads | `/publicidade/resumo-anunciante` | Ads |
| Vendas (lista omni) | `/vendas/omni/lista` | Atendimento, CRM, BI |
| Perguntas (pré-venda) | `/perguntas/vendedor` | Atendimento |
| Pós-venda (mensagens, reclamações) | `/post-purchase/post-sales` | Atendimento, Reputação, CRM |
| Gestão de anúncios | `/anuncios/lista` | Anúncios, Criador |
| Promoções | `/anuncios/lista/promos` | Promoções |
| Full — enviar mercadoria (remessas) | `/shipping/inbounds` | Full |
| Full — retiradas | `/fulfillment/withdrawals` | Full |
| Catálogo (sugestões/oportunidades) | `/catalogo/sugerencias` | Criador, Anúncios |
| Reputação | `/reputacao` | Reputação |
| Central de marketing | `/marketing/resumo` | Promoções, CRM |
| Canal de transmissão | `/marketing/canal-de-transmissao` | CRM |
| Clips (vídeos) | `/video/creator` | Diretor de Criativo |
| **Central de Afiliados** | `/seller-affiliates` | Promoções (módulo afiliados) |
| ├ Campanha com afiliados | `/seller-affiliates/campaign` | Promoções |
| ├ Campanhas exclusivas | `/seller-affiliates/target-campaign` | Promoções |
| ├ Métricas de afiliados | `/seller-affiliates/dashboard` | Promoções, BI |
| ├ Relatório de campanhas | `/seller-affiliates/orders` | Promoções, Financeiro |
| └ Mensagens com afiliados | `/seller-affiliates/chat` | Promoções (rascunho; envio só com aprovação) |
| Tarifas e pagamentos | `/billing/resume` | Financeiro |
| Emissor de NF-e | `/billing/invoiceissuer/fiscal-hub` | Financeiro |
| Minhas marcas (Brand Hub) | `/brand-hub` | Diretor Comercial |
| **Novidades (anúncios oficiais do ML)** | `/novidades` | Comitê/Radar (radar de mudanças) |
| Central de aprendizagem | `/aprender` | Suporte |
| Preferências de venda | `/preferencias-de-venda` | Setup |

### Regras de navegação na Central
- Sempre navegue pela URL direta do mapa acima (mais confiável que caçar menu).
- Caminho do mapa deu 404 ou tela diferente → o ML mudou DE NOVO: registre a URL nova que a tela abriu, avise o dono da loja ("⚠️ mudou o caminho X") e siga pelo menu lateral/busca.
- Páginas da Central carregam por JavaScript: espere o carregamento (2-3s) antes de ler; tela em branco → espere e tente 1x de novo.
- A busca do topo aceita título, SKU ou # do anúncio — atalho pra achar anúncio específico.
- O painel antigo (myaccount/summary etc.) NÃO existe mais — não tente os caminhos antigos.

## 💰 PARÂMETROS-PADRÃO DA OPERAÇÃO ML
- Margem líquida mínima: 30% no preço normal · piso absoluto em promoção: 5%
- Comissão: Clássico ~11-14% · Premium ~16-19% (12x sem juros) — **confirme a taxa real no painel de Tarifas (`/billing/resume`); se divergir, vale o painel**
- Custo fixo por unidade em itens < R$79 — confirme a faixa vigente no painel
- Frete grátis obrigatório ≥ R$79 (custo do vendedor, tabela por peso/reputação)
- Metas de Ads (ACOS/ROAS por objetivo): a tabela oficial vive no `agente-ads-ml` — fonte única
- Reputação: manter verde; as 3 métricas (reclamações, cancelamentos, atraso) no `playbook_platinum.md`

## 🏗️ MECÂNICAS PRÓPRIAS DO ML (resumo — detalhe nos playbooks)
- **Catálogo/Buy Box:** disputa por página única de produto → `playbook_buybox_catalogo.md` (Criador)
- **Full:** estoque no depósito do ML; remessas por `/shipping/inbounds` → `playbook_full_flex.md`
- **Flex:** entrega no mesmo dia pela sua operação → mesmo playbook
- **Tipos de anúncio:** Clássico vs Premium (exposição + parcelamento vs custo)
- **Afiliados:** Central própria (`/seller-affiliates`) — comissão extra pra atrair afiliados; módulo no `agente-promocoes-ml`
