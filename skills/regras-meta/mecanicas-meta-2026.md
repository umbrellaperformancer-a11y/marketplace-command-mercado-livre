# MECÂNICAS DA META 2026 — detalhe, evidência e verificação · v2.1

Mantido pelo `agente-radar-meta`. Cada item: fato · impacto por agente · `verificado_em` · como conferir na tela. Quando a tela divergir, o Radar abre linha no `changelog.md` e sobe versão.

| # | mecânica | fato (resumo) | impacto | verificado_em | conferir em |
|---|---|---|---|---|---|
| 1 | Andromeda | retrieval criativo-primeiro; rollout global fim/2025 | Arquiteto, Creative, Públicos | 2026-08-29 (fontes secundárias) | criação de campanha: opções Advantage+ pré-marcadas |
| 2 | Fluxo unificado | fev/2026: Manual + ASC → 1 fluxo; Advantage+ padrão em Vendas/Leads/App | Arquiteto, Publicador | 2026-08-29 | Ads Manager → Criar |
| 3 | Atribuição jan/2026 | 7d-view e 28d-view removidas (API/relatórios) | Analista, Tracking, BI | 2026-08-29 | Colunas → Configuração de atribuição |
| 4 | Atribuição mar/2026 | click = só link click; social → engage-through 1d; engaged-view 5s | Analista, Tracking, Diretor | 2026-08-29 | idem; comparar mar/25 vs mar/26 |
| 5 | Aprendizado | ~50 eventos/7d; pausar, evento, público, criativo, anúncio novo, grande mudança de verba/lance resetam | Publicador, Otimizador, Escala | 2026-08-29 (Help Center via terceiros) | coluna "Última edição significativa" |
| 6 | Endurecimento 2026 | relatos de reset em edições antes seguras (abr–mai/2026) | todos que editam | 2026-08-29 (relatos) | observar coluna de entrega após edições |
| 7 | Lances | Highest Volume / Cost Cap / Bid Cap / Min ROAS; manual aposentado | Financeiro, Arquiteto | 2026-08-29 | conjunto → estratégia de lance |
| 8 | Dedup | event_id+event_name, 48h; fallback fbp/external_id | Tracking | 2026-08-29 (dev docs Meta) | Events Manager → Dedup keys |
| 9 | EMQ / cobertura / ACR | Dataset Quality API; EMQ 0–10 | Tracking | 2026-08-29 (dev docs Meta) | Events Manager → Diagnóstico |
| 10 | Marketing API v25.0 | fev/2026; ASC/AAC APIs depreciadas; smart_promotion_type removido | Tracking, adapter futuro | 2026-08-29 | changelog dev Meta |
| 11 | Tributos BR | PIS/COFINS/ISS na fatura desde 01/01/2026 (~12,15% SP) | Financeiro, Budget, Setup | 2026-08-29 | última fatura da conta |
| 12 | Taxas de localização | jul/2026, por país do público (IT, ES, FR, UK, TR, AT…) | Financeiro | 2026-08-29 | fatura / aviso Meta |
| 13 | Limite de gasto | cumulativo, vitalício, para entrega ao bater | Alertas, Budget | 2026-08-29 | Business Settings → Cobrança |
| 14 | Pacing diário | pode exceder o diário e compensar na semana (hist. ~25%) | Alertas | 2026-08-29 (verificar) | Help Center "orçamento diário" |
| 15 | Regras automatizadas | nativas, if-then, notificação/pausa/ajuste | Publicador, Alertas | 2026-08-29 | Ads Manager → Regras automatizadas |
| 16 | Catálogo | content_ids = id do feed; IDs estáveis; product sets | Catálogo | 2026-08-29 | Commerce Manager |
| 17 | Disclosure IA | obrigatória desde mar/2026 | Creative, Copy, Vídeo, Publicador, Auditoria | 2026-08-29 | criação de anúncio → opção de divulgação |
| 18 | Verificação do negócio | libera limites/apelação; expansão até fim/2026; 2FA | Auditoria, Setup | 2026-08-29 | Business Settings → Central de segurança |
| 19 | Creative Fatigue label | rótulos Creative Limited / Creative Fatigue na coluna de entrega | Creative, Alertas | 2026-08-29 | coluna Entrega |
| 20 | Placements novos | Threads, Reels compráveis | Arquiteto, Analista | 2026-08-29 | conjunto → posicionamentos |

## PROTOCOLO DE VERIFICAÇÃO NA INSTALAÇÃO (Setup executa, Radar repete mensalmente)
1. Abrir cada tela listada em "conferir em" na CONTA ATIVA (trava de identidade).
2. Para cada mecânica: CONFIRMADA / DIVERGENTE / NÃO VERIFICÁVEL NA TELA.
3. Divergente → linha no `changelog.md` + aviso ao Comitê + proposta de nova versão.
4. Nenhuma mecânica é usada como CONFIRMADA em decisão sem passar por 1–2.

## FONTES CONSULTADAS NA CONSTRUÇÃO (ago/2026)
Documentação de desenvolvedores da Meta (Conversions API, Dataset Quality API); Transparency Center (Advertising Standards); Meta Business Help Center (via citações de terceiros — o site bloqueia leitura automatizada); análises especializadas de 2026 sobre Andromeda, atribuição, aprendizado, lances, tributos BR. O Radar deve substituir citações de terceiros por leitura direta da tela.
