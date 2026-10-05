# commit_push_alteracoes

Use quando for commitar o que ainda não foi commitado, agrupando por contexto, e em seguida fazer push.

## O que observar

Todos os arquivos que ainda não foram commitados no repositório atual.

## Como organizar

Analise o contexto de cada alteração e agrupe arquivos que pertencem ao mesmo assunto. Um grupo vira um commit. Não misture assuntos diferentes no mesmo commit.

Use exatamente um destes prefixos na mensagem, seguido de uma frase curta do que mudou:

- `feat`: nova funcionalidade.
- `fix`: correção de um bug.
- `chore`: manutenção que não afeta o código de produção (dependências, configs, scripts).
- `refactor`: reestruturação do código sem mudar o comportamento.
- `test`: adição ou ajuste de testes.
- `docs`: alterações em documentação.

## Passos

1. Veja o status e o diff dos arquivos não commitados.
2. Separe em grupos por contexto e escolha o prefixo de cada grupo.
3. Faça um commit por grupo, só com os arquivos daquele grupo, mensagem `prefixo: descrição curta`.
4. Se não houver alteração, não crie commit vazio e não faça push.
5. Com os commits feitos, execute o push da branch atual para o remote.

Não altere o histórico já publicado. Não use force push.
