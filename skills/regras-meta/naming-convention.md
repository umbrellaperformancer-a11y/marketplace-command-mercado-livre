# NAMING CONVENTION — Meta Ads Performance OS · v2.1

Nome é dado: o Analista, o BI e o log leem o nome para classificar. Sem nome padrão, o objeto não é publicado.

## CAMPANHA
`[TIPO]-[OBJETIVO]-[PRODUTO/LINHA]-[ESTRUTURA]-[DATA AAAAMM]-[vN]`
- TIPO: CORE · TESTE · ESCALA · EXP · RMK · LANC
- OBJETIVO: VENDAS · LEADS · CONVERSAS · TRAFEGO · ENGAJ
- ESTRUTURA: ASC (Advantage+ Sales) · CBO · ABO · CAT (catálogo)
Ex.: `CORE-VENDAS-OCULOS-SOL-ASC-202609-v1`

## CONJUNTO
`[PUBLICO]-[LOCAL]-[EVENTO]-[LANCE]`
- PUBLICO: BROAD · ADV (Advantage+ Audience) · RMK-7 / RMK-30 · CLIENTES · EXCL-<x>
- LOCAL: BR · SP · <UF> · <país>
- EVENTO: PURCHASE · ATC · LEAD · CONVERSA
- LANCE: HV (highest volume) · CC-<valor> · BC-<valor> · MR-<valor>
Ex.: `BROAD-BR-PURCHASE-HV`

## ANÚNCIO
`[FORMATO]-[CONCEITO]-[HOOK]-[ANGULO]-[CREATOR]-[IA?]-[vN]`
- FORMATO: VID916 · VID11 · IMG · CAR · CAT · DCO
- IA?: `IA` quando gerado/modificado por IA (disclosure obrigatória)
Ex.: `VID916-PROVA-SOCIAL-H03-DURABILIDADE-UGC-ANA-v2`

## PRODUCT SETS
`PS-[RANKING]-[LINHA]` → `PS-HERO-OCULOS` · `PS-CORE-ACESSORIOS` · `PS-EXCL-SEMESTOQUE`

## REGRAS
1. Sem acento, sem espaço, hífen como separador, maiúsculas.
2. `vN` sobe a cada edição de criativo/copy (novo anúncio, não edição do existente).
3. Objeto legado sem padrão: o Setup registra o mapeamento em `dados/snapshots/naming_legado.md`; renomear só com aprovação (renomear não reseta aprendizado).
4. Nome nunca contém dado pessoal, preço interno ou custo.
