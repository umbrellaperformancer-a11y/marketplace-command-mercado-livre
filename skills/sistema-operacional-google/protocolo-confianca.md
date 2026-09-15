# PROTOCOLO DE CONFIANÇA · v2.0
Estados e efeitos: APROVADO decide · APROVADO_COM_RESSALVA decide declarando · DIVERGENTE não decide dinheiro · VENCIDO refaz leitura · INSUFICIENTE coleta mais · DECISAO_BLOQUEADA só o dono libera.
## Hierarquia de fontes
gasto: Ads (export CSV) > Ads (tela) > fatura (bruto real) · conversões atribuídas: Ads por fonte/janela · comportamento no site: GA4 · receita real: ERP/plataforma · custos: base_custos.md · feed/aprovação: Merchant · saúde: página de política/status. Export vence tela para número; tela vence para status.
## SLA de frescor (config)
Ads ≤24h (D+1) / ≤2h (intraday) · Merchant ≤24h · GA4 ≤24h · ERP ≤24h · custos ≤30d.
## Gatilhos automáticos de rebaixamento
conversões dentro de lag_dias usadas como definitivas → RESSALVA · tag Purchase sem disparo com tráfego → DIVERGENTE 🔴 · Google ≥2× ERP → DIVERGENTE 🔴 · divergência Google×GA4 > tolerancia_ga4 → DIVERGENTE (Tracking investiga; nunca "escolher" o certo arbitrariamente) · comparação com fonte/janela diferente → INSUFICIENTE · ERP > SLA → VENCIDO · campanha ativa sem impressões >6h → DIVERGENTE ⚫ · CID divergente → DECISAO_BLOQUEADA + PARA.
## Veto localizado
Bloqueia: escalar, subir budget, mudar tCPA/tROAS, criar campanha com lance automático sobre conversão suspeita. Não bloqueia: Merchant/feed, estrutura, naming, negativas óbvias de desperdício com amostra, criativos, auditoria.
## Natureza
CONFIRMADO · CALCULADO (fórmula) · ESTIMADO (premissa) · INFERIDO · AUSENTE (nunca preencher).
