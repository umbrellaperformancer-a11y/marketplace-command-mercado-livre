# SCALE RULES — quando e como escalar · v2.1

Proibido: `ROAS > X → escala`. Escala só com o checklist inteiro verde. Valores entre `< >` vêm da config.

## CHECKLIST DE ELEGIBILIDADE (todos obrigatórios)
1. **PERFORMANCE:** roas_bruto_equivalente ≥ `<meta_roas_bruto>` ou cpa_bruto ≤ `<cpa_max_bruto>` por ≥ `<dias_estabilidade>` (referência 3–7) com conversões ≥ `<conv_min_escala>`.
2. **ESTABILIDADE:** fora da fase de aprendizado; nenhuma edição significativa dentro de `<janela_nao_edicao_dias>`; variação diária de CPA dentro de `<variacao_max_pct>`.
3. **MARGEM:** margem_pos_midia > 0 com dado APROVADO; Financeiro sem veto.
4. **ESTOQUE:** DOH_pos_escala ≥ lead_time + `<margem_dias>`; product set sem item zerado.
5. **CAIXA:** orçamento pós-escala (bruto) ≤ `<orcamento_mes_bruto>` restante e ≤ `<orcamento_sustentavel_dia>`.
6. **CRIATIVO:** estado ≠ FADIGANDO/SATURADO; CPM por alcance estável; ≥ `<criativos_min_ativos>` ativos ou pipeline pronto.
7. **SINAL:** EMQ Purchase ≥ `<emq_minimo>`, dedup na faixa, cobertura ≥ `<cobertura_min>`; Tracking sem veto.
8. **CONTA:** Account Quality sem restrição; limite de gasto da conta com folga ≥ escala planejada × 7 dias; Auditoria sem veto.
9. **OPERAÇÃO:** capacidade de despacho/atendimento para o volume projetado (dono confirma).

## ROTAS DE ESCALA
| rota | quando | como | reseta? |
|---|---|---|---|
| **Vertical (incremento)** | incremento desejado ≤ `<limite_orcamento_sem_reset_pct>` | subir orçamento no nível correto (campanha/CBO ou conjunto/ABO), 1× por `<cooldown_padrao_h>` | não (dentro do limite) |
| **Vertical (salto)** | incremento > limite | duplicar campanha/conjunto com o novo orçamento (nasce pausado), ativar com aprovação, manter original | novo objeto aprende do zero; original intacto |
| **Horizontal** | público/oferta/geo nova | novo conjunto/campanha com criativos vencedores | novo objeto |
| **Por criativo** | vencedor claro | levar vencedor para campanha de escala; nunca adicionar a conjunto estável (reseta) | depende |
| **Por produto / product set** | HERO com DOH ok | product set dedicado + verba própria | novo objeto |
| **Redistribuição** | um objeto sobra, outro falta | reduzir no perdedor (KR) e subir no vencedor dentro dos limites | conforme magnitude |

## RITMO
- 1 escala por objeto por `<cooldown_padrao_h>`; reavaliar em `<dias_estabilidade>` antes da próxima.
- Soma dos aumentos do dia ≤ `<aumento_max_dia_pct>` (matriz §4).
- Escala em Advantage+ Sales: preferir incremento no orçamento da campanha; a Meta faz o pacing.

## BLOQUEIOS AUTOMÁTICOS (Escala não propõe)
Veto ativo de Financeiro/Tracking/Auditoria · dado DIVERGENTE/VENCIDO/INSUFICIENTE · aprendizado em curso · restrição de conta · DOH insuficiente · orçamento bruto acima do sustentável · criativo em fadiga sem substituto.

## SAÍDA OBRIGATÓRIA
Pacote-padrão + plano: rota, objeto, nível, valor antes → depois (líquido e bruto), RESET_APRENDIZADO, DOH pós-escala, impacto esperado (receita e lucro bruto), risco, critério de reversão, NEXT_REVIEW.
