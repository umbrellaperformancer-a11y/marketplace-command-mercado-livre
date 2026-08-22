---
name: regras-tiktok
description: Regras específicas do TikTok Shop para as lojas do grupo. Use em qualquer tarefa de TikTok Shop — define os painéis (Central do Vendedor, TikTok Ads Manager, Central de Negócios) e as mecânicas próprias do TikTok (comissão + tarifa fixa, GMV Max obrigatório, Shop Health/pontos de violação, logística, repasse, afiliados, DNA operacional). Identidade da loja vem da config do projeto. Use APENAS para TikTok Shop — NÃO use para Mercado Livre nem Shopee.
---

# ▶️ REGRAS — TIKTOK SHOP (motor compartilhado)

Valem para qualquer loja de TikTok Shop do grupo. A identidade da loja (conta, nome, @, URL, concorrente, advertiser/ad account, pastas, Chrome) vem da **config do projeto ativo**. As regras de aprovação, coleta via Chrome e diário de bordo estão em `regras-comuns`. A arquitetura do cérebro (hierarquia, protocolos, criticidade, auditoria, memória, aprendizado) está no KERNEL `sistema-operacional-tiktok` — todo agente `agente-*-tiktok` herda o kernel + estas regras.

> ⚠️ As taxas e regras do TikTok Shop mudam com frequência (campanhas, incentivos, programa de frete). **Sempre confira o número real na Central do Vendedor antes de fechar preço/margem.** Os valores abaixo são a referência de 2026 — quando a tela divergir, a tela vence e o Financeiro recalcula.

## 🧠 A LÓGICA DO TIKTOK É DIFERENTE (descoberta, não busca)
No ML/Shopee o cliente **busca** o produto. No TikTok **o produto encontra o cliente** — via vídeo curto, LIVE e a vitrine do perfil. Por isso o motor de crescimento aqui é **conteúdo + creators + afiliados + GMV Max**, não só SEO de busca. Isso muda a prioridade de todos os agentes: criativo e creators puxam tráfego; ficha/SEO e logística sustentam a conversão e a reputação.

## PAINÉIS PRINCIPAIS
- **Central do Vendedor** (`seller-br.tiktok.com`) — produtos, pedidos, promoções, afiliados, finanças, envio e **Shop Health (Saúde da Loja)**.
- **TikTok Ads Manager** (`ads.tiktok.com`) — campanhas (GMV Max de Produto e de LIVE).
- **Central de Negócios / Business Center** — vincula contas TikTok ↔ contas de anúncios ↔ loja; autorizações de GMV Max e de afiliados.
- Áreas-chave na Central do Vendedor: **Produtos** · **Pedidos** · **Promoções (cupons/ofertas/combos)** · **Afiliados (Programa do Vendedor)** · **LIVE & Vídeo / Conteúdo** · **Finanças / Carteira** · **Envio** · **Shop Health / Dados**.

## CADASTRO E FISCAL
- **CNPJ obrigatório** (MEI, EI, SLU, LTDA, etc.). **CPF não vende** no TikTok Shop Brasil.
- **NF-e por pedido** é obrigatória (e CT-e/MDF-e no transporte). Faturamento do TikTok é cruzado com a Receita.

## TAXAS (referência 2026 — confirmar na Central do Vendedor)
- **Comissão = (Preço do produto − descontos do vendedor) × 6%.**
- **Tarifa fixa por item** vendido (relatos de **R$2 a R$4** por item em 2026; mudou/dobrou no início do ano e pode variar por faixa/programa). **Tratar como item de conferência no painel**, não como constante.
- **Programa de Taxas de Envio / subsídio de frete:** para o cliente ver "frete grátis"/cupom de frete (forte gancho de conversão), o vendedor paga uma **taxa de serviço de frete**. O frete é **custo compartilhado** — entender a parcela do vendedor.
- **Incentivo a novos vendedores:** isenção de comissão por até **~90 dias** (cumprindo missões) + frete grátis. É temporário — não embutir no preço-base.
- Comissão incide sobre venda concluída (cancelada/reembolsada não paga).

## REPASSE (ciclo de pagamento)
- O prazo começa na **confirmação da entrega**. Há **liquidação de ~7 dias corridos** (janela de disputa/devolução) → saldo disponível por volta do **8º dia (D+7)**.
- **1 saque grátis por semana**; saques extras podem ter tarifa.

