# CONTRATO DE DADOS — META ADS PERFORMANCE OS · v2.1

Todo registro que circula entre agentes, entra em log ou alimenta o BI segue este contrato. Campo ausente = `AUSENTE`, nunca em branco silencioso.

## 1. IDENTIDADE (obrigatórios em todo registro)
| campo | descrição |
|---|---|
| tenant_id | cliente/operação |
| empresa_id · marca_id | empresa e marca |
| business_id | Business Manager (portfólio) |
| ad_account_id | `act=` numérico — a chave da trava de identidade |
| ad_account_nome | nome exibido (só conferência) |
| pixel_id · dataset_id | fonte de eventos |
| catalogo_id · product_set_id | quando o objeto é de catálogo |
| campanha_id · adset_id · ad_id · creative_id | hierarquia Meta |
| produto_id · sku · content_id | vínculo com produto (content_id = id do feed) |

## 2. CONTEXTO
| campo | descrição |
|---|---|
| data_inicio · data_fim · timezone · currency | sempre no fuso e moeda da conta |
| janela_atribuicao | ex.: `7d_click/1d_engage/1d_view` — obrigatório em qualquer métrica de conversão |
| objetivo · local_conversao | Vendas / Leads / Conversas — site / WhatsApp / loja |
| evento_otimizacao | Purchase, AddToCart, Lead, Conversa… |
| estrategia_lance · cost_cap · min_roas · bid_cap | valores LÍQUIDOS (como na Meta) |
| estrutura | CBO / ABO / Advantage+ |
| status | ativo / pausado / rascunho / em revisão / rejeitado / aprendizado / aprendizado limitado / creative fatigue |
| learning_status · last_significant_edit_at | estado de aprendizado e última edição significativa |

## 3. ENTREGA E CUSTO
| campo | descrição |
|---|---|
| budget · budget_nivel | valor e nível (campanha/conjunto) |
| spend | gasto LÍQUIDO (Ads Manager) |
| imposto_pct · spend_bruto | `spend_bruto = spend × (1 + imposto_pct)` |
| impressions · reach · frequency · cpm · cpm_por_alcance | cpm_por_alcance = spend ÷ reach × 1000 |
| clicks · link_clicks · ctr · cpc | CTR de link separado de CTR geral |

## 4. FUNIL E CONVERSÃO (por janela declarada)
landing_page_views · view_content · add_to_cart · checkout · purchase · **purchase_click_through** · **purchase_engage_through** · **purchase_view_through** · leads · conversas_iniciadas · revenue_meta · cpa · cpa_bruto · roas · roas_bruto_equivalente (= roas ÷ (1+imposto)).

## 5. NEGÓCIO (Business View)
revenue_site · revenue_erp · pedidos_erp · cmv · taxas · impostos_venda · frete · descontos · devolucoes · margem_contribuicao · lucro_pos_midia · mer (= receita total ÷ spend_bruto total) · aov · cac · ltv · payback.
Regra: revenue_meta, revenue_site e revenue_erp são **perspectivas** — nunca somadas.

## 6. SAÚDE DE SINAL E CONTA
emq_purchase · emq_por_evento · dedup_rate · event_coverage · capi_ativa · api_version · account_quality_status · verificacao_negocio · limite_gasto_conta · limite_gasto_consumido · rascunhos_pendentes · regras_nativas_ativas.

## 7. CRIATIVO
formato · proporcao · conceito · hook · angulo · persona · oferta · cta · creator · duracao · conteudo_ia (bool) · thumbstop · retencao_3s · estado_fadiga.

## 8. PROVENIÊNCIA (obrigatórios)
| campo | valores |
|---|---|
| fonte | ads_manager_tela · ads_manager_export · events_manager · commerce_manager · account_quality · erp · site · cerebro_central · calculado |
| natureza | CONFIRMADO · CALCULADO · ESTIMADO · INFERIDO · AUSENTE |
| extraido_em | timestamp |
| freshness | idade do dado |
| confidence | APROVADO · APROVADO_COM_RESSALVA · DIVERGENTE · VENCIDO · INSUFICIENTE · DECISAO_BLOQUEADA |
| lineage | de onde veio cada componente de um número calculado |

## 9. REGRAS DE NORMALIZAÇÃO
1. Converter tudo para o timezone e a moeda da conta antes de comparar.
2. Métrica de conversão sem `janela_atribuicao` é INSUFICIENTE.
3. Comparação entre períodos exige mesma janela, mesmo estado de aprendizado e período equivalente (mesmo dia da semana, mesma hora de corte, promoção equivalente).
4. Conversão de D-1 ainda matura durante a janela — marcar `maturado: não` até fechar a janela.
5. Número calculado carrega `lineage` com os componentes e a fórmula (`formulas-financeiras.md`).
6. Contagem Meta ≥ 2× ERP → `DIVERGENTE` + alerta 🔴 Tracking (suspeita de dedup).
