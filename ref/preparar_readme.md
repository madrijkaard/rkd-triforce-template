# preparar_readme

Use quando for criar ou atualizar o README.md do repositório que tem o próprio .git dentro de src do rkd-triforce-template, em inglês, no padrão: selos de tecnologias, About the project, Technologies used (tabela), Mapped features e How to run the project.

No projeto `rkd-triforce-template` existe o diretório `src`. Dentro de `src` há um `.git` próprio: é outro repositório, diferente de `rkd-triforce-template`.

O `README.md` documenta esse repositório de dentro de `src`, não o template. O arquivo fica na raiz desse repositório, ou seja, em `src/README.md`.

## Quando acionar

Ao ser acionada, entre em `src` e verifique se `README.md` existe ali.

- Se não existir, crie `src/README.md`.
- Se existir, reescreva mantendo esta mesma estrutura, atualizando o conteúdo com o que o código desse repositório realmente faz hoje.

O README é escrito **em inglês** (todo o texto, inclusive os títulos das seções e os valores de status), estilizado e bem formatado: ícone ao lado de cada título, títulos em fonte maior (use heading markdown, `#` para o nome do projeto e `##` para as quatro seções). Não invente tecnologias, funcionalidades, comandos ou configurações. Se algo não estiver no código, escreva que ainda não foi definido (em inglês, por exemplo `Not defined yet`).

A conversa com o usuário continua em português; só o conteúdo do `README.md` é em inglês.

## Estrutura obrigatória

Ordem do arquivo: título `#` do projeto, selos de tecnologias, e então as quatro seções `##`.

### 0. Selos das tecnologias (acima de "About the project")

Logo abaixo do título `#` e **antes** da seção `## About the project`, coloque uma linha centralizada com os selos (badges) das tecnologias realmente usadas no projeto, no estilo do exemplo do usuário: cada selo tem um rótulo cinza à esquerda (a categoria, como `PLATFORM`, `LANGUAGE`, `DOCUMENT`) e o nome da tecnologia à direita, com a cor da marca e o ícone dela.

Use `img.shields.io` no estilo `for-the-badge`, dentro de `<p align="center">`, um `<img>` por selo, com `alt` descritivo:

```html
<p align="center">
  <img src="https://img.shields.io/badge/platform-Electron-47848F?style=for-the-badge&logo=electron&logoColor=white" alt="Electron">
  <img src="https://img.shields.io/badge/language-JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black" alt="JavaScript">
  <img src="https://img.shields.io/badge/document-DOCX-2B579A?style=for-the-badge&logo=microsoftword&logoColor=white" alt="DOCX">
</p>
```

Regras dos selos:

- Só inclua tecnologias que existem no código (linguagens, plataforma/framework, bibliotecas principais, formatos de arquivo tratados). Não invente nenhuma.
- Escolha um rótulo de categoria curto e coerente (`platform`, `language`, `library`, `document`, `format`, `tool`).
- Use o `logo=` com o slug do Simple Icons quando existir e `logoColor` com bom contraste (preto em fundos claros, como o amarelo do JavaScript; branco nos demais). Sem ícone disponível, omita o `logo=`.
- Use a cor oficial da marca quando for conhecida; senão, uma cor neutra.
- Os selos devem coincidir com as tecnologias listadas na tabela da seção 2.

### 1. About the project

Ícone no título. Breve descrição do projeto, em inglês.

### 2. Technologies used

Ícone no título. As principais tecnologias do projeto (linguagens, bibliotecas, frameworks e ferramentas auxiliares) apresentadas **numa tabela de 2 colunas**: na primeira, o nome da tecnologia; na segunda, para que ela é usada neste projeto (não uma descrição genérica da tecnologia).

| Technology | What it is used for |
| --- | --- |

Uma linha por tecnologia, só as que existem no código.

### 3. Mapped features

Ícone no título. Liste as funcionalidades já implementadas numa tabela de 3 colunas:

| Feature | What it does | Status |
| --- | --- | --- |

Status só pode ser:

- `COMPLETE`: a implementação está feita, existem testes que a cobrem devidamente e esses testes estão todos passando.
- `PARTIAL`: a implementação está pela metade, ou ainda não existem testes para ela.

### 4. How to run the project

Ícone no título. Descrição a partir do zero, em inglês:

- requisitos para o programa funcionar;
- programas que precisam estar instalados antes;
- comandos necessários para colocar o programa em funcionamento;
- configurações e arquivos que precisam ser editados antes, o que editar e por quê.

Seja claro e específico. Use blocos de código para os comandos.
