# analisar_projeto_atual

Use quando for analisar o projeto que está dentro de src do rkd-triforce-template: linguagem, framework, bibliotecas, configurações e funcionalidades (completas ou incompletas).

No `rkd-triforce-template`, a pasta `src` não é o código do template. Dentro de `src` existe **outro repositório**, com o próprio `.git`. Toda a análise é desse repositório aninhado, não do template.

## Escopo

- Trabalhe só em `rkd-triforce-template/src`.
- Não misture `spec`, `ref` nem a raiz do template com o projeto analisado.
- Se `src` estiver vazio (só `.gitkeep`) ou não tiver `.git`, diga que não há projeto para analisar e pare.

## O que observar

1. **Identidade do repositório:** remoto, branch atual, últimos commits relevantes, estrutura de pastas na raiz.
2. **Stack:** linguagem(ns), runtime, framework, bibliotecas e dependências (ex.: `package.json`, `requirements.txt`, `Cargo.toml`, `go.mod`, lockfiles).
3. **Configurações:** scripts de build/test/start, lint, TypeScript, Electron, Docker, CI, env de exemplo, targets (desktop, web, API).
4. **Funcionalidades:** percorra o código (módulos principais, rotas, UI, serviços, testes). Para cada funcionalidade, diga o que ela faz e se está **completa** ou **incompleta**.
   - Completa: implementada de ponta a ponta e, quando houver testes, eles passam no que cobre essa parte.
   - Incompleta: parcial, stub, TODO, feature flag off, sem testes onde o projeto costuma ter, ou quebrada.
5. **Não invente:** só afirme o que o código, configs e testes mostram.

## Como entregar

Responda em português, em prosa clara, com estas seções:

1. **Visão geral** — o que é o projeto e onde está (repo aninhado em `src`).
2. **Stack e configurações** — linguagem, framework, bibliotecas e configs relevantes.
3. **Funcionalidades** — lista ou tabela: nome, o que faz, status (completa / incompleta) e breve evidência.
4. **Lacunas ou riscos** — só se houver evidência (testes falhando, deps faltando, etc.).

Não altere arquivos do projeto nem do template. Não faça commit nem push.
