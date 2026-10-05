# importar_especificacao_drive

Use quando for importar do Google Drive uma pasta de especificação (spec_NOME_DO_PROJETO_data_…) para o diretório spec local do rkd-triade-template.

No `rkd-triade-template`, a pasta local `spec` recebe os documentos de especificação que vão orientar o trabalho no código em `src`. Esta skill **baixa** do Google Drive o conteúdo de uma pasta de exportação criada pela skill `exportar_especificacao_drive` e coloca esse conteúdo em `rkd-triade-template/spec`.

## Pré-requisitos

- Conector Google Drive conectado e utilizável.
- Pasta local do template em `/workspace/rkd-triade-template` (ou o caminho equivalente do workspace).

## Pasta pai no Drive

Todas as exportações ficam **dentro** de uma pasta chamada exatamente:

```text
rkd-triade-template
```

1. Busque essa pasta no Meu Drive pelo nome.
2. Se **não existir**, pare e diga ao usuário que atualmente **não existe nenhum documento de especificação para ser importado** (nunca houve exportação via `exportar_especificacao_drive`). Não pergunte nome de projeto nesse caso.
3. Se existir, use o `folderId` dela para listar as pastas filhas.

## Passo 1 — Distinct de `NOME_DO_PROJETO`

Liste as pastas filhas de `rkd-triade-template` cujo nome segue o padrão:

```text
spec_NOME_DO_PROJETO_data_yyyy_mm_dd_hh:mm
```

Regras de parse:

- Prefixo obrigatório: `spec_`
- Sufixo obrigatório: `_data_` + `yyyy_mm_dd_hh:mm` (hora e minuto com dois dígitos; o `:` entre hora e minuto faz parte do padrão)
- O trecho entre `spec_` e `_data_` é o `NOME_DO_PROJETO`
- Ignore pastas que não casarem com esse padrão

Faça um **distinct** dos `NOME_DO_PROJETO` encontrados (cada nome aparece uma vez na lista, mesmo que haja várias datas).

Se não houver nenhuma pasta válida (ou a pasta pai estiver vazia), diga que atualmente **não existe nenhum documento de especificação para ser importado** e pare.

Caso contrário, **liste os nomes distintos** e **pergunte no chat** qual `NOME_DO_PROJETO` o usuário quer importar. Use um widget com uma opção por nome quando couber; se forem muitos, liste em texto e peça a confirmação. **Não invente nomes** e **não prossiga** até o usuário confirmar um dos nomes listados.

## Passo 2 — Listar versões daquele projeto

Com o `NOME_DO_PROJETO` confirmado:

1. Filtre as pastas filhas cujo nome começa com `spec_<NOME_DO_PROJETO>_data_`.
2. Se **não houver nenhuma** para esse nome (por exemplo o usuário digitou um nome que não estava na lista), diga que atualmente **não existe nenhum documento de especificação para ser importado no projeto NOME_DO_PROJETO** e pare.
3. Liste **todas** as pastas `spec_NOME_DO_PROJETO_data_yyyy_mm_dd_hh:mm` disponíveis para esse projeto (de preferência da mais recente para a mais antiga, se a data/hora no nome permitir ordenar).
4. Pergunte qual pasta exata importar. Espere a confirmação do usuário. Não baixe nada até ele confirmar o nome completo da pasta.

## Passo 3 — Importar para `spec` local

Com a pasta `spec_NOME_DO_PROJETO_data_yyyy_mm_dd_hh:mm` confirmada:

1. Garanta que a pasta local `rkd-triade-template/spec` exista; se não existir, crie-a.
2. **Substitua o conteúdo** de `spec` pelo conteúdo interno da pasta escolhida no Drive:
   - Remova o conteúdo atual de `spec` (arquivos e subpastas), **sem** apagar a própria pasta `spec`.
   - Baixe **todos** os arquivos e subpastas de dentro da pasta de exportação no Drive e coloque-os em `spec`, preservando nomes e a estrutura relativa.
3. Use as ferramentas do conector Google Drive (e o fluxo de download suportado pelo ambiente para arquivos grandes). Não cole bytes no chat.
4. Não altere nem apague nada no Google Drive.
5. Não faça commit nem push por causa desta importação.

## Depois

Informe:

- o `NOME_DO_PROJETO` escolhido
- a pasta do Drive importada: `rkd-triade-template/<nome completo da pasta>`
- quantos arquivos foram trazidos para `spec`
- que a pasta local `spec` está pronta para o trabalho com o código em `src`

Se o Drive não estiver autenticado, ofereça autenticar o conector e só continue após a autorização.
