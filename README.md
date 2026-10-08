<p align="center">
  <img src="assets/triforce-logo.png" alt="Triforce: ref · spec · src" width="448">
</p>

# rkd-triforce-template

Template para uma esteira de desenvolvimento com IA orientada a especificação, organizada em três pastas:

| Pasta | Papel |
| --- | --- |
| `ref` | Referências e skills que guiam a IA. |
| `spec` | Documentos de especificação, um por problema, no formato `spec_<titulo>_<NNNN>.md`. |
| `src` | Onde fica o projeto implementado. É outro repositório, com o próprio `.git`, e é ignorado por este template. |

## Skills em `ref`

- `plano_documento_especificacao.md`: gera o documento de especificação em `spec`.
- `preparar_readme.md`: cria ou atualiza o README do repositório de `src`.
- `commit_push_alteracoes.md`: agrupa as alterações do repositório de `src`, faz os commits com prefixo e dá push.
- `remover_projeto_src.md`: esvazia `src` depois de conferir se há algo sem commit.
