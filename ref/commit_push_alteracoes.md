# commit_push_alteracoes

Use quando for commitar e dar push no repositório que tem o próprio .git dentro de src do rkd-triforce-template, agrupando por contexto com prefixo feat, fix, chore, refactor, test ou docs.

No projeto `rkd-triforce-template` existe o diretório `src`. Dentro de `src` há um `.git` próprio: é outro repositório, diferente de `rkd-triforce-template`.

Quando esta skill for acionada, o alvo é somente o repositório cujo `.git` fica dentro de `src`. Entre nesse diretório e rode os comandos Git ali. Não commite nem faça push de `rkd-triforce-template`.

## Como organizar

Olhe todos os arquivos que ainda não foram commitados nesse repositório de `src`.

Analise o contexto de cada alteração e agrupe arquivos que pertencem ao mesmo assunto. Um grupo vira um commit. Não misture assuntos diferentes no mesmo commit.

Use exatamente um destes prefixos na mensagem, seguido de uma frase curta do que mudou:

- `feat`: nova funcionalidade.
- `fix`: correção de um bug.
- `chore`: manutenção que não afeta o código de produção (dependências, configs, scripts).
- `refactor`: reestruturação do código sem mudar o comportamento.
- `test`: adição ou ajuste de testes.
- `docs`: alterações em documentação.

## Passos

1. Entre em `src` e confirme que o `.git` dali é o repositório em uso.
2. Veja o status e o diff dos arquivos não commitados.
3. Separe em grupos por contexto e escolha o prefixo de cada grupo.
4. Faça um commit por grupo, só com os arquivos daquele grupo, mensagem `prefixo: descrição curta`.
5. Se não houver alteração, não crie commit vazio e não faça push.
6. Com os commits feitos, execute o push da branch atual desse repositório para o remote dele.

Não altere o histórico já publicado. Não use force push.
