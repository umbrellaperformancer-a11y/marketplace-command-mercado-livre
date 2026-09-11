---
name: "vinculador-browser-projeto"
description: "Localiza o perfil de browser correto de um projeto pelo Mercado Livre, grava um identificador persistente no localStorage e registra o vínculo em arquivos do projeto. Use antes de automações que precisem escolher entre browsers ou perfis Chrome."
---

# Vinculador de Browser do Projeto

Vincule o projeto atual a um único browser antes de executar tarefas no Mercado Livre ou em outros marketplaces.

## Regra obrigatória

Nunca comece perguntando qual browser deve ser conectado. Primeiro abra uma página do Mercado Livre em **todos os browsers/perfis disponíveis**, leia o identificador em cada um e tente fazer o match automático com o vínculo salvo no projeto. Só solicite o ID manualmente quando a varredura não produzir um match confiável.

## Identificador canônico

- Chave no `localStorage` de `mercadolivre.com.br`: `umbrella_project_browser_id`.
- Formato recomendado: `umb_<project_slug>_<uuid>`.
- O ID precisa ser exclusivo por vínculo projeto/browser e permanecer estável entre sessões.
- Não use cookies, nome visível do perfil, posição da janela ou índice temporário da conexão como identificador canônico.
- Se o conector exibir um ID estável do browser/perfil, registre-o como `connector_browser_id`, mas mantenha também o ID canônico no `localStorage`.

## Fluxo

1. Descubra todos os browsers/perfis acessíveis pelo conector do navegador.
2. Em cada um, abra ou reutilize uma aba em `https://www.mercadolivre.com.br/`.
3. Em cada aba, execute `localStorage.getItem('umbrella_project_browser_id')` no contexto da página.
4. Leia, se existirem, `.browser-link.json` e `VINCULO_BROWSER.md` na raiz do projeto.
5. Compare todos os IDs encontrados com `project_browser_id` já registrado:
   - um único match: selecione esse browser automaticamente;
   - nenhum match, mas existe somente um browser: peça o ID exibido pelo conector ou autorização para gerar um novo ID e grave o vínculo;
   - nenhum match e existem vários browsers: apresente os candidatos e peça somente a escolha necessária;
   - mais de um match do mesmo ID: pare, informe a duplicidade e peça qual browser deve permanecer vinculado.
6. Em vínculo novo, gere um UUID e grave no escolhido com `localStorage.setItem('umbrella_project_browser_id', '<ID_GERADO>')`.
7. Releia a chave no mesmo browser e continue somente se o valor for idêntico.
8. Crie ou atualize os arquivos de [references/registro.md](references/registro.md).
9. Confirme brevemente: projeto, browser, ID e resultado da validação.

## Regras de consistência

- Não altere IDs de browsers que não foram escolhidos.
- Não crie um ID se já houver match válido.
- Login do Mercado Livre não prova o vínculo: contas iguais podem estar abertas em perfis diferentes.
- Execute leitura e gravação em `mercadolivre.com.br`, pois o `localStorage` é isolado por origem.
- Se scripts forem bloqueados, use o ID estável do conector como fallback e registre `storage_status: unavailable`.
- Depois do vínculo, outras skills devem consultar `.browser-link.json` antes de pedir seleção manual.

## Saída esperada

Deixe na raiz do projeto:

- `.browser-link.json`: registro para leitura automática.
- `VINCULO_BROWSER.md`: documento legível e instruções de recuperação.

Leia [references/registro.md](references/registro.md) antes de criar ou atualizar esses arquivos.
