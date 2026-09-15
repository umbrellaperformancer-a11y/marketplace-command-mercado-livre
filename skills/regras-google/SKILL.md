---
name: regras-google
description: Regras específicas do Google Ads / Merchant Center / GA4 para o Google Ads Performance Brain. Use em QUALQUER tarefa de Google Ads — define os painéis, o DNA da conta (metas, margens, autonomia, limites) e as mecânicas vivas da plataforma (Smart Bidding e aprendizado, lag de conversão, pacing 2×, PMax e canibalização de marca, Shopping/feed/custom labels, recomendações e auto-apply, conversões/Consent Mode/Enhanced, tributos BR conforme fatura). Identidade da conta vem da config do projeto. Use APENAS para Google — NÃO use para Meta Ads nem marketplaces.
---

# ▶️ REGRAS — GOOGLE ADS (motor compartilhado) · v2.0

Identidade da CONTA ATIVA (Customer ID, Merchant ID, GA4, moeda, fuso) em `config/empresa.yaml`. Arquitetura no KERNEL `sistema-operacional-google`; aprovação/PARA/número real em `regras-comuns`. Arquivos-irmãos: `mecanicas-google.md` (tabela verificável), `matriz-autonomia-google.md`, `kill-rules.md`, `scale-rules.md`, `naming-convention.md`, `changelog.md`.
> ⚠️ A tela vence o texto. Divergiu → reporta e o `agente-radar-google` versiona.

## PAINÉIS (sempre conferindo o CID no topo — kernel §4)
Google Ads (Visão geral, Campanhas, Grupos, Anúncios/Assets, Palavras, **Termos de pesquisa**, Públicos, Produtos, **Relatório de estratégia de lances/learning**, Recomendações/auto-apply, Alterações, Faturamento — só leitura de status) · Merchant Center (Produtos/Diagnóstico, feed, custom labels, política) · GA4 (Aquisição, Monetização, eventos, consent) · Página de status de política.

## 1. CONVERSÕES E LAG (a regra nº 1 da leitura)
- O Google reporta a conversão **na data do CLIQUE**: os últimos `lag_dias` (config, padrão 3–7; medir o lag real da conta no Setup) sempre parecem piores e depois "preenchem". Kill/scale só com dado maturado; D-1 nunca é definitivo.
- Fontes: tag do Google Ads (primária recomendada) vs importadas do GA4 — **nunca misturar fontes na mesma comparação**; a conta define quais ações são "primárias" (contam para lances).
- Google Ads ≠ GA4 por definição (modelo data-driven vs last click, data do clique vs sessão, consent). Divergência dentro de `tolerancia_ga4` (config, ref. 15–30%) é normal; acima → Tracking investiga (nunca "escolher o certo").
- Enhanced Conversions e Consent Mode: status verificado no Setup; ausentes = subcontagem esperada, confiança com ressalva.
- **Data exclusions**: se o tracking quebrar por dias, além do veto, recomendar exclusão do período para o Smart Bidding não aprender com dado sujo. **Seasonality adjustments** para promoções-relâmpago em vez de mexer na meta.

## 2. SMART BIDDING E APRENDIZADO
- Estratégias: Maximize Conversions/Value (com tCPA/tROAS opcional), tCPA, tROAS, Manual (legado). Lance real é do algoritmo; controle é pela META.
- **Reseta/reinicia aprendizado (~2 semanas):** trocar estratégia; mudar tCPA/tROAS além de `limite_meta_sem_reset_pct` (ref. 15–20% por vez); mudar ações de conversão primárias; grandes mudanças de orçamento. Status "Learning/Limited" no relatório de lances = não julgar performance.
- Meta agressiva demais (tROAS muito acima do histórico) **colapsa a entrega**. Introdução gradual (`fator_introducao_meta`).
- Toda recomendação declara RESET sim/não/provável; cooldown por objeto (`cooldown_padrao_h`); mudanças múltiplas no mesmo objeto → de uma vez (um reset).

