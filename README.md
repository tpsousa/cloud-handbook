# Cloud Engineering — Technical Handbook

**Fundamentos, infraestrutura e práticas de sustentação em cloud computing.**

Este handbook é um projeto pessoal de estudo e documentação desenvolvido por **Thiago Sousa**, estudante de Ciência da Computação na Universidade Federal do Maranhão (UFMA).

O material reúne conhecimentos adquiridos por meio de estudos independentes, documentação técnica e experimentação prática, com o objetivo de consolidar conceitos fundamentais de cloud computing, infraestrutura, redes, Linux e operações em ambientes de nuvem.

A proposta é construir uma referência técnica de consulta, conectando os fundamentos teóricos às situações encontradas na prática de engenharia de cloud.

**Acesse o material:**

- **Site:** https://tpsousa.github.io/cloud-handbook/
- **PDF:** [`docs/assets/cloud-engineering-handbook.pdf`](docs/assets/cloud-engineering-handbook.pdf)

## Executando localmente

O projeto utiliza MkDocs para gerar a documentação. Para executar o site localmente, tenha Python e pip instalados e execute:

```bash
python -m venv .venv
source .venv/bin/activate      # Windows: .venv\Scripts\activate
pip install -r requirements.txt
mkdocs serve                   # http://127.0.0.1:8000
```

## Publicação no GitHub Pages

A publicação é automatizada por GitHub Actions.

1. Crie o repositório `cloud-handbook` no GitHub e envie o código para a branch `main`.
2. No arquivo `mkdocs.yml`, configure `site_url`, `repo_url` e `repo_name` com os dados do seu repositório. Atualize também o endereço do site neste README.
3. O workflow em `.github/workflows/deploy.yml` executa a publicação a cada push na branch `main`, gerando o site na branch `gh-pages`.
4. Em **Settings → Pages**, configure a publicação a partir da branch `gh-pages`, utilizando a pasta `/ (root)`.
5. Após a conclusão do deploy, o site estará disponível no endereço configurado.

## Estrutura do projeto

```text
cloud-handbook/
├── docs/
│   ├── index.md
│   ├── introducao.md
│   ├── 01-... até 19-....md
│   ├── glossario.md
│   ├── assets/
│   │   └── cloud-engineering-handbook.pdf
│   └── stylesheets/
│       └── extra.css
├── mkdocs.yml
├── requirements.txt
└── .github/
    └── workflows/
        └── deploy.yml
```

## Licença

A licença do conteúdo deve ser definida antes da divulgação pública. Uma opção para permitir o compartilhamento e a adaptação do material, com atribuição de autoria, é a [Creative Commons Attribution 4.0 International (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/deed.pt-br).

Antes de adotá-la, revise seus termos e adicione o arquivo `LICENSE` ao repositório.
