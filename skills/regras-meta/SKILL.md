---
name: regras-meta
description: Regras específicas do Meta Ads (Facebook, Instagram, WhatsApp, Messenger) para o Meta Ads Performance OS. Use em QUALQUER tarefa de Meta Ads — define os painéis (Ads Manager, Events Manager, Commerce Manager, Account Quality, Business Settings), o DNA da conta (metas, margens, autonomia, limites) e as mecânicas vivas da plataforma em 2026 (Andromeda/Advantage+ padrão, atribuição, fase de aprendizado e edição significativa, lances, tracking, tributos BR, limites de gasto, catálogo, políticas). Identidade da conta vem da config do projeto. Use APENAS para Meta Ads — NÃO use para Mercado Livre, Shopee, Amazon, TikTok Shop nem SHEIN.
---

# ▶️ REGRAS — META ADS (motor compartilhado) · v2.1

Valem para qualquer conta de anúncios operada pelo Meta Ads Performance OS. A identidade da CONTA ATIVA (act=, business_id, nome, pixel, catálogo, moeda, fuso, pastas) vem de **`config/empresa.yaml`**. Aprovação obrigatória, PARA e "número real ou nada" estão em `regras-comuns`. Arquitetura (hierarquia, trava de identidade, comunicação, confiança, autonomia, logs) está no KERNEL `sistema-operacional-meta` — todo `agente-*-meta` herda kernel + estas regras. Arquivos-irmãos: `mecanicas-meta-2026.md` (detalhe e fontes), `matriz-autonomia-meta.md`, `kill-rules.md`, `scale-rules.md`, `naming-convention.md`, `changelog.md`.

> ⚠️ A Meta muda painel, atribuição, aprendizado e política com frequência. **A tela vence o texto.** Quando divergir, o agente reporta e o `agente-radar-meta` atualiza este arquivo com versão nova + changelog. Cada mecânica abaixo tem `verificado_em` no arquivo de detalhe.

## 🧠 A LÓGICA DA META EM 2026 (criativo é o público)
Desde o Andromeda (rollout completo fim de 2025) o sistema de entrega lê o **criativo** para prever quem deve ver o anúncio; interesses e lookalikes viraram sugestão. Em fev/2026 a Meta fundiu "Manual" e "Advantage+ Shopping" num fluxo único: Advantage+ Audience, Advantage+ Placements, Advantage+ Creative e CBO já vêm ligados. O que move resultado: **diversidade criativa** (referência 10–20 anúncios ativos com hooks/formatos distintos), **estrutura simples** (poucos conjuntos, bem financiados) e **qualidade de sinal** (Pixel + CAPI, EMQ alto). Isso muda a prioridade de todos os agentes: Creative Strategist puxa a aquisição; Arquiteto não replica estrutura antiga por hábito; Públicos cuida de exclusões, remarketing e saturação — não de "achar o público".

## PAINÉIS PRINCIPAIS (sempre por URL direta com `act=` / `business_id` — kernel §4)
- **Ads Manager** `adsmanager.facebook.com/adsmanager/manage/campaigns?act=<id>&business_id=<bm>` — campanhas, conjuntos, anúncios, colunas, breakdowns, **Exportar relatório (CSV)** (fonte primária em conta grande), regras automatizadas, rascunhos ("Revisar e publicar").
- **Events Manager** `business.facebook.com/events_manager2/list/pixel/<pixel_id>?business_id=<bm>` — Pixel/dataset, CAPI, EMQ, dedup, cobertura, Test Events, diagnósticos.
- **Commerce Manager** — catálogo, feed, product sets, itens rejeitados, taxa de match.
- **Account Quality** `business.facebook.com/accountquality?business_id=<bm>` — restrições, rejeições, apelações.
- **Business Settings** — contas, pessoas, papéis, verificação do negócio, limite de gasto da conta, cobrança (só leitura de status — nunca de números de cartão).
- **Biblioteca de Anúncios** — concorrência (pública).

## 1. ATRIBUIÇÃO (referência 2026)
- Jan/2026: janelas **7d-view e 28d-view removidas**. Mar/2026: **click-through = só clique em link**; likes, shares, saves e comentários foram para **engage-through (1 dia)**. Cobrança não mudou; só o relatório. Engaged-view de vídeo = 5s.
- Padrão de conversão de site: **7d click / 1d engage-through / 1d view**. A janela da CONTA ATIVA está em `config/empresa.yaml → janela_atribuicao` e vai em TODO número de conversão.
- Regras: comparar só janelas iguais; reportar click-through e engage-through separados; queda de conversões após mudança de definição não é queda de performance até prova; conversão de D-1 ainda matura por 7 dias.
- Três visões: **META VIEW** (atribuída) · **BUSINESS VIEW** (ERP/loja) · **EXECUTIVE VIEW** (consolidada). Nunca somar.

