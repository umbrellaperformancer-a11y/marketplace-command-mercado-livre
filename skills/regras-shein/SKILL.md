---
name: regras-shein
description: Regras específicas da SHEIN Marketplace para as lojas da operação. Use em qualquer tarefa de SHEIN — define os painéis (Seller Hub / Central do Vendedor SHEIN) e as mecânicas próprias da SHEIN (comissão 16%, SFS/fulfillment, campanhas e flash sales, desempenho do vendedor, devoluções de moda, repasse). Identidade da loja vem da ficha do projeto. Use APENAS para SHEIN — NÃO use para Mercado Livre, Shopee, TikTok Shop nem Amazon.
---

# 🖤 REGRAS — SHEIN MARKETPLACE (motor compartilhado)

Valem para qualquer loja de SHEIN da operação. A identidade da loja (conta, nome, URL, concorrente, pastas, Chrome) vem da **ficha do projeto ativo**. As regras de aprovação, coleta via Chrome e diário estão em `regras-comuns`. A arquitetura do cérebro (hierarquia, protocolos, criticidade, auditoria, memória, aprendizado) está no KERNEL `sistema-operacional-shein` — todo agente `agente-*-shein` herda o kernel + estas regras.

> ⚠️ A SHEIN Marketplace Brasil é jovem e muda rápido (taxas, programas, painéis, incentivos). **Sempre confira o número real no Seller Hub antes de fechar preço/margem.** Os valores abaixo são a referência gravada — quando a tela divergir, **a tela vence**, o Financeiro recalcula e o `agente-radar-shein` atualiza esta skill.

## 🧠 A LÓGICA DA SHEIN É DIFERENTE (moda + tendência + campanha)
No ML o cliente busca o produto exato; no TikTok o produto encontra o cliente. Na SHEIN o cliente **navega moda**: entra pra descobrir tendência, roda feed, categoria e campanha, compra por impulso visual e preço. Consequências pra TODO agente:
- **A curadoria da plataforma decide exposição:** campanhas, flash sales, etiquetas de destaque e posicionamento valem mais que SEO puro. Estar na campanha certa com o produto certo é o jogo.
- **Tendência é matéria-prima:** catálogo parado envelhece em semanas. Quem lê a tendência antes (Tendências) e lança rápido (Criador) ganha a janela.
- **Foto vende, medida segura:** a foto padrão moda converte; a ficha de medidas/atributos completa é o que impede a devolução — e devolução em moda é o assassino silencioso da margem.
- **Grade é tudo:** tamanho×cor. A grade quebrada (P e M zerados, GG sobrando) mata a conversão do anúncio inteiro e engorda o estoque parado.

## PAINEL PRINCIPAL — SELLER HUB (Central do Vendedor SHEIN)
Tudo passa pelo **Seller Hub**. Áreas-chave (nomes podem variar por atualização — confirmar na tela):
- **Produtos / Catálogo** — cadastro, grades, atributos, imagens, status de aprovação
- **Pedidos** — processamento, prazo de despacho, etiquetas
- **Marketing / Campanhas / Promoções** — inscrição em campanhas, flash sales, cupons e (quando disponível na conta) listagens patrocinadas
- **Dados / Desempenho** — vendas, tráfego, conversão, desempenho da loja e do produto
- **Financeiro / Liquidação** — repasses, comissões cobradas por pedido, histórico
- **Logística / Envio** — envio próprio, agendamento de coleta, SFS
- **Gestão de Notas Fiscais** — NF-e das vendas (inclusive SFS)
- **SHEIN University** — treinamentos e regras oficiais

## CADASTRO E FISCAL
- **CNPJ obrigatório** para vender na SHEIN Brasil (a exigência substituiu o cadastro por CPF).
- **NF-e por pedido** é obrigatória. Para operar o SFS, exige-se **certificado digital A1** vinculado (comunicação fiscal automática).
- Foco de catálogo: **moda, vestuário, calçados, acessórios (inclui óculos), beleza e lifestyle** — categorias fora desse eixo podem ter restrição; confirmar antes de planejar linha nova.

## TAXAS (referência — confirmar no Seller Hub)
- **Comissão = (preço da mercadoria − cupons − descontos) × 16%.** Incide sobre o valor final pago pelo cliente.
- Comissão cobrada **apenas em pedido processado e entregue**; cancelamento/devolução/reembolso = comissão devolvida ao vendedor.
- **Sem tarifa fixa por item e sem taxa de anúncio** (diferencial vs Shopee/ML — torna ticket baixo mais viável). ⚠️ Tratar como item de conferência: se a tela mostrar taxa fixa, tarifa de frete grátis ou comissão diferente de 16% (há relatos de faixas de 18–20% em 2026), **a tela vence**.
- **Isenção de comissão para novos vendedores** (fontes divergem: 30 ou 90 dias, com CNPJ). É temporário — **não embutir no preço-base**; conferir a data de fim na conta.
- Usando **SFS**: soma-se a **taxa de operação logística do SFS** (armazenagem/manuseio/frete conforme contrato) — pegar o valor real no painel antes de precificar.

