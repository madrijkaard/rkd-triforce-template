# remover_projeto_src

Use quando for esvaziar src do rkd-triforce-template. Antes de apagar, rode git status no repositório de src; se houver alterações não commitadas, avise e só continue após o usuário confirmar. Sempre mantém a pasta src e o src/.gitkeep. Ao concluir a remoção, aciona a skill exportar_especificacao_drive e, depois que a exportação terminar, esvazia spec mantendo só a pasta e o spec/.gitkeep.

No projeto `rkd-triforce-template`, limpe o conteúdo do diretório `src`, mantendo a pasta `src` e o arquivo `src/.gitkeep`. Depois da remoção, exporte a especificação para o Google Drive com a skill [exportar_especificacao_drive](sand-workflow:exportar-especificacao-drive) e, só depois que a exportação terminar com sucesso, esvazie `spec`, mantendo a pasta e o `spec/.gitkeep`.

## Antes de apagar

1. Entre em `src`.
2. Se existir um `.git` ali, rode `git status` nesse repositório.
3. Se houver alteração não commitada (modificados, staged, untracked relevantes), avise o usuário o que ainda falta commitar e **pergunte se ele quer continuar**.
4. Só apague depois de um sim explícito. Se ele não quiser continuar, pare.
5. Se `src` estiver vazio (só com `.gitkeep`), ou não tiver `.git`, ou o status estiver limpo, pode seguir sem perguntar.

## Remoção

Apague todo o conteúdo de `src` do `rkd-triforce-template` (arquivos, pastas e itens ocultos, incluindo `.git`, `.gitignore` e qualquer outro), **exceto `src/.gitkeep`**. Por exemplo: `find src -mindepth 1 ! -name .gitkeep -exec rm -rf {} +`.

- A pasta `src` **nunca** é apagada.
- O arquivo `src/.gitkeep` **nunca** é apagado. Se ele não existir ao final, recrie-o vazio, porque é ele que mantém a pasta `src` no repositório do template.

Não apague a raiz do template nem `ref`. Não faça commit nem push dessa limpeza no template.

## Depois: exportar a especificação

Sempre que esta skill for acionada, **logo na sequência** do processo de remoção (conteúdo de `src` apagado e `src/.gitkeep` conferido), acione a skill [exportar_especificacao_drive](sand-workflow:exportar-especificacao-drive) e siga a receita dela por inteiro (perguntar o `NOME_DO_PROJETO`, criar a pasta `spec_NOME_yyyy_mm_dd_hh:mm` no Drive e enviar todos os documentos de `spec`).

- Não pule esta etapa e não peça autorização extra só para acionar a skill: o fluxo da própria `exportar_especificacao_drive` (inclusive a pergunta do nome do projeto) continua valendo.
- Só acione se a remoção tiver sido concluída. Se o usuário não confirmou a remoção e o processo parou, não acione a exportação nem mexa em `spec`.

## Depois: esvaziar spec

Assim que o procedimento da skill `exportar_especificacao_drive` **finalizar com sucesso** (todos os arquivos enviados e conferidos no Drive), remova todos os arquivos de `rkd-triforce-template/spec`, mantendo apenas a pasta `spec` e o arquivo `spec/.gitkeep`. Por exemplo: `find spec -mindepth 1 ! -name .gitkeep -exec rm -rf {} +`.

- Apague arquivos, subpastas e itens ocultos de `spec`, **exceto `spec/.gitkeep`**.
- A pasta `spec` **nunca** é apagada. O `spec/.gitkeep` **nunca** é apagado: se ele não existir ao final, recrie-o vazio.
- **Não apague nada de `spec` se a exportação falhou, foi interrompida, ficou incompleta ou não foi feita** (por exemplo, `spec` estava vazia e a exportação avisou e parou, o Drive não estava autenticado ou o usuário não informou o nome do projeto). Nesse caso, avise o que ficou pendente e mantenha os arquivos.
- Não faça commit nem push dessa limpeza.

## Depois

Informe que `src` foi esvaziado (mantendo `src/.gitkeep`), o resultado da exportação (projeto, caminho no Drive, link e quantidade de arquivos) e que `spec` ficou só com o `spec/.gitkeep` (ou, se a exportação não terminou, que `spec` foi mantida).
