# MATRIZ DE AUTONOMIA — META ADS PERFORMANCE OS · v2.1

Padrão de instalação: **N2 em tudo**. A coluna "N3 possível?" diz o que o dono PODE liberar depois; o valor liberado fica em `config/empresa.yaml → autonomia`. Nenhum percentual abaixo é regra universal — todos apontam para a config. "Reseta?" = efeito na fase de aprendizado (`regras-meta §3`).

| ação | nível padrão | N3 possível? | limite (config) | aprovação | cooldown | rollback | reseta? | log |
|---|---|---|---|---|---|---|---|---|
| ler qualquer painel | N0 | — | — | não | — | — | não | leitura carimbada act= |
| exportar relatório CSV | N0 | — | — | não | — | — | não | sim |
| recomendar / simular | N1 | — | — | não | — | — | — | decision_log |
| preparar campanha/conjunto/anúncio (rascunho) | N2 | não | — | **publicar só com "pode publicar"** | — | descartar rascunho | n/a | execution_log |
| publicar campanha nova | N2 | não | orçamento ≤ `orc_max_nova_campanha` | sim, dono | `cooldown_padrao_h` | pausar | n/a | sim + evidência |
| criar conjunto em campanha ativa | N2 | não | — | sim | sim | pausar | não no conjunto irmão; CBO redistribui | sim |
| adicionar anúncio a conjunto ativo | N2 | não | — | sim | sim | pausar anúncio | **sim (conjunto)** | sim |
| duplicar (nasce pausado) | N2 | sim | — | ativar = aprovação | — | pausar | n/a | sim |
| pausar anúncio | N2 | sim | — | N3 se liberado | `cooldown_padrao_h` | ativar | conjunto pode reaprender | sim |
| pausar conjunto | N2 | sim (só ⚫/kill rule cumprida) | — | N3 se liberado | sim | ativar (**reseta ao voltar**) | **sim** | sim |
| pausar campanha | N2 | só ⚫ | — | sim | sim | ativar | sim | sim |
| pausar tudo (kill switch global) | humano | só ⚫ pré-autorizado | — | dono | — | ativar 1 a 1 | sim | sim + alerta ⚫ |
| ativar objeto pausado | N2 | não | — | sim | sim | pausar | sim | sim |
| aumentar orçamento (declarar nível) | N2 | sim | ≤ `limite_orcamento_sem_reset_pct` por vez; ≤ `aumento_max_dia_pct`; ≤ `orcamento_mes_bruto` | N3 se liberado e checklist verde | `cooldown_padrao_h` + fora de aprendizado | valor anterior (não devolve aprendizado) | não se ≤ limite; **provável** acima | sim |
| reduzir orçamento | N2 | sim | ≥ `reducao_max_pct` | N3 se liberado | sim | valor anterior | provável se grande | sim |
| mudar estratégia de lance / cost cap / min ROAS | N2 | não | dentro de `formulas §4` | sim | sim | valor anterior | **sim** | sim |
| mudar evento de otimização | N2 | não | — | sim | sim | valor anterior | **sim** | sim |
| mudar público / exclusões | N2 | não | — | sim | sim | valor anterior | **sim** | sim |
| mudar placements | N2 | não | — | sim | sim | valor anterior | provável | sim |
| editar copy/criativo de anúncio ativo | N2 | não | — | sim | sim | versão anterior | provável (criativo) | sim |
| mudar janela de atribuição | N2 | não | — | sim + Tracking | — | valor anterior | não (relatório) | sim + alerta 🟡 |
| editar product set | N2 | sim (só remover SEM ESTOQUE) | — | N3 só para remoção por ruptura | — | reincluir | não | sim |
| alterar feed / IDs do catálogo | N2 | não | IDs nunca mudam | sim + Catálogo | — | versão anterior do feed | sim (produto) | sim |
| instalar regra automatizada nativa | N2 | não | só notificação e pausa por CPA com amostra | sim | — | desligar regra | não | sim |
| alterar configuração de tracking (Pixel/CAPI/eventos) | N2 | não | com backup documentado | sim + Tracking | — | backup | não | sim |
| subir lista de clientes | N2 | não | base legal LGPD confirmada, hash | sim | — | excluir público | não | sim (sem PII) |
| apelar restrição no Account Quality | N2 | não | texto preparado | sim, dono envia | — | — | — | sim |
| alterar limite de gasto da conta | **PROIBIDO** | — | — | — | — | — | — | recusar + log |
| alterar método/threshold de cobrança | **PROIBIDO** | — | — | — | — | — | — | recusar + log |
| excluir campanha/conjunto/anúncio/público | **PROIBIDO** | — | — | — | — | — | — | recusar (só pausa) |
| login / captcha / 2FA | **PROIBIDO** | — | — | humano | — | — | — | PARA |

## REGRAS DA MATRIZ
1. Ação não listada = N2 por padrão.
2. N3 nunca vale dentro da fase de aprendizado, com dado DIVERGENTE/VENCIDO/INSUFICIENTE, com conta em restrição, ou com veto ativo.
3. Toda ação N3 executada é reportada ao dono no próximo D+1 com ANTES/DEPOIS.
4. Limite financeiro agregado: soma dos aumentos do dia ≤ `aumento_max_dia_pct` do orçamento diário total; soma do mês ≤ `orcamento_mes_bruto`.
5. Mudar esta matriz = nova versão + `changelog.md` + aprovação do dono.