## 2. ESTRUTURA E ADVANTAGE+
- Advantage+ é o padrão para Vendas, Leads e App. Advantage+ Sales (ex-Advantage+ Shopping) é a campanha padrão de e-commerce.
- **CBO** distribui verba entre conjuntos; **ABO** dá controle por conjunto. Quebrar em conjuntos só por necessidade real (exclusão, oferta, geografia, orçamento isolado de teste).
- Advantage+ Creative (melhorias automáticas) ≠ Dynamic Creative (combina seus ativos) ≠ Flexible Ad Formats (Meta escolhe o formato). O agente de Testes escolhe; para isolar variável usa conjuntos separados.
- Local de conversão: site, app, **conversas (WhatsApp/Messenger/Direct — comum no BR)**, loja. Venda fechada no WhatsApp entra na Meta via evento de conversa/CAPI, não pelo Purchase do site.

## 3. FASE DE APRENDIZADO E EDIÇÃO SIGNIFICATIVA (a regra do cooldown)
- Sai do aprendizado com **~50 eventos de otimização em 7 dias**. "Aprendizado limitado" = diagnóstico estrutural (orçamento incapaz de gerar 50 eventos, público, sinal) — consolidar, não pausar por CPA.
- **Reseta:** pausar o conjunto; mudar evento de otimização, público ou criativo; **adicionar anúncio novo a conjunto ativo**; mudança grande de lance ou orçamento (magnitude importa — referência de mercado ~20% de uma vez; limite exato em `config → limite_orcamento_sem_reset_pct`). **Não reseta:** nome, agenda dentro da janela, pequenas mudanças de orçamento.
- 2026 endureceu: relatos de reset em edições antes seguras. Política do cérebro: resolver tudo antes de publicar; após sair do aprendizado, **janela de não-edição** (`config → janela_nao_edicao_dias`, referência 7); se precisar editar, todas as mudanças de uma vez.
- Todo agente declara **RESET_APRENDIZADO: sim/não/provável** em qualquer recomendação. O Publicador faz o pré-check antes de executar.
- Cost cap: usar custo por evento medido desde a última edição significativa; esperar ~50 eventos antes de definir.

## 4. LANCES
- Lance manual real foi praticamente aposentado. Controle: **Highest Volume**, **Cost Cap**, **Bid Cap**, **Minimum ROAS** (e Highest Value).
- Cost Cap / Min ROAS muito acima do histórico recente **colapsam a entrega**. Introdução: fração configurável do histórico (`config → fator_introducao_cap`), apertar gradualmente a cada N dias.
- Em Advantage+ Sales de alto volume a Meta aplica pacing próprio; Min ROAS é guia, não trava.
- **Parâmetros da Meta são LÍQUIDOS; metas do Financeiro são BRUTAS.** Conversão obrigatória em `sistema-operacional-meta/formulas-financeiras.md §4`.

## 5. TRACKING — LIMIARES TÉCNICOS
- Dedup: mesmo `event_id` + `event_name` (case-sensitive) no Pixel e na CAPI, janela 48h; fallback `event_name` + fbp ou external_id.
- Dedup saudável no Purchase (setup dual): **~40–70%**. ≈0 → event_id não passa. ≈100% → anormal. Contagem 2× do esperado = dedup quebrado, ROAS inflado.
- Cobertura de eventos = % de eventos do Pixel cobertos pela CAPI com chave de dedup. Alvo: ViewContent, AddToCart, Purchase todos por servidor.
- **EMQ** 0–10; típico 4–6; **alvo ≥ 7**; o que importa é o EMQ do Purchase. Parâmetros: email, telefone, nome, cidade, estado, CEP, país, external_id, fbp/fbc (hasheados). Mudança reflete em 24–48h, estabiliza em 3–5 dias.
- Marketing API: v25.0 na data desta versão (fev/2026); versão depreciada para de ser aceita em silêncio.
- Limiares de rebaixamento de confiança em `sistema-operacional-meta/protocolo-confianca.md §5`.

