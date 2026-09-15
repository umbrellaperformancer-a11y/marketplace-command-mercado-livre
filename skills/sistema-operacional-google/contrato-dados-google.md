# CONTRATO DE DADOS — GOOGLE ADS PERFORMANCE BRAIN · v2.0
Campo ausente = AUSENTE, nunca em branco.
## 1. IDENTIDADE
tenant_id · empresa_id · mcc_id (se houver) · **customer_id (CID — chave da trava)** · conta_nome · merchant_id · ga4_property_id · campanha_id/nome · grupo_id · anuncio_id/asset_id · asset_group (PMax) · keyword · match_type · termo · produto_id/item_id/sku · custom_label_0..4 · url_final
## 2. CONTEXTO
data_inicio/fim · timezone · currency · **fonte_conversao** (tag Google / GA4 importada / offline) · **janela e modelo de atribuição** · estrategia_lance (tCPA/tROAS/MaxConv/MaxValue/Manual) · meta_vigente (tCPA/tROAS) · **learning_status do lance** · last_change_at · status · tipo_campanha (Search/PMax/Shopping/DemandGen/Video/Display)
## 3. ENTREGA E CUSTO
budget_dia · spend (como exibido) · **imposto_incluso (sim/não/PENDENTE)** · imposto_pct · **spend_bruto** (= spend se incluso; senão spend × (1+t)) · impressões · **impression_share · search_lost_IS_budget · search_lost_IS_rank** · cliques · CTR · CPC · custo_por_conversão
## 4. CONVERSÃO (na data do clique — declarar maturação)
conversões · valor_conversão · CPA · ROAS · conversões_por_tempo_de_conversão (lag) · **maturado: sim/não** · conversões GA4 (purchase, add_to_cart, begin_checkout, view_item) · receita GA4 · pedidos_erp · receita_erp
## 5. NEGÓCIO
cmv · impostos_venda · taxas · frete · descontos · devoluções · margem_contribuicao · lucro_pos_midia · MER (= receita total ÷ spend_bruto) · AOV · CAC · LTV
## 6. SAÚDE
status_conta · política/suspensão · produtos aprovados/limitados/reprovados (Merchant) · taxa de aprovação do feed · consent mode / enhanced conversions status · auto_apply (ligado?) · optimization_score (informativo, nunca meta)
## 7. PROVENIÊNCIA
fonte (ads_tela/ads_export/merchant/ga4/erp/calculado) · natureza · extraido_em · freshness · confidence · lineage
## 8. NORMALIZAÇÃO
1. Mesma fonte de conversão e mesma janela em qualquer comparação. 2. Conversão dentro de `lag_dias` = imatura. 3. Google View, GA4 View e Business View nunca somadas; divergência Google×GA4 tem tolerância (config) e explicação (modelo, data do clique vs data da sessão, consent). 4. Google ≥ 2× ERP → DIVERGENTE + 🔴 Tracking. 5. Número calculado carrega fórmula (`formulas-financeiras.md`).
