# plano_documento_especificacao

Use quando o usuário descreve um problema a resolver e pede (ou o fluxo exige) gerar um documento de especificação em spec do rkd-triade-template. A implementação fica no repositório com .git próprio dentro de src.

Arquitetura de desenvolvimento orientado a IA no projeto `rkd-triade-template`. Três pastas na raiz:

- `spec`: início de tudo. Cada problema vira um documento de especificação aqui, no repositório `rkd-triade-template`.
- `src`: dentro desta pasta existe outro repositório, com o próprio arquivo `.git`, diferente de `rkd-triade-template`. A solução é implementada nesse repositório, não no template.
- `ref`: referências e skills, inclusive este procedimento.

## Quando usar

O usuário conversa sobre o problema a resolver. Essa conversa é a entrada. No final, gere um documento de especificação e grave-o em `spec` de `rkd-triade-template`.

Quando for implementar a solução descrita nesse documento, o código vai no repositório cujo `.git` fica dentro de `src`. Não implemente a solução nos arquivos do template.

## Nomenclatura do arquivo

`spec_<titulo_do_problema>_<NNNN>`

- `spec` é prefixo fixo de todo documento de especificação.
- `<titulo_do_problema>`: a partir da conversa, elabore um título curto no contexto, em snake_case, sem acentos.
- `<NNNN>`: versão com 4 dígitos, autoincremento com base nos documentos que já existem em `spec` (o próximo número depois do maior sufixo encontrado; se a pasta estiver vazia, comece em `0001`).
- Extensão: `.md`.

Antes de nomear, liste os arquivos em `spec` de `rkd-triade-template` e calcule o próximo número. Não reutilize um número já usado.

## Estrutura obrigatória do documento

### Problema

Breve descrição do problema.

### Solução proposta

Breve descrição da solução proposta.

### Funcionalidades a serem criadas

Lista geral apenas com o nome de cada funcionalidade.

### Detalhe

Para **cada** funcionalidade da lista anterior, um bloco próprio com:

1. O nome da funcionalidade como título.
2. Descrição detalhada do passo a passo, cobrindo **somente** o escopo daquela funcionalidade, até a conclusão dela.
3. Tabela de **entrada de dados**, duas colunas:

| atributo | significado |
| --- | --- |
| nome do atributo | para que serve e o que faz nesta funcionalidade |

4. Tabela de **saída de dados**, duas colunas:

| atributo | significado |
| --- | --- |
| nome do atributo | o que esse atributo representa nesta funcionalidade |

Nenhuma funcionalidade da lista geral fica sem o seu bloco de detalhe, tabela de entrada e tabela de saída.

## Regras

- Um problema = um documento em `spec` de `rkd-triade-template`.
- A implementação da solução fica no repositório de dentro de `src`, que tem o próprio `.git`.
- Não misture o passo a passo de funcionalidades diferentes no mesmo bloco de detalhe.
- Escreva em português, no tom da conversa com o usuário.
- Se a conversa ainda não der para nomear funcionalidades, entradas ou saídas, pergunte o que falta antes de gravar o arquivo.
