# preparar_readme

Use quando for criar ou atualizar o README.md na raiz de src do projeto rkd-triade-template.

## O que observar

O arquivo `README.md` na raiz da pasta `src`.

Quando esta skill for acionada:

- se `src/README.md` não existir, crie-o;
- se existir, reescreva mantendo esta mesma estrutura, atualizando o conteúdo com o que o código realmente faz hoje.

O README é em português, estilizado e bem formatado: ícone ao lado de cada título, títulos em fonte maior (heading markdown, `#` para o nome do projeto e `##` para as quatro seções). Não invente tecnologias, funcionalidades, comandos ou configurações. Se algo não estiver no código, escreva que ainda não foi definido.

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
