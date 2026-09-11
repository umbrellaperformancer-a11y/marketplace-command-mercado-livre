---
name: "regras-amazon"
description: "Regras específicas da Amazon Brasil para as lojas do programa. SEMPRE aplique em qualquer tarefa de Amazon — define os painéis do Seller Central, as mecânicas próprias da Amazon (tarifa de indicação, Oferta em Destaque/Buy Box, A9/A10, FBA/DBA/FBM, Account Health, Ads) e as regras de operação (coleta pelo Chrome e aprovação obrigatória do dono da loja antes de aplicar qualquer mudança). Identidade da loja vem da config do projeto. Herda o sistema-operacional-amazon. Use APENAS para Amazon — NÃO use para Mercado Livre nem Shopee."
---

# 🟠 REGRAS — AMAZON BRASIL (motor compartilhado)

Valem para qualquer loja Amazon do programa. A identidade da loja (conta, marca, catálogo, concorrente, pastas, Chrome/deviceId) vem da **config do projeto ativo**, não daqui. Todos os agentes `*-amazon` leem este skill primeiro.

## 1. COLETA DE DADOS — AUTOMÁTICA PELO CHROME
- **Use a extensão do Chrome** para abrir o Seller Central e puxar os dados ao vivo. **NÃO pergunte a fonte** — vá direto ao Chrome da loja ativa (deviceId da config).
- **1 loja = 1 Chrome.** Tudo da loja roda no mesmo Chrome: coletar, gerar imagem e publicar.
- Painel fora do ar ou pedindo login? **Avise e siga com o que conseguir** (parcial > nada).
- **Nunca invente número.** Sem dado real, marque "a confirmar".

## 2. APLICAÇÃO DE MUDANÇAS — SEMPRE COM APROVAÇÃO
- **NUNCA** publique/edite anúncio, mude preço, ligue/desligue promoção ou campanha, mude orçamento, crie/cancele remessa FBA ou responda caso de Account Health **sem o dono da loja autorizar.**
- Antes de aplicar, preview: **item + valor atual → novo valor + impacto estimado em R$** — e espere o **"pode aplicar"**.
- Uma ação de cada vez; lote só com autorização explícita.
- Pode coletar, analisar e preencher formulário — mas **pare antes de clicar** em Salvar/Publicar/Confirmar/Enviar/Excluir.
- **Nunca toque** em dados bancários, cartão, documentos fiscais ou configurações de conta/2FA.
- Antes de qualquer ação irreversível confirme: **navegador certo · Amazon · loja certa · pasta certa.**
- ⚠️ Amazon é a plataforma mais rígida dos 3 marketplaces: erro de política pode **suspender a conta**. Na dúvida entre agressivo e seguro, escolha o seguro e consulte o agente de Reputação.

## 3. PAINÉIS DO SELLER CENTRAL (iguais para qualquer loja)
Base: `https://sellercentral.amazon.com.br`
- Início / Painel: `/home`
- Gerenciar Inventário: `/inventory`
- Adicionar produto: `/abis/listing/syh`
- Preços / Painel de Preços: `/pricing/dashboard`
- Oferta em Destaque (Buy Box) e alertas de preço: dentro do Painel de Preços
- Promoções / Ofertas (Deals): `/merchandising`
- Cupons: `/cpn/dashboard`
- Publicidade (Ads): `https://advertising.amazon.com.br` (campanhas SP/SB/SD)
- Relatórios de Negócios (Business Reports): `/business-reports` — sessões, unidades, USP%
- Desempenho da Conta (Account Health): `/performance/dashboard`
- Voz do Cliente (Voice of the Customer): `/voice-of-the-customer`
- Feedback e Avaliações: `/feedback-manager`
- Remessas FBA: `/fba/sendtoamazon`
- Planejamento de estoque FBA / IPI: `/inventory-planning`
- Brand Analytics + Search Query Performance (exige Brand Registry): menu Marcas
- Gerenciar Experimentos (A/B, exige Brand Registry): menu Marcas
- Conteúdo A+ : `/enhanced-content`
- Loja da marca (Store): via menu Marcas / Amazon Ads
- Atendimento (mensagens do comprador): `/messaging`
> URLs mudam de vez em quando — se um caminho falhar, navegue pelo menu do Seller Central.

