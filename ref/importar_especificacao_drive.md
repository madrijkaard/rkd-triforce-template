# importar_especificacao_drive

Use quando for importar do Google Drive uma pasta de especificação (rkd-triade-template/NOME_DO_PROJETO/spec_…) para o diretório spec local do rkd-triade-template.

No `rkd-triade-template`, a pasta local `spec` recebe os documentos de especificação que vão orientar o trabalho no código em `src`. Esta skill **baixa** do Google Drive o conteúdo de uma pasta de exportação criada pela skill `exportar_especificacao_drive` e coloca esse conteúdo em `rkd-triade-template/spec`.

## Pré-requisitos

- Conector Google Drive conectado e utilizável.
- Pasta local do template em `/workspace/rkd-triade-template` (ou o caminho equivalente do workspace).

## Hierarquia no Drive

As exportações ficam em:

```text
rkd-triade-template/NOME_DO_PROJETO/spec_NOME_DO_PROJETO_yyyy_mm_dd_hh:mm
```

## Pasta raiz `rkd-triade-template`

1. Busque essa pasta no Meu Drive pelo nome exato `rkd-triade-template`.
2. Se **não existir**, pare e diga ao usuário que atualmente **não existe nenhum documento de especificação para ser importado** (nunca houve exportação via `exportar_especificacao_drive`). Não pergunte nome de projeto nesse caso.
3. Se existir, use o `folderId` dela para listar as pastas filhas (cada filha deve ser um `NOME_DO_PROJETO`).

## Passo 1 — Distinct de `NOME_DO_PROJETO`

Liste as **pastas filhas diretas** de `rkd-triade-template`. Cada pasta cujo nome **não** começa com `spec_` é tratada como um `NOME_DO_PROJETO` candidato.

Para confirmar que há algo importável, em cada pasta de projeto verifique se existe ao menos uma filha no padrão atual:

```text
spec_NOME_DO_PROJETO_yyyy_mm_dd_hh:mm
```

Compatibilidade: também aceite pastas antigas `spec_NOME_DO_PROJETO_data_yyyy_mm_dd_hh:mm` e pastas `spec_…` que ainda estejam **diretamente** sob `rkd-triade-template`; parse o `NOME_DO_PROJETO` delas e inclua no distinct.

Faça um **distinct** dos `NOME_DO_PROJETO` encontrados.

Se não houver nenhum projeto com pasta de exportação válida, diga que atualmente **não existe nenhum documento de especificação para ser importado** e pare.

Caso contrário, **liste os nomes distintos** e **pergunte no chat** qual `NOME_DO_PROJETO` o usuário quer importar. Use um widget com uma opção por nome quando couber. **Não invente nomes** e **não prossiga** até o usuário confirmar um dos nomes listados.

## Passo 2 — Listar versões daquele projeto

Com o `NOME_DO_PROJETO` confirmado:

1. Abra a pasta `rkd-triade-template/NOME_DO_PROJETO` (nome exatamente igual).
2. Se essa pasta de projeto **não existir**, diga que atualmente **não existe nenhum documento de especificação para ser importado no projeto NOME_DO_PROJETO** e pare.
3. Liste **todas** as pastas filhas `spec_NOME_DO_PROJETO_yyyy_mm_dd_hh:mm` (e, se houver, as antigas `spec_NOME_DO_PROJETO_data_yyyy_mm_dd_hh:mm`), de preferência da mais recente para a mais antiga.
4. Se não houver nenhuma, diga que atualmente **não existe nenhum documento de especificação para ser importado no projeto NOME_DO_PROJETO** e pare.
5. Pergunte qual pasta exata importar. Espere a confirmação. Não baixe nada até ele confirmar o nome completo da pasta.

## Passo 3 — Importar para `spec` local

Com a pasta de exportação confirmada:

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
- a pasta do Drive importada: `rkd-triade-template/NOME_DO_PROJETO/<nome completo da pasta>`
- quantos arquivos foram trazidos para `spec`
- que a pasta local `spec` está pronta para o trabalho com o código em `src`

Se o Drive não estiver autenticado, ofereça autenticar o conector e só continue após a autorização.
