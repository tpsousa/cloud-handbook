# Cloud Engineering — Technical Handbook

Fundamentos, infraestrutura e mentalidade de sustentação.
Material pessoal de estudo e referência técnica de **Thiago Sousa**.

📖 **Site:** https://tpsousa.github.io/cloud-handbook/
📄 **PDF:** [`docs/assets/cloud-engineering-handbook.pdf`](docs/assets/cloud-engineering-handbook.pdf)

## Rodando localmente

```bash
python -m venv .venv
source .venv/bin/activate      # Windows: .venv\Scripts\activate
pip install -r requirements.txt
mkdocs serve                   # abre em http://127.0.0.1:8000
```

## Publicando no GitHub Pages

1. Crie o repositório `cloud-handbook` no GitHub e faça push da branch `main`.
2. Em `mkdocs.yml`, troque `SEU-USUARIO` pelo seu usuário do GitHub (`site_url`, `repo_url`, `repo_name`) e neste README.
3. O workflow em `.github/workflows/deploy.yml` roda a cada push na `main` e publica na branch `gh-pages`.
4. Em **Settings → Pages**, escolha **Deploy from a branch**, branch `gh-pages`, pasta `/ (root)`.
5. Em alguns minutos o site fica no ar.

## Estrutura

```
cloud-handbook/
├── docs/
│   ├── index.md
│   ├── introducao.md
│   ├── 01-… até 19-….md      # um arquivo por capítulo
│   ├── glossario.md
│   ├── assets/               # PDF para download
│   └── stylesheets/extra.css
├── mkdocs.yml
├── requirements.txt
└── .github/workflows/deploy.yml
```

## Licença

Defina a licença do conteúdo antes de divulgar (sugestão: [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/deed.pt-br)) e adicione um arquivo `LICENSE`.
