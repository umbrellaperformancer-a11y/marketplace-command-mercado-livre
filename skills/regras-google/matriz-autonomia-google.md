# MATRIZ DE AUTONOMIA · v2.0 — padrão N2; N3 só o que o dono liberar (config). "Reseta?" = aprendizado do lance.
| ação | padrão | N3? | limite (config) | reseta? | rollback |
|---|---|---|---|---|---|
| ler / exportar | N0 | — | — | não | — |
| recomendar/simular | N1 | — | — | — | — |
| preparar campanha (rascunho/pausada) | N2 | não | orc_max_nova_campanha | n/a | descartar |
| publicar campanha nova | N2 | não | idem; "pode publicar" | novo objeto aprende | pausar |
| pausar/ativar anúncio ou keyword | N2 | sim | — | leve | reverter |
| pausar campanha | N2 | só ⚫ | — | sim (ao voltar) | ativar |
| pausar tudo | humano | só ⚫ pré-aut. | — | sim | 1 a 1 |
| alterar budget | N2 | sim | ≤ limite_budget_sem_reset_pct/vez; ≤ aumento_max_dia_pct | provável se grande | valor anterior |
| alterar tCPA/tROAS | N2 | não | ≤ limite_meta_sem_reset_pct; dentro de formulas §4 | **sim se além do limite** | valor anterior |
| trocar estratégia de lance | N2 | não | — | **sim** | anterior |
| adicionar negativa (grupo/campanha) | N2 | sim (lista pré-aprovada de desperdício óbvio) | risco avaliado | não | remover |
| negativa AMPLA / lista compartilhada | N2 | não | crítica | não | remover |
| adicionar keyword | N2 | sim | — | não | pausar |
| editar RSA/assets | N2 | não | — | leve | versão anterior |
| editar asset group PMax / audience signals | N2 | não | — | provável | anterior |
| brand exclusions PMax | N2 | não | — | provável | anterior |
| alterar ações de conversão / janela | N2 | não | backup obrigatório + Tracking | **sim** | backup |
| data exclusion / seasonality adj. | N2 | não | Tracking assina | não | remover |
| editar feed/custom labels (Merchant) | N2 | sim (só label por ruptura/ranking) | ids nunca mudam | não | versão do feed |
| aceitar recomendação do Google | N2 | nunca auto | classificação registrada | depende | — |
| desligar auto-apply | N2 | não | — | não | religar |
| apelação de política | prepara; dono envia | não | — | — | — |
| pagamento/cartão/cobrança · excluir objeto · edição em massa · operar MCC · login/captcha | **PROIBIDO** | — | — | — | — |
Regras: N3 nunca em learning, dado ruim, conta restrita ou veto · ações N3 reportadas no D+1 · soma dos aumentos do dia ≤ aumento_max_dia_pct · mudar a matriz = versão + changelog + dono.