## ADS — GMV MAX (obrigatório)
- Desde **set/2025**, **GMV Max é o único tipo de campanha de Shop Ads** (substituiu Video Shopping Ads, Product Shopping Ads e LIVE Shopping Ads no fluxo padrão). IA automatiza **lance, criativo, segmentação e posicionamento**.
- Dois tipos: **GMV Max de Produto** (ROI total do canal, fora da LIVE) e **GMV Max de LIVE** (receita da sala da LIVE).
- O vendedor define **Meta de ROI/ROAS + orçamento diário**; o sistema otimiza. Usa **vídeos próprios + listings + vídeos de afiliados** como criativo.
- Atribuição: pedidos de **orgânico + pago + afiliado** são atribuídos ao GMV Max no painel da Central do Vendedor (atribuição de 1 dia para o produto).
- **1 conta de anúncios principal por loja**. Ligar GMV Max de LIVE pausa LIVE Shopping Ads antigos; ligar GMV Max de Produto pausa VSA/PSA dos mesmos produtos.

## AFILIADOS (Programa de Afiliados do Vendedor)
- O vendedor **define a comissão de afiliado** (% por produto ou para a loja). Faixas comuns no mercado: **8%–15%** (chega a 5%–20% em produtos agressivos).
- Dois modelos: **Colaboração Aberta** (qualquer creator pega o produto) e **Colaboração Direcionada** (convida creators específicos).
- A comissão de afiliado é **custo variável que entra na margem** — pode derrubar o lucro rápido. Sempre validar com `agente-financeiro-tiktok`.

## LOGÍSTICA (Brasil)
- **FBT (Fulfilled by TikTok) ainda NÃO está disponível no Brasil** (existe nos EUA/UK). A operação física é do vendedor/parceiro.
- Modos: **Envio pelo Vendedor** (Correios/transportadora/SuperFrete, etiqueta própria) e **Envio pelo TikTok/parceiros** (coleta no vendedor + entrega via transportadora). Pickup/dropoff disponíveis.
- Métricas que o algoritmo vigia: **prazo de despacho**, **taxa de envio no prazo**, **taxa de cancelamento**, **reclamações de entrega** — afetam diretamente o alcance orgânico no feed.
- Prazo de entrega padrão tende a **até ~15 dias**; despacho rápido é exigência, não diferencial.

## REPUTAÇÃO — SHOP HEALTH / PONTOS DE VIOLAÇÃO
- Painel: **Central do Vendedor > Shop Health (Saúde da Loja)** → aba **Registros de violação** → **Recurso** para apelar (resposta ~3 dias úteis).
- Moderação por **IA + revisão humana**. Cada infração soma **pontos de violação**; o acúmulo dispara **sanções progressivas**: advertência → restrição → bloqueio de vendas / limitação de anúncios → **suspensão temporária → banimento permanente**.
- Violações comuns: produto **falsificado/IP**, **alegações enganosas** (cura, efeito exagerado), produto **proibido/restrito**, **atraso/cancelamento**, divergência entre vídeo/anúncio e produto. (Atenção: creators levam ponto por produto de loja falsificado — vigiar o que se promove.)

## 🧬 DNA OPERACIONAL (metas do grupo no TikTok — guardadas pelo Orquestrador)
- **Ruptura ≤ 2%** · **Resposta ao cliente < 1h** · **Avaliação > 4.8** · **Cancelamento < 2%** · **Despacho < 24h**.
- Jamais permitir: ruptura, atraso, reclamação, queda de reputação, falta de campanha, **LIVE sem estoque**, anúncio sem criativo.

## POLÍTICA DE MARGEM
Vale o piso do grupo (`regras-comuns`): **mínimo 30%** no normal/Ads, base **40%**, promoção é exceção (barra só < 5%). **No TikTok, a comissão de afiliado entra na conta da margem** junto com 6% + tarifa fixa + frete + imposto + Ads.

## CONTEXTO QUE VEM DA CONFIG DO PROJETO (não fixar aqui)
Loja · conta/@ TikTok · URL · concorrente · advertiser/ad account · nº de SKUs · CNPJ · pastas de saída · Chrome (deviceId).
