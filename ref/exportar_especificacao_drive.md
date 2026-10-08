# exportar_especificacao_drive

Use quando for exportar o diretório spec do rkd-triforce-template para o Google Drive, em rkd-triforce-template/NOME_DO_PROJETO/spec_NOME_DO_PROJETO_yyyy_mm_dd_hh:mm.

No `rkd-triforce-template`, a pasta `spec` guarda os documentos de especificação usados para gerar o código do projeto que esteve (ou está) em `src`. Esta skill copia o **conteúdo de `spec`** para o Google Drive numa pasta nova com nomenclatura própria — não sobe a pasta com o nome literal `spec`.

## Pré-requisitos

- Conector Google Drive conectado e utilizável.
- Pasta local `rkd-triforce-template/spec` existente. Se estiver vazia ou ausente, avise e pare.

## Nome do projeto (obrigatório)

Antes de qualquer upload, **pergunte no chat** qual é o `NOME_DO_PROJETO` que entra na nomenclatura da pasta no Drive.

- Não invente o nome.
- Não prossiga com create/upload até o usuário digitar o nome no chat.
- Aceite o texto que ele enviar como `NOME_DO_PROJETO` (sanitize só o necessário para um nome de pasta válido no Drive: evite `/` e caracteres que o Drive rejeitar; preserve o restante).

## Hierarquia no Drive

Uma exportação bem-sucedida fica neste caminho:

```text
rkd-triforce-template/NOME_DO_PROJETO/spec_NOME_DO_PROJETO_yyyy_mm_dd_hh:mm
```

### 1. Pasta raiz `rkd-triforce-template`

- Se já existir no Meu Drive, reutilize-a (busque por nome e use o `folderId`).
- Se não existir, crie-a uma vez na raiz do Meu Drive e use o id retornado.

### 2. Pasta do projeto `NOME_DO_PROJETO`

Dentro de `rkd-triforce-template`, verifique se já existe uma pasta filha com o **nome exatamente igual** ao `NOME_DO_PROJETO` informado.

- Se existir, reutilize o `folderId` dela.
- Se **não** existir, crie a pasta `NOME_DO_PROJETO` como filha de `rkd-triforce-template` e use o id retornado.
- Todas as exportações daquele projeto (atuais e futuras) ficam **dentro** dessa pasta de projeto.

### 3. Pasta de exportação `spec_…`

Dentro de `NOME_DO_PROJETO`, crie **sempre uma pasta nova** com o nome exato:

```text
spec_NOME_DO_PROJETO_yyyy_mm_dd_hh:mm
```

Regras:

- Prefixo fixo: `spec_`
- Em seguida o `NOME_DO_PROJETO` informado pelo usuário
- Depois `_` e a data/hora locais do usuário (`America/Sao_Paulo`), no formato `yyyy_mm_dd_hh:mm` (hora e minuto com dois dígitos; o `:` entre hora e minuto faz parte do padrão pedido)
- **Não** use o literal `_data_` no nome
- Exemplo: se o projeto for `sivem-core` e for 2026-10-05 20:04 (UTC-3), o caminho no Drive fica `rkd-triforce-template/sivem-core/spec_sivem-core_2026_10_05_20:04`

Nunca crie a pasta `spec_…` na raiz do Drive nem como filha direta de `rkd-triforce-template`; ela deve ser filha de `NOME_DO_PROJETO`.
Não use o nome `spec` sozinho no Drive.

## O que exportar

1. Liste os arquivos (e subpastas, se houver) em `rkd-triforce-template/spec`.
2. Garanta a pasta `rkd-triforce-template` no Drive (reutilizar ou criar).
3. Garanta a pasta `NOME_DO_PROJETO` **dentro** de `rkd-triforce-template` (reutilizar se o nome for exatamente igual; senão criar).
4. Crie a pasta de exportação com a nomenclatura `spec_…` **como filha** de `NOME_DO_PROJETO` (`create_folder` com `parentId` da pasta do projeto).
5. Envie **todos** os documentos de especificação da pasta local `spec` para dentro dessa pasta de exportação, preservando nomes de arquivo e, se houver subpastas, a estrutura relativa.
6. Use as ferramentas do conector Google Drive. Para conteúdo binário grande, use o fluxo de upload suportado pelo ambiente; não cole bytes no chat.
7. Não apague nem altere os arquivos locais em `spec`.
8. Não faça commit nem push por causa desta exportação.

## Depois

Informe:

- o `NOME_DO_PROJETO` usado
- o caminho no Drive: `rkd-triforce-template/NOME_DO_PROJETO/<nome da pasta de exportação>`
- link da pasta de exportação (se a API devolver)
- quantos arquivos foram enviados

Se o Drive não estiver autenticado, ofereça autenticar o conector e só continue após a autorização.
