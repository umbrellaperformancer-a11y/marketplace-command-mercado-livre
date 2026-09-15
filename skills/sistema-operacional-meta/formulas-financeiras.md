# FÓRMULAS FINANCEIRAS — META ADS PERFORMANCE OS · v2.1

Convenção: **líquido** = como aparece no Ads Manager (sem imposto). **bruto** = o que sai do caixa. `t` = `imposto_midia_pct` da config (referência BR 2026: PIS/COFINS 9,25% + ISS municipal 2–5% ≈ 12,15% em SP — conferir na fatura). `f` = fator de segurança configurável (padrão 0,90).

## 1. Gasto
- `spend_bruto = spend_liquido × (1 + t)`
- `cpa_bruto = spend_bruto ÷ conversões` = `cpa_liquido × (1 + t)`
- `roas_bruto_equivalente = roas_ads_manager ÷ (1 + t)`

## 2. Margem de contribuição (por pedido, SKU, campanha ou período)
`MC = RECEITA − CMV − IMPOSTOS_SOBRE_VENDA − TAXAS(gateway/plataforma) − FRETE/SUBSÍDIO − DESCONTOS − DEVOLUÇÕES − MÍDIA_BRUTA`
- `margem_pre_midia = (RECEITA − CMV − IMPOSTOS − TAXAS − FRETE − DESCONTOS − DEVOLUÇÕES) ÷ RECEITA`
- `margem_pos_midia = MC ÷ RECEITA`
- `lucro_pos_midia = MC` (absoluto)

## 3. Pisos e tetos
- `CPA_max_bruto = AOV × margem_pre_midia` (para lucro zero na 1ª compra); com LTV: `CPA_max_bruto = AOV × margem_pre_midia + (LTV_incremental × margem_pre_midia × fator_LTV_configurável)`
- `ROAS_breakeven_bruto = 1 ÷ margem_pre_midia`
- `ROAS_alvo_bruto = 1 ÷ (margem_pre_midia − margem_alvo)`
- `orcamento_sustentavel_dia = caixa_disponivel_para_midia ÷ dias_do_ciclo`, limitado por `DOH` (estoque) e capacidade operacional

## 4. Conversão para parâmetros da Meta (SEMPRE em líquido)
- `Cost_Cap_Meta = (CPA_max_bruto ÷ (1 + t)) × f`
- `Min_ROAS_Meta = ROAS_breakeven_bruto × (1 + t) ÷ f` (ou `ROAS_alvo_bruto × (1 + t)`)
- `Bid_Cap_Meta` (quando usado) `= Cost_Cap_Meta × (1 + folga_leilão_configurável)`
Errar essa conversão coloca o cost cap ~t acima do que a margem suporta. Sempre exibir os dois números lado a lado.

## 5. Eficiência de canal
- `MER = receita_total_periodo ÷ spend_bruto_total`
- `CAC = spend_bruto_aquisicao ÷ novos_clientes`
- `payback_meses = CAC ÷ (MC_media_por_cliente_por_mes)`
- `LTV = AOV × margem_pre_midia × compras_por_cliente_no_horizonte`

## 6. Estoque
- `venda_media_dia = unidades_vendidas_30d ÷ 30` (ou janela configurável)
- `DOH = estoque_disponivel ÷ venda_media_dia`
- `DOH_pos_escala = estoque_disponivel ÷ (venda_media_dia × (1 + incremento_projetado))` — se `< lead_time_reposicao + margem_dias` → alerta 🟡, bloqueio de escala se `< lead_time`.

## 7. Fadiga (sinais)
- `cpm_por_alcance = spend ÷ reach × 1000` — alta sustentada = sinal primário
- `razao_1d7d = purchase_1d_click ÷ purchase_7d_click` — caindo = fadiga formando
- `queda_ctr = (ctr_hoje − ctr_media_7d) ÷ ctr_media_7d` — direcional por N dias

## 8. Regras de uso
1. Toda fórmula usada cita este arquivo e a seção no `lineage`.
2. Componente AUSENTE → resultado ESTIMADO ou AUSENTE, nunca CONFIRMADO.
3. Receita Meta e receita ERP nunca entram na mesma soma.
4. Regime tributário (Simples/Presumido/Real) e crédito de PIS/COFINS: registrar como `PENDENTE_CONFIGURACAO` e apontar ao contador — o cérebro não decide crédito tributário.
