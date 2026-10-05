# remover_projeto_src

Use quando for esvaziar src do rkd-triade-template. Antes de apagar, rode git status no repositório de src; se houver alterações não commitadas, avise e só continue após o usuário confirmar.

## Antes de apagar

1. Entre em `src`.
2. Se existir um `.git` ali, rode `git status` nesse repositório.
3. Se houver alteração não commitada (modificados, staged, untracked relevantes), avise o usuário o que ainda falta commitar e **pergunte se ele quer continuar**.
4. Só apague depois de um sim explícito. Se ele não quiser continuar, pare.
5. Se `src` estiver vazio, ou não tiver `.git`, ou o status estiver limpo, pode seguir sem perguntar.

## Remoção

Apague **todo** o conteúdo de `src` do `rkd-triade-template`: arquivos, pastas e itens ocultos (incluindo `.git`, `.gitignore`, `.gitkeep` e qualquer outro). A pasta `src` deve permanecer, vazia.

Não apague `spec`, `ref` nem a raiz do template. Não faça commit nem push dessa limpeza no template.
