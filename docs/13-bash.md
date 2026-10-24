# 13. Bash

## 13.1 Fundamentos

```bash title="Variáveis, condicionais e loops"
# Variáveis
NOME="servidor-01"
echo $NOME

# Condicional
if [ "$STATUS" == "ativo" ]; then
    echo "Serviço rodando"
else
    echo "Serviço parado"
fi

# Loop
for arquivo in $(ls /var/log); do
    echo "Encontrado: $arquivo"
done
```

## 13.2 Redirecionamento e Pipes

```bash title="Redirecionamento e encadeamento de comandos"
comando > arquivo.txt     # sobrescreve o arquivo com a saída
comando >> arquivo.txt    # adiciona a saída ao final do arquivo
comando1 | comando2       # envia a saída do comando1 como entrada do comando2
```

## 13.3 Ferramentas de Texto: grep, awk, sed, cut, sort, xargs

```bash title="Manipulação de texto e logs"
grep -i "error" app.log          # filtra linhas contendo "error" (case-insensitive)
awk '{print $1}' access.log      # imprime a primeira coluna de cada linha
sed 's/erro/ERRO/g' log.txt      # substitui ocorrências de texto
cut -d',' -f2 dados.csv          # extrai a segunda coluna de um CSV
sort -n numeros.txt              # ordena numericamente
xargs -I {} rm {}                # aplica um comando a cada linha recebida
```

## 13.4 Cron

O **cron** agenda execução periódica de scripts, sem intervenção manual.

```cron title="Exemplo de crontab: executar script a cada 5 minutos"
*/5 * * * * /home/thiago/scripts/verifica_servico.sh
```

## 13.5 Script Real: Verificação de Serviço com Alerta

```bash title="verifica_servico.sh"
#!/bin/bash

SERVICO="nginx"
LOG="monitor.log"

if systemctl is-active --quiet "$SERVICO"; then
    echo "OK: o serviço $SERVICO está rodando normalmente."
else
    echo "$(date '+%d/%m/%Y %H:%M:%S') - ALERTA: $SERVICO não está ativo!" >> "$LOG"
    echo "ALERTA registrado no log."
fi
```

Executando: `chmod +x verifica_servico.sh` para tornar o arquivo executável, seguido de `./verifica_servico.sh`.

Esse padrão (verificar condição, agir, registrar em log com data/hora) é a base de praticamente qualquer script de monitoramento simples em ambiente de sustentação.
