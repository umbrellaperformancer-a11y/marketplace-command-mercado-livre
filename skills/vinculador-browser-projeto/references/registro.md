# Registro do vínculo

Crie os arquivos abaixo na raiz do projeto. Preserve campos adicionais existentes ao atualizar.

## `.browser-link.json`

```json
{
  "schema_version": 1,
  "project_name": "NOME_DO_PROJETO",
  "project_browser_id": "umb_slug_uuid",
  "connector_browser_id": "ID_DO_CONECTOR_OU_NULL",
  "browser_label": "NOME_VISIVEL_OU_NULL",
  "verification_origin": "https://www.mercadolivre.com.br",
  "local_storage_key": "umbrella_project_browser_id",
  "storage_status": "verified",
  "verified_at": "DATA_ISO_8601",
  "last_match_status": "matched|created|manual-fallback"
}
```

Use JSON válido e `null` sem aspas quando o valor não existir.

## `VINCULO_BROWSER.md`

```markdown
# Vínculo do Browser

- Projeto: NOME_DO_PROJETO
- Browser/perfil: NOME_VISÍVEL
- ID do projeto no browser: ID
- ID do conector: ID OU “não disponível”
- Domínio de validação: https://www.mercadolivre.com.br
- Status: verificado
- Última validação: DATA/HORA

## Como validar

Abra o Mercado Livre no browser e compare a chave `umbrella_project_browser_id` do `localStorage` com `project_browser_id` do arquivo `.browser-link.json`.

## Recuperação

Se não houver match, execute novamente `/vinculador-browser-projeto`. Não substitua o vínculo sem confirmar o browser correto.
```

## Atualização

- Atualize `verified_at`, `last_match_status`, rótulo e ID do conector após nova validação.
- Preserve `project_browser_id` enquanto o vínculo continuar válido.
- Em troca deliberada de browser, registre no final de `VINCULO_BROWSER.md` a data, o ID anterior e o novo.
