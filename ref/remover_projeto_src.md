# remover_projeto_src

Use quando for esvaziar src do rkd-triade-template. Antes de apagar, rode git status no repositório de src; se houver alterações não commitadas, avise e só continue após o usuário confirmar. Sempre mantém a pasta src e o src/.gitkeep.

## Antes de apagar

1. Entre em `src`.
2. Se existir um `.git` ali, rode `git status` nesse repositório.
3. Se houver alteração não commitada (modificados, staged, untracked relevantes), avise o usuário o que ainda falta commitar e **pergunte se ele quer continuar**.
4. Só apague depois de um sim explícito. Se ele não quiser continuar, pare.
5. Se `src` estiver vazio (só com `.gitkeep`), ou não tiver `.git`, ou o status estiver limpo, pode seguir sem perguntar.

## Remoção

Apague todo o conteúdo de `src` do `rkd-triade-template` (arquivos, pastas e itens ocultos, incluindo `.git`, `.gitignore` e qualquer outro), **exceto `src/.gitkeep`**. Por exemplo: `find src -mindepth 1 ! -name .gitkeep -exec rm -rf {} +`.

- A pasta `src` **nunca** é apagada.
- O arquivo `src/.gitkeep` **nunca** é apagado. Se ele não existir ao final, recrie-o vazio, porque é ele que mantém a pasta `src` no repositório do template.

Não apague `spec`, `ref` nem a raiz do template. Não faça commit nem push dessa limpeza no template.