## REPASSE (ciclo de pagamento)
- Referência: **ciclo de pagamento semanal** (fontes citam também prazos de até ~30 dias conforme modelo/política vigente) — **confirmar o ciclo real da conta no painel Financeiro** e usar esse número no fluxo de caixa.
- Conciliar sempre: repasse real × estimado (comissão devolvida de cancelados entra na conta).

## LOGÍSTICA (Brasil)
Modelo misto — dois modos:
- **Envio pelo vendedor:** o vendedor processa e despacha no prazo da plataforma (despacho rápido é exigência; atraso derruba desempenho). Coleta/agendamento conforme configuração da conta.
- **SFS — SHEIN Fulfillment Service:** estoque nos CDs da SHEIN (rede em SP — Guarulhos e região). A SHEIN armazena, embala e envia. Benefícios relatados: **etiquetas de destaque e até ~6× mais tráfego**, melhor posição de busca, acesso a **campanhas exclusivas**, entrega mais rápida, risco de atraso de despacho eliminado. Estoque no SFS zerou → a oferta **reverte automaticamente** pro envio do vendedor. Devolução não recebida volta ao estoque do CD; recebida e devolvida volta ao vendedor.
- **Logística reversa:** rede de pontos de coleta (parceria com transportadoras/Pontos Pickup, QR code sem etiqueta) — devolução é fácil pro cliente; conte com ela no planejamento.

## DESEMPENHO DO VENDEDOR (reputação)
- A SHEIN **monitora de perto**: prazo de despacho, estoque atualizado, cancelamentos, atrasos, divergência anúncio×produto, qualidade/avaliações e taxa de devolução.
- Falhas geram **penalizações progressivas**: perda de visibilidade, exclusão de campanhas, restrições e — em violação de política/termos — **suspensão da conta**. O detalhamento de faixas/pontos não é público e estável: **o `agente-reputacao-shein` mapeia as métricas e sanções REAIS no painel de Desempenho da conta** e o Radar mantém esta seção atualizada.
- Pecados capitais na SHEIN: **cancelar por falta de estoque** e **atrasar despacho** — os dois derrubam ranking e fecham porta de campanha.

## MARKETING E CRESCIMENTO (alavancas da plataforma)
- **Campanhas da SHEIN** (temáticas/sazonais, com inscrição de produtos), **flash sales / vendas relâmpago**, **cupons** e **posicionamentos em destaque** — o motor principal de tráfego do marketplace.
- **Listagens patrocinadas (Ads)** — disponibilidade e formato variam por conta/fase do programa; o `agente-ads-shein` confirma na tela o que existe antes de planejar verba.
- **Transmissões ao vivo / conteúdo da SHEIN** — produtos de vendedores podem ser destacados em lives e ações de conteúdo da plataforma; entrada geralmente via campanha/convite.
- **SFS como alavanca de marketing:** além de logística, é elegibilidade pra campanha e etiqueta — tratar a decisão de mandar estoque pro SFS como decisão comercial, não só logística.

## 🧬 DNA OPERACIONAL (metas da operação na SHEIN — guardadas pelo Orquestrador)
- **Ruptura ≤ 2% por grade** · **Despacho < 24h** · **Cancelamento < 2%** · **Avaliação > 4.7** · **Taxa de devolução por SKU vigiada contra a média da categoria** (moda devolve mais — o que importa é estar ABAIXO da média e caindo).
- Jamais permitir: venda sem estoque na grade, pedido vencendo prazo de despacho, produto em campanha sem estoque reforçado, anúncio com medida/atributo faltando, foto fora do padrão.

## POLÍTICA DE MARGEM
Vale o piso da operação (`regras-comuns`): **mínimo 30%** no preço normal, base **40%**, promoção é exceção (barra só < 5%). **Conta completa da SHEIN:** preço − 16% comissão − frete/custo logístico (ou taxa SFS) − imposto − CMV − custo de campanha/Ads rateado. Cupom/desconto reduz a base da comissão (16% sobre o valor final) — a conta considera isso.

## CONTEXTO QUE VEM DA FICHA DO PROJETO (não fixar aqui)
Loja · conta SHEIN · URL da loja · categoria principal · concorrente · nº de SKUs · CNPJ · usa SFS? · pastas de saída · Chrome (deviceId).

---
_Changelog: v1.0 — criação da skill (referências de mercado 2024–2026; itens marcados "confirmar na tela" pendentes da 1ª auditoria do agente-radar-shein na conta real)._