## 3. ORÇAMENTO E PACING
- O Google pode gastar **até 2× o orçamento diário** num dia, compensando no mês (média × 30,4). Alerta de "gasto disparou" compara com o MÊS/semana, não com o dia.
- "Limitada por orçamento" + Search Lost IS (budget) alto = oportunidade de escala SE piso e estoque permitirem; Lost IS (rank) = problema de lance/qualidade, não de verba.

## 4. SEARCH, KEYWORDS E TERMOS
- Separar BRAND × NON-BRAND sempre (Brand mede captura, não geração — nunca provar crescimento com ROAS de marca).
- Match types atuais são amplos; a alavanca real é o **relatório de Termos** + negativas. Negativa nunca automática: avaliar volume, intenção, período, correspondência que pode bloquear tráfego bom; negativas amplas são ação crítica.
- Quality/Ad Strength e Optimization Score são métricas do Google, não do negócio: nunca otimizar para elas cegamente; pinning em RSA documenta o trade-off.

## 5. PERFORMANCE MAX
- PMax **tem prioridade sobre Shopping padrão** no leilão do mesmo produto — coexistência é decisão de arquitetura, não acaso.
- ROAS alto exige investigar composição: quanto é marca? remarketing? poucos SKUs? Usar insights/termos disponíveis, quebra por canal quando exposta, e relatório de produtos.
- **Brand exclusions / negativas de campanha** para conter canibalização de marca; Final URL expansion desligada salvo decisão; asset groups espelham os custom labels (§6); sem assets mínimos o grupo limita a entrega.
- Nunca reconstruir PMax automaticamente; mudanças são edições significativas.

## 6. SHOPPING, MERCHANT E CUSTOM LABELS (o ranking vira alavanca aqui)
- content: feed com título, imagem, preço, disponibilidade, GTIN/marca, categoria; **item_id estável**; preço/disponibilidade do feed = site (divergência reprova).
- Diagnóstico: aprovados / limitados / reprovados — reprovação de HERO é ⚫ bloqueio comercial; suspensão de Merchant é ⚫⚫.
- **custom_label_0..4**: o ranking financeiro (HERO/CORE/TESTE/BAIXA/SEM_ESTOQUE) é gravado como label pelo Merchant (com aprovação) e Shopping/PMax segmentam e orçam por label. SEM_ESTOQUE sai por disponibilidade do feed, nunca por exclusão manual esquecida.
- Mudanças em massa no feed disparam revisão; cadência mínima diária.

## 7. RECOMENDAÇÕES E AUTO-APPLY
- **Setup verifica se auto-apply está LIGADO** (muitas contas têm sem saber) e recomenda desligar (com aprovação). Nenhuma recomendação é aceita no fluxo de outra ação.
- Toda recomendação do Google: ACEITAR / TESTAR / REJEITAR / INVESTIGAR, com motivo registrado. Optimization Score não é meta.

## 8. COBRANÇA E TRIBUTOS (Brasil)
- Como o imposto aparece depende do faturamento da conta: **`imposto_incluso: sim/não/PENDENTE`**, conferido na fatura real pelo Setup — nunca assumir. Toda decisão de dinheiro usa o bruto conforme a config (`formulas §4`).
- Regime tributário/créditos → PENDENTE + contador. O cérebro nunca toca em pagamento, cartão, limite de cobrança.

## 9. POLÍTICAS E SAÚDE
- Reprovações de anúncio, restrições e suspensões (Ads e Merchant): congelar expansão, preservar relatórios, apelação como changelog conciso enviada pelo dono; nunca criar conta paralela.
- Alterações críticas (exigem cuidado dobrado): conversões, estratégia de lance, budget elevado, URLs, feed, exclusões amplas, configurações de conta.

## 🧬 DNA DA CONTA (valores em `config/empresa.yaml`)
metas (receita, tROAS/tCPA bruto, MER) · orçamento mês bruto · reservas teste/escala · lag_dias · tolerancia_ga4 · limite_meta_sem_reset_pct · limite_budget_sem_reset_pct · cooldown_padrao_h · dias_estabilidade · fator_introducao_meta · amostra_min_kill · janela_min_kill_dias · conv_min_kill/escala · doh_min · autonomia N3 · alertas. Vazio = PENDENTE_CONFIGURACAO.
