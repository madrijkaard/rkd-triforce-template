# adicionar_projeto_src

Use quando for clonar um repositório do GitHub do usuário logado para dentro de src do rkd-triade-template, com o .git na raiz de src (sem pasta com o nome do projeto).

O `rkd-triade-template` é um repositório Git. A pasta `src` **não** faz parte do código do template: nela deve ficar **outro repositório**, com o próprio `.git`. Esse repositório aninhado é o projeto de implementação.

## Objetivo

Clonar um repositório ao qual a conta GitHub logada tem acesso e colocar o conteúdo **direto** em `rkd-triade-template/src`.

## Layout correto

Um `git clone` normal cria uma pasta com o nome do projeto e, dentro dela, o código (`README.md`, `.git`, etc.).

Em `src` **não** deve existir essa pasta intermediária. Os arquivos do clone (incluindo `.git` e `README.md`) ficam na **raiz de `src`**:

- Certo: `src/README.md`, `src/.git`, …
- Errado: `src/<nome-do-repo>/README.md`, `src/<nome-do-repo>/.git`, …

## Antes de clonar

1. Confirme qual repositório clonar (owner/nome ou URL). Se o usuário não disse, pergunte.
2. Verifique o conteúdo atual de `src`.
3. Se `src` já tiver um projeto (qualquer coisa além de `.gitkeep`), **não** clone por cima. Avise e só continue se o usuário pedir limpeza (use a skill remover_projeto_src) ou confirmar substituição explícita.
4. Mantenha `src/.gitkeep` no template quando `src` estiver vazio; após um clone bem-sucedido o `.git` do projeto aninhado passa a ocupar `src`, e o `.gitkeep` do template deixa de ser necessário ali (pode ser removido junto com o clone).

## Clone

Clone **para a raiz de `src`**, sem pasta com o nome do repositório. Preferências:

```bash
git clone <url-do-repo> /caminho/para/rkd-triade-template/src
```

Se `src` ainda tiver só `.gitkeep`, remova o conteúdo de `src` (exceto se a skill de remoção exigir confirmação) ou use um clone em diretório temporário e mova **todo** o conteúdo (incluindo `.git` e arquivos ocultos) para `src`.

Garanta ao final:

- `src/.git` existe e é o do repositório clonado.
- Não existe `src/<nome-do-repo>/`.
- O remoto e a branch padrão fazem sentido (`git -C src remote -v`, `git -C src status`).

Use a autenticação já disponível no computador (`gh` / credential helper). Não force push. Não faça commit no template por causa desse clone (`src` está no `.gitignore` do template).

## Depois

Informe o repositório clonado, a branch e que o `.git` está na raiz de `src`. Não invente funcionalidades nem reescreva o README a menos que o usuário peça outra skill.
