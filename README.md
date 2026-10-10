<p align="center">
  <img src="assets/triforce-logo.png" alt="Triforce: ref · spec · src" width="448">
</p>

# rkd-triforce-template

## Sobre o projeto

Template para uma esteira de desenvolvimento com IA orientada a especificação. Cada problema vira primeiro um documento de especificação. A IA segue esse documento para implementar a solução num projeto separado, guiada por um conjunto de skills que padronizam cada etapa: clonar o projeto, analisar o código, especificar, documentar, commitar e sincronizar as especificações com o Google Drive.

## Estrutura

| Diretório | Função |
| --- | --- |
| `ref` | Guarda as skills customizadas que orientam a IA em cada etapa do fluxo. Não é um repositório Git próprio. |
| `spec` | Guarda os documentos de especificação, um por problema, no formato `spec_<titulo>_<NNNN>.md`. Não é um repositório Git próprio. |
| `src` | Recebe o projeto onde a solução é implementada. É outro repositório, com o próprio `.git`, e é ignorado por este template. |

## Skills

| Skill | O que faz |
| --- | --- |
| `adicionar_projeto_src` | Clona um repositório do GitHub direto na raiz de `src`, sem pasta intermediária. Ao concluir, aciona `importar_especificacao_drive` para trazer a especificação do Google Drive para `spec`. |
| `remover_projeto_src` | Esvazia `src`, mantendo a pasta e o `.gitkeep`. Antes, confere se há alterações sem commit. Ao concluir, aciona `exportar_especificacao_drive` e, se a exportação terminar com sucesso, esvazia `spec`, mantendo a pasta e o `.gitkeep`. |
| `analisar_projeto_atual` | Analisa o projeto em `src`: linguagem, framework, bibliotecas, configurações e funcionalidades completas ou incompletas. |
| `plano_documento_especificacao` | Transforma a conversa sobre um problema num documento de especificação em `spec`. |
| `preparar_readme` | Cria ou atualiza o `README.md` do projeto em `src`, escrito em inglês, com selos de tecnologias no topo e as seções About the project, Technologies used, Mapped features e How to run the project. |
| `commit_push_alteracoes` | Agrupa as alterações do projeto em `src` por contexto, faz os commits com prefixo (`feat`, `fix`, `chore`, `refactor`, `test`, `docs`) e dá push. |
| `exportar_especificacao_drive` | Envia o conteúdo de `spec` para o Google Drive, em `rkd-triforce-template/NOME_DO_PROJETO/spec_NOME_DO_PROJETO_yyyy_mm_dd_hh:mm`. |
| `importar_especificacao_drive` | Lista os projetos exportados no Google Drive e traz a exportação mais recente do projeto escolhido para `spec`. |
