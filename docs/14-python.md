# 14. Python para Infraestrutura

## 14.1 Bibliotecas Relevantes

| Biblioteca | Uso |
|---|---|
| `psutil` | Coleta de métricas do sistema: CPU, memória, disco, processos |
| `requests` | Chamadas HTTP para APIs externas ou health checks de serviços |
| `boto3` | SDK oficial da AWS para Python, automatiza criação/consulta de recursos |

## 14.2 Script Real: Monitoramento de Disco

```python title="disco_monitor.py"
import shutil
from datetime import datetime

def verificar_disco():
    try:
        total, usado, livre = shutil.disk_usage("/")
        porcentagem_usado = (usado / total) * 100

        if porcentagem_usado > 90:
            agora = datetime.now().strftime("%d/%m/%Y %H:%M:%S")
            mensagem = f"{agora} - ALERTA: disco em {porcentagem_usado:.1f}% de uso\n"
            print(mensagem)
            with open("monitor.log", "a") as arquivo:
                arquivo.write(mensagem)
        else:
            print(f"Disco OK, uso atual: {porcentagem_usado:.1f}%")

    except Exception as e:
        print("Não foi possível verificar o status do disco:", e)

verificar_disco()
```

!!! warning "Atenção"

    Em automação de infraestrutura, um script sem tratamento de erro (`try/except`) é uma falha grave, não apenas um detalhe estético: sem ele, um problema inesperado pode interromper a execução silenciosamente, comprometendo toda a automação sem gerar alerta nenhum.

## 14.3 Extensão Natural: psutil e requests

O mesmo padrão do script de disco se estende naturalmente a CPU e memória usando `psutil`:

```python title="Padrão equivalente para CPU (usando psutil)"
import psutil
from datetime import datetime

def verificar_cpu(limite=90):
    uso = psutil.cpu_percent(interval=1)
    if uso > limite:
        agora = datetime.now().strftime("%d/%m/%Y %H:%M:%S")
        print(f"{agora} - ALERTA: CPU em {uso}%")
    else:
        print(f"CPU OK: {uso}%")

verificar_cpu()
```

```python title="Verificando se um serviço web está no ar"
import requests

def verificar_servico(url):
    try:
        resposta = requests.get(url, timeout=5)
        if resposta.status_code == 200:
            print("Serviço no ar.")
        else:
            print(f"Serviço com problema, código: {resposta.status_code}")
    except requests.exceptions.RequestException:
        print("Serviço inacessível.")

verificar_servico("https://exemplo.com")
```
