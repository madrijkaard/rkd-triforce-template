# exportar_especificacao_drive

Use quando for exportar o diretório spec do rkd-triade-template para o Google Drive, dentro da pasta rkd-triade-template, renomeando com o nome do projeto e data/hora.

No `rkd-triade-template`, a pasta `spec` guarda os documentos de especificação usados para gerar o código do projeto que esteve (ou está) em `src`. Esta skill copia o **conteúdo de `spec`** para o Google Drive numa pasta nova com nomenclatura própria — não sobe a pasta com o nome literal `spec`.

## Pré-requisitos

- Conector Google Drive conectado e utilizável.
- Pasta local `rkd-triade-template/spec` existente. Se estiver vazia ou ausente, avise e pare.

## Nome do projeto (obrigatório)

Antes de qualquer upload, **pergunte no chat** qual é o `NOME_DO_PROJETO` que entra na nomenclatura da pasta no Drive.

- Não invente o nome.
- Não prossiga com create/upload até o usuário digitar o nome no chat.
- Aceite o texto que ele enviar como `NOME_DO_PROJETO` (sanitize só o necessário para um nome de pasta válido no Drive: evite `/` e caracteres que o Drive rejeitar; preserve o restante).

## Pasta pai no Drive

Todas as exportações ficam **dentro** de uma pasta chamada exatamente:

```text
rkd-triade-template
```

- Se essa pasta já existir no Meu Drive, reutilize-a (busque por nome e use o `folderId` encontrado).
- Se não existir, crie-a uma vez na raiz do Meu Drive e use o id retornado.
- Nunca crie a pasta `spec_…` na raiz do Drive; ela deve ser filha de `rkd-triade-template`.

## Nomenclatura da pasta de exportação

Dentro de `rkd-triade-template`, crie **uma pasta nova** com o nome exato:

```text
spec_NOME_DO_PROJETO_data_yyyy_mm_dd_hh:mm
```

Regras:

- Prefixo fixo: `spec_`
- Em seguida o `NOME_DO_PROJETO` informado pelo usuário
- Depois o literal `_data_`
- Depois data e hora locais do usuário (`America/Sao_Paulo`), no formato `yyyy_mm_dd_hh:mm` (hora e minuto com dois dígitos; o `:` entre hora e minuto faz parte do padrão pedido)
- Exemplo: se o projeto for `sivem-core` e for 2026-10-05 13:36 (UTC-3), o caminho no Drive fica `rkd-triade-template/spec_sivem-core_data_2026_10_05_13:36`

Não use o nome `spec` sozinho no Drive.

## O que exportar

1. Liste os arquivos (e subpastas, se houver) em `rkd-triade-template/spec`.
2. Garanta a pasta pai `rkd-triade-template` no Drive (reutilizar ou criar).
3. Crie a pasta de exportação com a nomenclatura acima **como filha** de `rkd-triade-template` (`create_folder` com `parentId` dessa pasta pai).
4. Envie **todos** os documentos de especificação da pasta local `spec` para dentro dessa pasta de exportação, preservando nomes de arquivo e, se houver subpastas, a estrutura relativa.
5. Use as ferramentas do conector Google Drive. Para conteúdo binário grande, use o fluxo de upload suportado pelo ambiente; não cole bytes no chat.
6. Não apague nem altere os arquivos locais em `spec`.
7. Não faça commit nem push por causa desta exportação.

## Depois

Informe:

- o `NOME_DO_PROJETO` usado
- o caminho no Drive: `rkd-triade-template/<nome da pasta de exportação>`
- link da pasta de exportação (se a API devolver)
- quantos arquivos foram enviados

Se o Drive não estiver autenticado, ofereça autenticar o conector e só continue após a autorização.