## 4. MECÂNICAS PRÓPRIAS DA AMAZON (o que a difere de ML/Shopee)
- **Catálogo único por ASIN**: você não "cria um anúncio", você cria/entra numa **página de produto (ASIN)**. Vários vendedores podem disputar o MESMO ASIN — quem vence leva a **Oferta em Destaque (Buy Box)**, onde acontecem ~80%+ das vendas.
- **Oferta em Destaque** é decidida por algoritmo: preço total (item+frete), método de entrega (FBA/DBA pesam muito), Account Health, prazo, estoque, histórico. Não é leilão de preço puro.
- **Tarifas**: mensalidade do plano Profissional (~R$19/mês) + **tarifa de indicação por categoria** (na maioria das categorias entre 8% e 15% — **confirme a tarifa exata da categoria no Seller Central antes de qualquer conta de margem**) + custos FBA quando aplicável.
- **Logística no Brasil**: **FBA** (estoque no CD da Amazon, ganha selo Prime, força máxima na Buy Box) · **DBA/Enviado pela Amazon** (você estoca, Amazon coleta/entrega) · **FBM** (você envia). Prioridade competitiva: FBA > DBA > FBM.
- **Algoritmo A9/A10**: rankeia por relevância (palavra-chave indexada em título, bullets, descrição, termos de busca de backend) × performance (CTR, conversão/CVR, vendas, velocidade de venda, avaliações, disponibilidade). Sem indexar, não existe; sem converter, não sobe.
- **Account Health é vida ou morte**: ODR (taxa de pedidos com defeito) **< 1%** · cancelamento pré-envio **< 2,5%** · envio atrasado **< 4%** · rastreio válido **≥ 95%**. Estourar = risco real de suspensão. Toda decisão passa por esse filtro.
- **Reviews**: proibido pedir avaliação positiva, oferecer brinde por review ou manipular. Permitido: botão "Solicitar avaliação", programa **Vine** (exige Brand Registry). Violação = suspensão.
- **Brand Registry** destrava o arsenal: A+, Brand Story, Store, Sponsored Brands/Display, Brand Analytics, Search Query Performance, Experimentos, Vine, proteção de marca. Registrar a marca é prioridade estratégica nº1 de quem tem marca própria.
- **Eventos**: Prime Day, Black Friday, Cyber Monday, datas sazonais — exigem inscrição antecipada de Deals e estoque FBA posicionado semanas antes.

## 5. PARÂMETROS-PADRÃO DA OPERAÇÃO AMAZON (sobrescreva na config da loja)
- **Margem**: piso **30%** de margem líquida no preço normal e em Ads; promoção pode furar para girar estoque, bloqueio só abaixo de **5%**; base estimada 40% até o setup gravar o CMV real em `dados/base_custos.md` (fonte oficial de custos).
- **Ads**: ACOS-alvo por fase — lançamento 25–40% (comprando ranking) · crescimento 15–25% · maturidade ≤ 15%; **TACOS saudável 5–10%** e caindo com o orgânico subindo; orçamento inicial R$20–30/dia por campanha; toda mudança de lance espera **7 dias de dados** antes de nova mudança.
- **Estoque**: colchão de segurança +30%; previsão de demanda a cada 7 dias; FBA com cobertura-alvo de 30–60 dias (nem ruptura, nem taxa de armazenagem prolongada).
- **Preço**: nunca abaixo do preço mínimo do Financeiro; repricing sempre com piso travado.

## 6. REGISTRO NO DIÁRIO DE BORDO
Sempre que APLICAR uma ação aprovada, gere no final da resposta:
```
AAAA-MM-DD | Agente | o que foi feito | antes → depois | impacto | status
```
- Agentes válidos: Comitê, Ads, Estoque, FBA, Promoções, Anúncios, Criador de Anúncio, Buy Box, Financeiro, Reputação, Competitividade, Diretor Comercial, Diretor Criativo, Growth, Dashboard.
- **status**: `aplicado` · `recomendado` · `pendente`.
- Quando pedirem "fecha o diário" / "o que fizemos hoje?": responda **APENAS as linhas com `|`** em bloco de código (resumo em texto só depois, separado).

## 7. ESTILO DE RESPOSTA
- Português brasileiro, direto. Toda recomendação com: o que fazer, por quê, impacto em R$, prioridade, quem executa.
- Termine oferecendo a próxima ação ("pode aplicar?" / "por onde quer começar?").

## CONTEXTO QUE VEM DA CONFIG DO PROJETO (não fixar aqui)
Loja · e-mail da conta · marca / Brand Registry (sim/não) · categoria e tarifa de indicação real · nº de SKUs/ASINs · programa logístico (FBA/DBA/FBM) · CMV por SKU · concorrente direto · metas · pastas de saída · Chrome (deviceId).
