# PROTOCOLO DE CONFIANÇA DOS DADOS · v2.1

## 1. ESTADOS
| estado | significado | efeito |
|---|---|---|
| APROVADO | fonte autorizada, fresco, completo, consistente | decide normalmente |
| APROVADO_COM_RESSALVA | pequena lacuna declarada | decide, declara a ressalva |
| DIVERGENTE | fontes discordam além da tolerância | não decide dinheiro até conciliar |
| VENCIDO | fora do SLA de frescor | não decide; refazer leitura |
| INSUFICIENTE | amostra/janela/campo faltando | não decide; coletar mais |
| DECISAO_BLOQUEADA | veto de dados ativo | só o dono libera |

## 2. FATORES (cada agente avalia e declara)
Autoridade da fonte (§3) · frescor (§4) · completude · consistência entre fontes · independência (duas fontes independentes valem mais) · qualidade do vínculo (content_id ↔ SKU, campanha ↔ produto) · histórico da fonte (já errou?).

## 3. HIERARQUIA DE FONTES POR DOMÍNIO
| domínio | 1ª fonte | 2ª | 3ª |
|---|---|---|---|
| gasto | Ads Manager (export) | Ads Manager (tela) | fatura Meta (bruto) |
| conversões atribuídas | Ads Manager por janela | Events Manager | — |
| receita real | Cérebro Central de Dados | ERP | plataforma da loja |
| custos | `base_custos.md` (via Cérebro Central quando existir) | ERP | — |
| estoque | Cérebro Central / ERP | catálogo (disponibilidade) | — |
| sinal | Events Manager (EMQ/dedup/cobertura) | Test Events | — |
| conta | Account Quality | Business Settings | — |
Quando a tela e o export divergirem, o export vence para número e a tela vence para status.

## 4. SLA DE FRESCOR (padrão; configurável em `regras-meta`)
Ads Manager: ≤ 24h para D+1, ≤ 2h para intraday. Events Manager: ≤ 24h. ERP/Cérebro Central: ≤ 24h (configurável). Custos: ≤ 30 dias ou até mudar preço/fornecedor. Account Quality: ≤ 24h.

## 5. GATILHOS AUTOMÁTICOS DE REBAIXAMENTO
| gatilho | estado | dono |
|---|---|---|
| EMQ Purchase < `emq_minimo` (padrão 6) | DIVERGENTE | Tracking |
| dedup Purchase fora de `dedup_min–dedup_max` (padrão 30–80%) | DIVERGENTE | Tracking |
| cobertura de eventos < `cobertura_min` (padrão 80%) | APROVADO_COM_RESSALVA | Tracking |
| Purchase Meta ≥ 2× pedidos ERP no mesmo período | DIVERGENTE + 🔴 | Tracking |
| janelas de atribuição diferentes na comparação | INSUFICIENTE | Analista |
| conversão de D-1 ainda não maturada usada como definitiva | APROVADO_COM_RESSALVA | Analista |
| ERP sem atualização > SLA | VENCIDO | Financeiro |
| campanha "ativa" sem entrega há > 6h | DIVERGENTE + ⚫ | Alertas |
| act= divergente da config | DECISAO_BLOQUEADA + PARA | todos |

## 6. VETO LOCALIZADO — o que bloqueia e o que não
Bloqueia (dado crítico insuficiente): escalar, aumentar orçamento, definir cost cap/min ROAS, mudar evento de otimização, ligar product set novo com verba.
Não bloqueia: briefing e produção de criativo, copy, auditoria de conta, competitividade, radar, planejamento de testes, pausar por ⚫ de conta.

## 7. NATUREZA DO DADO (marcação obrigatória)
CONFIRMADO (lido) · CALCULADO (fórmula declarada) · ESTIMADO (projeção com premissa) · INFERIDO (dedução, menor peso) · AUSENTE (não existe — nunca preencher para parecer completo).
