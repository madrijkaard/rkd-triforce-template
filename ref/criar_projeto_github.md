# criar_projeto_github

Use quando for criar um repositório novo no GitHub do usuário logado (com README.md e licença MIT) e em seguida carregá-lo em src do rkd-triforce-template com a skill adicionar_projeto_src.

Cria um repositório novo na conta GitHub logada no computador do agente, já com `README.md` e licença MIT, e depois carrega esse repositório em `rkd-triforce-template/src` com a skill [adicionar_projeto_src](sand-workflow:adicionar-projeto-src).

## Perguntas (obrigatórias)

Faça uma pergunta por vez no chat e espere a resposta antes da próxima. Não invente valores.

1. **Nome do repositório**: pergunte qual será o nome e use exatamente o que o usuário informar (ajuste só o necessário para um nome válido no GitHub, por exemplo trocando espaços por `-`, e avise se ajustou).
2. **Descrição do repositório**: pergunte qual será a descrição e use o texto informado.
3. **Visibilidade**: se o usuário não tiver dito, pergunte se o repositório será público ou privado.

Antes de criar, confirme que não existe já um repositório com esse nome na conta (`gh repo view <owner>/<nome>`). Se existir, avise e pare.

## Criação

Crie o repositório no GitHub com:

- o nome informado;
- a descrição informada;
- a opção que adiciona o arquivo `README.md` marcada;
- **MIT License** como licença.

Com o `gh` autenticado no computador do agente:

```bash
gh repo create <nome> --<public|private> --description "<descrição>" --add-readme --license mit
```

Se o `gh` não estiver instalado ou autenticado, instale e faça o login (entregando o navegador/código ao usuário quando for preciso), sem pedir token colado no chat.

Confira ao final: `gh repo view <owner>/<nome> --json name,description,url,licenseInfo,visibility` mostra a descrição certa, licença MIT e o `README.md` existe na branch padrão.

## Depois: carregar em src

Logo em seguida, acione a skill [adicionar_projeto_src](sand-workflow:adicionar-projeto-src) para o repositório recém-criado (`<owner>/<nome>`), no `rkd-triforce-template` do computador do agente, e siga a receita dela por inteiro (inclusive a checagem de `src` vazio e a importação da especificação que ela aciona).

- Não peça autorização extra só para acionar a skill; as regras dela continuam valendo.
- Se a criação falhou, não acione e avise o que aconteceu.

## Depois

Informe o nome, a descrição, a visibilidade, o link do repositório, que ele tem `README.md` e licença MIT, e o resultado da skill `adicionar_projeto_src`.
