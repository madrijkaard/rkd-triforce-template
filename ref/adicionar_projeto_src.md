# adicionar_projeto_src

Use quando for clonar um repositório do GitHub do usuário logado para dentro de src do rkd-triforce-template, com o .git na raiz de src (sem pasta com o nome do projeto). Ao concluir a inclusão, aciona em seguida a skill importar_especificacao_drive.

O `rkd-triforce-template` é um repositório Git. A pasta `src` **não** faz parte do código do template: nela deve ficar **outro repositório**, com o próprio `.git`. Esse repositório aninhado é o projeto de implementação.

## Objetivo

Clonar um repositório ao qual a conta GitHub logada tem acesso e colocar o conteúdo **direto** em `rkd-triforce-template/src`. Depois que o projeto estiver em `src`, importar a especificação do Google Drive com a skill [importar_especificacao_drive](sand-workflow:importar-especificacao-drive) (ver "Depois: importar a especificação").

## Layout correto

Um `git clone` normal cria uma pasta com o nome do projeto e, dentro dela, o código (`README.md`, `.git`, etc.).

Em `src` **não** deve existir essa pasta intermediária. Os arquivos do clone (incluindo `.git` e `README.md`) ficam na **raiz de `src`**:

- Certo: `src/README.md`, `src/.git`, …
- Errado: `src/<nome-do-repo>/README.md`, `src/<nome-do-repo>/.git`, …

## Antes de clonar

1. Confirme qual repositório clonar (owner/nome ou URL). Se o usuário não disse, pergunte.
2. Verifique o conteúdo atual de `src`.
3. Se `src` já tiver um projeto (qualquer coisa além de `.gitkeep`), **não** clone por cima. Avise e só continue se o usuário pedir limpeza (use a skill [remover_projeto_src](sand-workflow:remover-projeto-src)) ou confirmar substituição explícita.
4. O `src/.gitkeep` é versionado no template e **deve ser mantido sempre**, também depois do clone: é ele que faz a pasta `src` existir no GitHub do template. Nunca o deixe ser apagado pelo clone (ver "Preservar o `.gitkeep`" abaixo).

## Clone

Clone **para a raiz de `src`**, sem pasta com o nome do repositório. Preferências:

```bash
git clone <url-do-repo> /caminho/para/rkd-triforce-template/src
```

Se `src` ainda tiver só `.gitkeep`, não clone direto em `src` (o `git clone` exige pasta vazia): use um clone em diretório temporário e mova **todo** o conteúdo (incluindo `.git` e arquivos ocultos) para `src`, sem apagar o `src/.gitkeep`.

Garanta ao final:

- `src/.git` existe e é o do repositório clonado.
- `src/.gitkeep` continua existindo (ver abaixo).
- Não existe `src/<nome-do-repo>/`.
- O remoto e a branch padrão fazem sentido (`git -C src remote -v`, `git -C src status`).

Use a autenticação já disponível no computador (`gh` / credential helper). Não force push. Não faça commit no template por causa desse clone (`src` está no `.gitignore` do template).

## Preservar o `.gitkeep`

Depois do clone (ou da movimentação do conteúdo), garanta o `src/.gitkeep` do template:

1. Se `src/.gitkeep` não existir, recrie-o vazio (`touch src/.gitkeep`).
2. Registre-o na lista de ignorados local do repositório do projeto, para que ele **não** apareça como arquivo novo (`??`) nem seja commitado no repositório do projeto: acrescente a linha `.gitkeep` ao arquivo `src/.git/info/exclude` (crie o arquivo se faltar e não duplique a linha se ela já existir). Esse arquivo é local, não é versionado e não altera o `.gitignore` do projeto.
3. Confirme: `git -C src status --short` não lista `.gitkeep`, e `git status --short` no template não mostra `src/.gitkeep` como apagado (`D`).

## Depois: importar a especificação

Sempre que esta skill for acionada, **logo na sequência** do processo de inclusão (clone concluído, `.gitkeep` preservado e conferências feitas), acione a skill [importar_especificacao_drive](sand-workflow:importar-especificacao-drive) e siga a receita dela por inteiro (listar os projetos do Drive, o usuário escolher o número, achar a exportação mais recente, preparar `spec` e copiar o conteúdo).

- Não pule esta etapa e não peça autorização extra só para acionar a skill: o fluxo da própria `importar_especificacao_drive` (escolha do projeto e confirmação antes de substituir o que já está em `spec`) continua valendo.
- Só acione se a inclusão tiver sido concluída. Se o processo parou antes (por exemplo, `src` já tinha um projeto e o usuário não autorizou a limpeza, ou o clone falhou), não acione e avise que a importação não foi feita.
- Não faça commit nem push por causa da importação.

## Depois

Informe o repositório clonado, a branch e que o `.git` está na raiz de `src`, e em seguida o resultado da importação (projeto, pasta importada e arquivos trazidos para `spec`). Não invente funcionalidades nem reescreva o README a menos que o usuário peça outra skill.
