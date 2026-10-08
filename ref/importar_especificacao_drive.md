# importar_especificacao_drive

Use quando for importar do Google Drive a exportação mais recente de um projeto (rkd-triforce-template/NOME_DO_PROJETO/spec_NOME_DO_PROJETO_yyyy_mm_dd_hh:mm) para rkd-triforce-template/spec no workspace local.

Traz do Google Drive o conteúdo da exportação **mais recente** de um projeto e coloca esse conteúdo em `rkd-triforce-template/spec`, no workspace local (`/workspace/rkd-triforce-template/spec`).

## Layout do template no workspace

```text
/workspace/rkd-triforce-template/   (repositório Git do template)
├── src/    (outro repositório Git, com .git próprio: o projeto de implementação)
├── spec/   (NÃO é repositório Git: guarda os documentos de especificação)
└── ref/    (NÃO é repositório Git: guarda as skills pedidas pelo usuário)
```

- `rkd-triforce-template` é um repositório Git.
- `src` contém outro repositório Git, independente do template.
- `spec` e `ref` são pastas comuns de documentos, sem `.git` próprio.
- Esta skill só trabalha em `spec`.

O conteúdo de cada exportação no Drive são **documentos de especificação** (arquivos e, se houver, subpastas), não um repositório Git.

## Estrutura no Google Drive

```text
rkd-triforce-template/                              (pasta raiz, no Meu Drive)
├── NOME_DO_PROJETO_A/                            (um projeto)
│   ├── spec_NOME_DO_PROJETO_A_2026_10_01_09:15   (uma exportação)
│   ├── spec_NOME_DO_PROJETO_A_2026_10_05_18:40
│   └── spec_NOME_DO_PROJETO_A_2026_10_07_22:03   (mais recente)
└── NOME_DO_PROJETO_B/
    └── spec_NOME_DO_PROJETO_B_2026_09_30_14:00
```

- `rkd-triforce-template` é a pasta raiz.
- Cada pasta filha direta dela é um projeto, e o nome da pasta é o `NOME_DO_PROJETO`.
- Dentro de cada projeto há uma ou mais exportações, cada uma numa pasta `spec_NOME_DO_PROJETO_yyyy_mm_dd_hh:mm`: o termo `spec`, o nome do projeto e o ano, mês, dia, hora e minuto da exportação.

Caminho de uma exportação válida:

```text
rkd-triforce-template/NOME_DO_PROJETO/spec_NOME_DO_PROJETO_yyyy_mm_dd_hh:mm
```

## Pré-requisitos

- Conector Google Drive conectado. Se não estiver autenticado, ofereça autenticar e só continue depois.
- Repositório `rkd-triforce-template` no workspace, com a pasta `spec` dentro dele.

## Passo 1 — Listar os projetos

1. Busque no Google Drive a pasta com o nome exato `rkd-triforce-template`.
2. Se ela não existir, diga que não existe nenhuma exportação para importar e pare.
3. Liste as pastas filhas diretas dela. Cada uma é um `NOME_DO_PROJETO`. Ignore arquivos soltos.
4. Se não houver nenhuma pasta de projeto, diga que não existe nenhum projeto para importar e pare.
5. Mostre os projetos numerados, em ordem alfabética, exatamente neste formato:

```text
1 - NOME_DO_PROJETO
2 - NOME_DO_PROJETO
3 - NOME_DO_PROJETO
```

6. Peça ao usuário para escolher um dos números. Não invente nomes e não continue até ele responder com um número válido da lista.

## Passo 2 — Achar a exportação mais recente

1. Entre na pasta do projeto escolhido.
2. Considere só as pastas filhas cujo nome segue exatamente `spec_<NOME_DO_PROJETO>_yyyy_mm_dd_hh:mm`, com o mesmo nome de projeto da pasta.
3. Extraia a data e hora do **próprio nome** de cada pasta (ignore datas de criação ou modificação do Drive) e escolha a mais recente.
4. Se não houver nenhuma pasta válida, diga que não existe exportação para importar no projeto `NOME_DO_PROJETO` e pare.
5. Informe qual pasta foi escolhida e siga sem pedir outra confirmação.

## Passo 3 — Preparar `spec`

1. Garanta que `/workspace/rkd-triforce-template/spec` exista.
2. Se `spec` tiver qualquer coisa além de `spec/.gitkeep`:
   - Liste para o usuário os arquivos e pastas que estão em `spec` hoje e avise que serão substituídos.
   - Pergunte se pode substituir e só continue depois de um sim explícito. Se ele não confirmar, pare sem mexer em nada.
   - Ao confirmar, apague todo o conteúdo de `spec`, inclusive ocultos, mantendo a pasta `spec` e o `spec/.gitkeep`.
3. Se `spec` estiver vazio ou só com `spec/.gitkeep`, siga direto.

## Passo 4 — Copiar o conteúdo

1. Baixe **todo** o conteúdo de dentro da pasta de exportação escolhida, de forma recursiva: arquivos e pastas, ocultos ou não.
2. Coloque esse conteúdo **direto na raiz de `spec`**, preservando nomes e estrutura relativa. Não crie uma pasta intermediária com o nome da exportação ou do projeto.
   - Certo: `spec/spec_cadastro_..._0001.md`, ...
   - Errado: `spec/spec_NOME_DO_PROJETO_.../...`, `spec/NOME_DO_PROJETO/...`
3. Use as ferramentas do conector Google Drive para listar e baixar. Para muitos arquivos, baixe para uma pasta temporária e depois mova tudo, incluindo os ocultos, para `spec`. Não cole conteúdo de arquivos no chat.
4. Mantenha o `spec/.gitkeep` (ele é versionado no template). Se ele não existir ao final, recrie-o vazio.

## Passo 5 — Conferir

Confirme que o número de arquivos em `spec` (sem contar o `.gitkeep`) bate com o da pasta no Drive e que nenhuma pasta intermediária foi criada.

## Regras

- Não altere, mova nem apague nada no Google Drive.
- Não faça commit nem push no template nem no repositório de `src`.
- Não mexa em `src`, `ref` nem na raiz do template.

## Depois

Informe ao usuário:

- o `NOME_DO_PROJETO` escolhido;
- a pasta importada: `rkd-triforce-template/NOME_DO_PROJETO/<nome completo da pasta>`;
- quantos arquivos foram trazidos para `spec` e quais são;
- que a especificação está pronta para uso em `spec`.
