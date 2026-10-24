# 10. Docker

## 10.1 Conceitos Fundamentais

| Termo | Definição |
|---|---|
| Container | Processo isolado, empacotado com tudo que precisa para rodar (código, dependências, configuração), compartilhando o kernel do host |
| Image | Modelo imutável a partir do qual containers são criados |
| Dockerfile | Arquivo de instruções que define como construir uma image |
| Registry | Repositório onde images ficam armazenadas e versões são publicadas |
| Docker Hub | Registry público mais popular |
| Volume | Mecanismo de persistência de dados fora do ciclo de vida do container |
| Network | Camada de rede virtual que conecta containers entre si |

## 10.2 Relação com Virtualização e Cloud

Containers resolvem um problema prático que VMs resolvem de forma mais pesada: empacotar uma aplicação com tudo que ela precisa para rodar de forma consistente, independentemente de onde é executada. Em Cloud, é comum rodar containers dentro de VMs (instâncias EC2, por exemplo), combinando o isolamento da VM com a leveza e portabilidade do container.

!!! warning "Atenção"

    Um comportamento específico do sistema operacional hospedeiro pode interferir na comunicação entre containers mesmo quando a configuração de rede parece correta à primeira vista. Um exemplo real vivido: dois containers (uma API principal e uma API mock) que simplesmente não se comunicavam devido a um comportamento específico do Ubuntu na camada de rede do Docker. Isso reforça uma lição central de troubleshooting: às vezes o problema não está na aplicação, está no ambiente em que ela roda.

## 10.3 Dockerfile e Comandos Básicos

```dockerfile title="Exemplo simples de Dockerfile"
FROM python:3.11-slim

WORKDIR /app
COPY requirements.txt .
RUN pip install -r requirements.txt

COPY . .

EXPOSE 5000
CMD ["python", "app.py"]
```

```bash title="Comandos essenciais do Docker"
docker build -t minha-app .             # constrói a imagem a partir do Dockerfile
docker run -p 5000:5000 minha-app       # executa um container, mapeando portas
docker ps                               # lista containers em execução
docker logs -f nome_container           # acompanha logs de um container
docker exec -it nome_container bash     # abre um terminal dentro do container
docker compose up                       # sobe múltiplos serviços definidos em compose.yml
```

!!! info "Contexto complementar"

    Variáveis de ambiente (`-e VAR=valor` no `docker run`, ou a seção `environment` no Docker Compose) são a forma padrão de injetar configuração, como credenciais de banco de dados, sem hardcodar valores dentro da imagem.
