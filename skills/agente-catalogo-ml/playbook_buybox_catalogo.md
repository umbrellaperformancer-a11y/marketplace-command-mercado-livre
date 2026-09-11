# 🏆 PLAYBOOK — BUY BOX E CATÁLOGO DO ML

A mecânica mais mal-entendida do ML — e a que mais move venda. Uso: ao criar anúncio, ao auditar, e sempre que "minhas vendas sumiram do nada".

## COMO FUNCIONA
No ML existem 2 mundos: o **anúncio tradicional** (seu, sua página, sua reputação de anúncio) e o **catálogo** (página ÚNICA por produto, onde vários vendedores disputam quem aparece como vencedor — o **Buy Box**). Quem vence leva ~quase todas as vendas daquela página; os outros ficam no "outras opções de compra".

## OS FATORES DA DISPUTA (o que decide o vencedor)
1. **Preço final** (produto + frete pro comprador) — o fator de maior peso. Centavos decidem.
2. **Reputação/nível** — verde escuro compete; amarelo pra baixo praticamente não vence (reputação é pré-requisito, cruza `agente-reputacao-ml`).
3. **Envio** — Full vence desempate (entrega mais rápida = pontos); Flex também pontua bem.
4. **Parcelamento sem juros** — oferecer 12x sem juros melhora a oferta (mas TEM CUSTO: validar com o Financeiro se a margem paga).
5. **Estoque disponível** — sem estoque, fora da disputa.

## QUANDO ENTRAR NO CATÁLOGO (e quando fugir)
**Entrar:** produto commodity/idêntico ao dos concorrentes (mesmo modelo, mesma marca) — a página de catálogo concentra o tráfego; ficar fora é invisibilidade.
**Fugir (ficar só no tradicional):** produto diferenciado, marca própria, kit exclusivo — no catálogo você vira comparação de preço puro; no tradicional você vende valor (fotos, descrição, marca).
**Estratégia dupla:** campeão commodity → catálogo (disputar Buy Box) + anúncio tradicional (capturar busca de marca). Não competem entre si: somam.

## OPERANDO A DISPUTA
- Perdeu o Buy Box → diagnóstico na ordem: preço final (incluindo frete) → reputação/termômetro → tipo de envio → estoque. O painel mostra o motivo/concorrente vencedor.
- Recuperar por preço: SÓ dentro da tabela de margem (`agente-financeiro-ml`) — Buy Box no prejuízo é derrota disfarçada de vitória. Alternativas antes de baixar preço: ativar Full no SKU, melhorar parcelamento, cupom (mantém preço cheio).
- Vigiar: concorrente ganhando por 50 centavos é sinal de guerra de margem — chame o Competitividade/Diretor Comercial antes de entrar na espiral.

## SINAL CLÁSSICO
"Minhas vendas do SKU X sumiram de um dia pro outro, visitas caíram junto" → 90% das vezes: perdeu o Buy Box ou o catálogo ganhou um vendedor mais agressivo. Checar a página de catálogo ANTES de mexer em Ads ou título.
