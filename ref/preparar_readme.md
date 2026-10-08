# preparar_readme

Use quando for criar ou atualizar o README.md do repositório que tem o próprio .git dentro de src do rkd-triade-template, no padrão Sobre o projeto, Tecnologias, Funcionalidades mapeadas e Como executar.

No projeto `rkd-triade-template` existe o diretório `src`. Dentro de `src` há um `.git` próprio: é outro repositório, diferente de `rkd-triade-template`.

O `README.md` documenta esse repositório de dentro de `src`, não o template. O arquivo fica na raiz desse repositório, ou seja, em `src/README.md`.

## Quando acionar

Ao ser acionada, entre em `src` e verifique se `README.md` existe ali.

- Se não existir, crie `src/README.md`.
- Se existir, reescreva mantendo esta mesma estrutura, atualizando o conteúdo com o que o código desse repositório realmente faz hoje.

O README é em português, estilizado e bem formatado: ícone ao lado de cada título, títulos em fonte maior (use heading markdown, `#` para o nome do projeto e `##` para as quatro seções). Não invente tecnologias, funcionalidades, comandos ou configurações. Se algo não estiver no código, escreva que ainda não foi definido.

## Estrutura obrigatória

### 1. Sobre o projeto

Ícone no título. Breve descrição do projeto.

### 2. Tecnologias utilizadas

Ícone no título. De forma geral, as principais tecnologias do projeto: linguagens, bibliotecas, frameworks e ferramentas auxiliares.

### 3. Funcionalidades mapeadas

Ícone no título. Liste as funcionalidades já implementadas numa tabela de 3 colunas:

| Funcionalidade | O que faz | Status |
| --- | --- | --- |

Status só pode ser:

- `COMPLETA`: a implementação está feita, existem testes que a cobrem devidamente e esses testes estão todos passando.
- `PARCIAL`: a implementação está pela metade, ou ainda não existem testes para ela.

### 4. Como executar o projeto

Ícone no título. Descrição a partir do zero:

- requisitos para o programa funcionar;
- programas que precisam estar instalados antes;
- comandos necessários para colocar o programa em funcionamento;
- configurações e arquivos que precisam ser editados antes, o que editar e por quê.

Seja claro e específico. Use blocos de código para os comandos.
