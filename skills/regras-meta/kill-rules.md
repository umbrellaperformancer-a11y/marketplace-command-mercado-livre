# KILL RULES — quando um objeto vira candidato a pausa/redução · v2.1

Proibido: `ROAS < X → pausa`. Toda kill rule é **combinada**, com amostra, janela, tracking saudável e estado de aprendizado. Resultado é sempre **CANDIDATO** — a execução segue a matriz (N2 padrão; N3 só se liberado). Valores entre `< >` vêm da config.

## KR-1 · Anúncio sem conversão com gasto relevante
gasto_bruto ≥ `<amostra_min_kill>` (referência: ≥ 2× CPA_max_bruto) **E** conversões = 0 **E** dias ativos ≥ `<janela_min_kill_dias>` **E** tracking APROVADO **E** conjunto fora do aprendizado **E** dado maturado (D-1 não conta como definitivo) → CANDIDATO A PAUSA do anúncio. Se for o único anúncio do conjunto → CANDIDATO A REDUÇÃO, não pausa (pausar conjunto reseta).

## KR-2 · CPA bruto acima do teto, sustentado
cpa_bruto ≥ `<cpa_max_bruto>` × `<fator_kill>` (referência 1,5) por ≥ `<janela_min_kill_dias>` **E** conversões ≥ `<conv_min_kill>` (referência 5) **E** tendência não melhorando (D-3 vs D-7) **E** tracking APROVADO **E** fora do aprendizado → CANDIDATO A REDUÇÃO (1ª vez) / PAUSA (2ª ocorrência após cooldown).

## KR-3 · Fadiga confirmada
estado_fadiga = SATURADO ou PERDEDOR (detector de fadiga, `regras-meta §9`) **E** existe substituto pronto (Creative Strategist) → CANDIDATO A SUBSTITUIÇÃO (adicionar novo → pausar velho depois; lembrar: adicionar anúncio reseta o conjunto → preferir conjunto novo/duplicado se o atual for estável).

## KR-4 · Margem no prejuízo (veto Financeiro)
margem_pos_midia < 0 no objeto por ≥ `<janela_min_kill_dias>` com dado APROVADO → CANDIDATO A REDUÇÃO imediata; Financeiro veta qualquer aumento.

## KR-5 · Produto sem estoque
DOH < `<doh_min_operacao>` ou item SEM ESTOQUE → remover do product set (N3 se liberado) e CANDIDATO A PAUSA dos anúncios exclusivos do produto.

## KR-6 · Risco de conta (veto Auditoria)
anúncio rejeitado em escala, rótulo de política, restrição parcial → CANDIDATO A PAUSA imediata dos objetos envolvidos; Auditoria assume; ⚫ se restrição de conta.

## O QUE NÃO É KILL RULE
- Conjunto em **aprendizado limitado**: consolidar verba/criativos, não pausar por CPA.
- Queda de conversões após mudança de atribuição/janela (verificar Tracking antes).
- CTR caiu sem CPM/frequência mudarem (verificar antes de culpar criativo).
- Um dia ruim (segunda parcial vs domingo completo).
- Conversões D-1 não maturadas.

## SAÍDA OBRIGATÓRIA
Pacote-padrão com FATO (números, janela), REGRA (KR-n), CANDIDATO A (pausa/redução/substituição), RESET_APRENDIZADO, IMPACTO (R$ bruto/dia poupado), RISCO (o que se perde), NEXT_REVIEW.