## 6. COBRANÇA, TRIBUTOS E LIMITES (Brasil)
- Desde 01/01/2026 a Meta repassa **PIS, COFINS e ISS** na fatura. Referência: 9,25% + ISS municipal 2–5% (SP 2,9% → ~12,15%). **`config → imposto_midia_pct` é obrigatório e conferido na fatura real pelo Setup — nunca assumir fixo.** O Ads Manager mostra TUDO sem imposto (orçamento, gasto, CPA, ROAS, limites).
- Regime tributário (Simples/Presumido/Real) muda crédito de PIS/COFINS → `PENDENTE_CONFIGURACAO` até o dono/contador informar; o cérebro não decide crédito.
- Taxas de localização (jul/2026) para público em IT, ES, FR, UK, TR, AT etc. — só se a conta anuncia fora do BR.
- **Limite de gasto da conta** é cumulativo e vitalício; ao bater, a entrega para e a campanha continua "ativa" no painel → alerta ⚫. Threshold de cobrança sobe com imposto. O cérebro NUNCA altera limite ou cobrança.
- **Pacing:** com orçamento diário a Meta pode gastar acima do diário em alguns dias e compensar na semana-calendário (limite histórico ~25%/dia; Radar confirma). Alerta "gasto disparou" compara com a semana.
- **Regras automatizadas nativas** = kill switch redundante fora do cérebro. Propor no D3 e instalar só com aprovação: notificação de gasto anormal + pausa por CPA com amostra mínima. Nunca regra só por ROAS da Meta.

## 7. CATÁLOGO
- `content_ids` dos eventos = `id` do feed, exatamente. **IDs estáveis** (trocar ID reseta o aprendizado por produto). Taxa de match alvo > 75%.
- Mudança frequente no feed dispara revisão e tira itens do ar temporariamente. Cadência: mínimo diário; horário para estoque volátil.
- **Product sets** = alavanca manual dentro do formato automatizado: HERO / CORE / BAIXA MARGEM / SEM ESTOQUE (excluído). Espelham o ranking de produtos. Identidade SKU ↔ EAN ↔ content_id vem do Catálogo Mestre do Cérebro Central quando existir.

## 8. POLÍTICAS E SAÚDE DA CONTA
- Anúncio fica sob revisão contínua; restrição pode ser de conta, Página, BM ou usuário. Apelação pelo Account Quality, como changelog conciso com correções verificáveis.
- **Verificação do negócio** libera limites maiores e acelera apelação; **2FA** obrigatório.
- **Desde mar/2026: disclosure obrigatória de conteúdo gerado/modificado por IA.** Rejeição comum. Todo criativo IA tem flag `conteudo_ia` e disclosure no Publicador.
- Categorias sensíveis (saúde, financeiro, emagrecimento) recebem mais revisão; claim ≠ landing page é causa frequente de rejeição.
- Durante revisão/restrição: congelar expansão, preservar relatórios, não reescrever funil em pânico. **Nunca** contornar enforcement, criar BM/conta paralela para fugir de restrição ou usar ativo vinculado a conta restrita.

## 9. CRIATIVO E FADIGA
- 9:16 vertical prioritário; hook no 1º segundo; legenda embutida.
- Advantage+ concentra entrega nos segmentos mais responsivos → fadiga em 2–3 semanas (antes 4).
- Ads Manager mostra rótulos **Creative Limited / Creative Fatigue** (mais confiáveis em conjunto com criativo único ou catálogo). Rótulo = dano feito; sinais antecedentes: **CPM por alcance** subindo sustentado, CTR caindo direcional (referência 5 dias), frequência por anúncio/placement, razão 1d/7d click migrando para janelas longas.
- Diferenciar **fadiga de criativo** (troca criativo) × **saturação de público** (amplia/exclui) × **esgotamento de oferta** (muda oferta). Tratar o errado desperdiça verba.

## 🧬 DNA OPERACIONAL DA CONTA (valores em `config/empresa.yaml`; abaixo os campos)
`meta_receita_mes` · `meta_roas_bruto` · `meta_mer` · `cpa_max_bruto` · `margem_pre_midia_min` · `orcamento_mes_bruto` · `reserva_teste_pct` · `reserva_escala_pct` · `emq_minimo` · `dedup_min/max` · `cobertura_min` · `frequencia_alerta` · `doh_min_escala` · `limite_orcamento_sem_reset_pct` · `janela_nao_edicao_dias` · `fator_introducao_cap` · `amostra_min_kill` · `janela_min_kill_dias` · `cooldown_padrao_h`. Campo vazio = `PENDENTE_CONFIGURACAO` (o agente avisa e não assume).
