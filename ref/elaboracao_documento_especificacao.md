# elaboracao_documento_especificacao

Use quando o usuário descreve um problema a resolver e pede (ou o fluxo exige) gerar um documento de especificação na pasta spec, no formato spec_título_000N.

## Pastas do projeto

Arquitetura de desenvolvimento orientado a IA. Três pastas na raiz:

- `spec`: início de tudo. A conversa sobre o problema vira um documento de especificação aqui.
- `src`: código da solução.
- `ref`: referências e skills, inclusive este procedimento.

## Entrada

A conversa inicial com a IA sobre o problema a resolver. No final dessa conversa, gerar o documento e gravá-lo em `spec`.

## Nomenclatura do arquivo

`spec_<titulo_do_problema>_<NNNN>.md`

- `spec` é prefixo fixo de todo documento de especificação.
- `<titulo_do_problema>`: a partir do que foi conversado, elaborar um título curto no contexto, em snake_case, sem acentos.
- `<NNNN>`: versionamento com 4 dígitos, autoincremento com base nos documentos que já existem na pasta `spec`. Se a pasta estiver vazia, começar em `0001`. O próximo arquivo usa o maior sufixo encontrado mais um. Não reutilizar um número já usado.

## Estrutura obrigatória do documento

### Problema

Breve descrição do problema.

### Solução proposta

Breve descrição da solução proposta.

### Funcionalidades a serem criadas

Lista geral apenas com o nome das funcionalidades que serão criadas.

### Detalhe

Para cada funcionalidade listada no tópico anterior, um bloco próprio contendo:

1. O nome da funcionalidade.
2. Descrição detalhada do passo a passo que compreende apenas o escopo daquela funcionalidade, até a sua conclusão.
3. Tabela de entrada de dados, duas colunas:

| atributo | significado |
| --- | --- |
| nome do atributo | para que aquele atributo serve e o que ele faz nesta funcionalidade |

4. Tabela de saída de dados, duas colunas:

| atributo | significado |
| --- | --- |
| nome do atributo | o que aquele atributo representa nesta funcionalidade |

Cada funcionalidade da lista geral tem o seu tópico de detalhe, a sua tabela de entrada e a sua tabela de saída. Não misturar o passo a passo de funcionalidades diferentes no mesmo bloco.

## Regras

- Cada problema a ser tratado é um documento de especificação na pasta `spec`.
- Escrever em português.
- Se a conversa ainda não der para nomear funcionalidades, entradas ou saídas, perguntar o que falta antes de gravar o arquivo.
