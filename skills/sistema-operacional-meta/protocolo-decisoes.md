# PROTOCOLO DE DECISÕES — `dados/decision_log.md` · v2.1

## FORMATO DE CADA DECISÃO (uma entrada por decisão, append-only)
```
ID: DEC-<AAAAMMDD>-<seq>
DATA/HORA: · CONTA: act=<id> · <nome>
OBJETO: campanha/conjunto/anúncio/criativo/produto/product set/conta
SITUAÇÃO: [o que estava acontecendo]
DADOS: [métricas, janela, período, fonte] · NATUREZA: [CONFIRMADO/CALCULADO/ESTIMADO/INFERIDO/AUSENTE] · CONFIANÇA: [estado]
DIAGNÓSTICO: [leitura] · HIPÓTESE: [por que]
AÇÃO: RECOMENDAR | PREPARAR | SIMULAR | EXECUTAR | CONFIRMAR
MOTIVO: · REGRA USADA: [ex.: kill-rules §2 / scale-rules §3 / matriz linha X]
VALOR ANTES → VALOR DEPOIS: (líquido e bruto quando for dinheiro)
NÍVEL DO ORÇAMENTO: campanha | conjunto
RESET_APRENDIZADO: sim | não | provável
RESPONSÁVEL (agente) · APROVADOR (dono / N3 pré-autorizado) · VETOS CONSULTADOS:
RESULTADO ESPERADO: [métrica, valor, prazo] · DATA DE REVISÃO:
--- fechamento ---
RESULTADO REAL: · VEREDITO: ACERTO | ERRO | INCONCLUSIVO · APRENDIZADO:
```

## REGRAS
1. Decisão sem DATA DE REVISÃO não é decisão — é opinião.
2. Sem fechamento, o agente não repete recomendação do mesmo tipo no mesmo objeto.
3. RECOMENDAR ≠ PREPARAR ≠ EXECUTAR ≠ CONFIRMAR. "Campanha alterada" só após CONFIRMAR com evidência lida na tela/export.
4. Decisão que derruba um veto registra a autorização escrita do dono.
5. Decisão de ⚫ pode pular a fila, nunca o log.
6. Auditoria cruzada mensal: o Orquestrador sorteia 5 decisões e o BI refaz a conta de trás pra frente.
