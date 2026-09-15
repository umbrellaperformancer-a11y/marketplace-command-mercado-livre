# PROTOCOLO DE HANDOFF — quem entrega o quê para quem · v2.1

Handoff = pacote-padrão (kernel §5) com TIPO `handoff`, salvo no chat do projeto e, quando gera decisão, no `decision_log`. Um handoff sem FATO numérico e sem NATUREZA do dado é devolvido.

## MAPA DE HANDOFFS
| de | para | o que entrega | quando |
|---|---|---|---|
| Setup | todos | `config/empresa.yaml`, Planilha v2, `base_custos.md`, baseline em `snapshots/` | instalação |
| Analista | Diretor, Otimizador, Funil, Creative | leitura hierárquica por janela, breakdowns, export CSV | D+1 e sob demanda |
| Diretor de Performance | Comitê | diagnóstico executivo | D+1, D+7 |
| Financeiro | Arquiteto, Budget, Escala, Publicador | CPA máximo bruto, ROAS break-even, Cost Cap/Min ROAS líquidos, veto | antes de qualquer verba/lance |
| Tracking | Analista, Escala, Publicador, Alertas | estado de confiança do sinal (EMQ/dedup/cobertura/janela), veto de escala | D+1 e antes de escalar |
| Catálogo | Escala, Publicador, Arquiteto | product sets atualizados, itens fora (sem estoque/rejeitados), taxa de match | D+1 |
| Creative Strategist | Copy, Vídeo, Testes, Arquiteto | briefing, matriz de combinações, lista de fadigados | semanal |
| Copy / Vídeo | Testes, Publicador | peças com hipótese, flag IA | por lote |
| Públicos | Arquiteto, Escala | exclusões, sobreposição, diagnóstico criativo × público × oferta | sob demanda |
| Funil | Growth, Creative, Tracking, dono | ponto de vazamento + hipótese + evidência | D+7 |
| Testes | Otimizador, Creative | resultado com decisão (vencedor/perdedor/inconclusivo) | fechamento do teste |
| Otimizador | Publicador | ação com FATO→DIAGNÓSTICO→HIPÓTESE→AÇÃO→IMPACTO→RISCO→RESET→REVIEW | por ação |
| Escala | Budget, Publicador | plano de escala com checklist verde | quando elegível |
| Budget | Comitê, Publicador | alocação CORE/TESTE/ESCALA/EXPERIMENTOS em bruto | D+7, D+30 |
| Competitividade | Creative, Growth, Comitê | movimentos do concorrente + reagir/ignorar/flanquear | semanal |
| Radar | Comitê, todos | relatório de mudanças de plataforma + skill atualizada | mensal |
| Auditoria | Publicador, Comitê | veto/liberação de conta, apelação | contínuo |
| Alertas | Orquestrador, dono | alertas classificados | contínuo |
| Publicador | execution_log, Alertas, Orquestrador | evidência pós-ação | toda execução |
| BI | Diretor, Comitê, dono | placar e dashboard | D+1, D+7, D+30 |
| Orquestrador | Comitê | fila consolidada 🟢🟡🔴⚫, conflitos arbitrados | D+1 |
| Comitê | dono | output executivo + prioridades 1/2/3 | D+7 e sob demanda |

## REGRAS
1. Handoff para o Publicador só chega com os vetos consultados (Financeiro, Tracking, Auditoria) e o checklist de 6 validações preenchido.
2. Quem recebe confirma recebimento em 1 linha ou devolve com motivo.
3. Handoff com dado VENCIDO ou INSUFICIENTE segue, mas a ação fica bloqueada até o dado ser refeito.
4. Ninguém "chama todos": o Orquestrador escolhe quem entra.
