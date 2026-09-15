# FÓRMULAS FINANCEIRAS · v2.0
`imposto_incluso` (config, conferido na fatura): se SIM, spend exibido já é bruto (t=0 nas conversões); se NÃO, spend_bruto = spend × (1+t). `f` = fator de segurança (config, padrão 0,90).
1. spend_bruto (acima) · cpa_bruto = spend_bruto ÷ conversões · roas_bruto_eq = valor_conv ÷ spend_bruto
2. MC = RECEITA − CMV − IMPOSTOS_VENDA − TAXAS − FRETE − DESCONTOS − DEVOLUÇÕES − MÍDIA_BRUTA · margem_pre/pos_midia
3. Pisos: CPA_max_bruto = AOV × margem_pre_midia (+ fator LTV configurável) · ROAS_be_bruto = 1 ÷ margem_pre_midia · ROAS_alvo = 1 ÷ (margem_pre − margem_alvo)
4. Conversão para o Google (parâmetros na moeda exibida): se imposto_incluso=SIM → tCPA = CPA_max_bruto × f; tROAS = ROAS_be_bruto ÷ f. Se NÃO → tCPA = (CPA_max_bruto ÷ (1+t)) × f; tROAS = ROAS_be_bruto × (1+t) ÷ f. Introdução: começar em `fator_introducao_meta` do histórico e apertar gradualmente — meta agressiva demais colapsa entrega.
5. MER = receita_total ÷ spend_bruto_total · CAC · LTV · payback
6. Estoque (quando informado): DOH = estoque ÷ venda_média_dia; DOH_pos_escala; bloqueio se < lead_time.
7. Regras: fórmula citada no lineage · componente AUSENTE → resultado ESTIMADO/AUSENTE · nunca somar Google + GA4 + ERP · regime tributário/crédito → PENDENTE + contador.
