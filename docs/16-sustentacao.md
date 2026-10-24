# 16. Mentalidade de Sustentação

Esta é, talvez, a parte mais importante deste handbook. Conhecimento técnico isolado (saber o que é uma subnet, o que é um Security Group) é necessário, mas não suficiente. O que realmente diferencia um bom profissional de sustentação é a **metodologia de investigação** diante de um incidente real.

## 16.1 Metodologia de Investigação

```mermaid
flowchart LR
    A[Sintoma] --> B[Hipótese] --> C[Coleta de evidências] --> D[Isolamento]
    D --> E[Diagnóstico] --> F[Correção] --> G[Validação] --> H[Prevenção]
```

| Etapa | Pergunta-guia |
|---|---|
| Sintoma | O que está sendo observado/reportado, exatamente? |
| Hipótese | Quais são as causas prováveis, dado o sintoma? |
| Coleta de evidências | Quais dados (logs, métricas, comandos) confirmam ou descartam cada hipótese? |
| Isolamento | O problema está na aplicação, no sistema operacional, na rede, ou em dependência externa? |
| Diagnóstico | Qual é, de fato, a causa raiz confirmada? |
| Correção | Qual ação resolve o problema imediato? |
| Validação | O sintoma original desapareceu de verdade, e nada mais quebrou? |
| Prevenção | O que evita que isso se repita? |

!!! warning "Atenção"

    Pular direto para "correção" sem antes isolar a causa raiz é o erro mais comum em situação de pressão. Um sintoma como "aplicação lenta" pode ter dezenas de causas possíveis: aplicar uma solução antes de confirmar a hipótese certa desperdiça tempo precioso durante um incidente e pode mascarar o problema real.

## 16.2 Cenário 1: Servidor Inacessível

**Sintoma:** não é possível acessar o servidor.

**Possíveis causas:** problema de DNS; regra de firewall/Security Group bloqueando; serviço parado; porta errada; processo travado consumindo todos os recursos; problema de rede entre cliente e servidor.

```bash title="Comandos"
ping servidor.exemplo.com              # a rede básica até o host responde?
dig servidor.exemplo.com               # o DNS está resolvendo corretamente?
telnet servidor.exemplo.com 443        # a porta específica está acessível?
systemctl status nome-servico          # o serviço está ativo no host?
top                                    # há algum processo consumindo tudo?
tail -f /var/log/nome-servico.log      # há erro recente no log do serviço?
```

**Interpretação:** se o `ping` funciona mas a porta não responde, o problema provavelmente está no serviço ou no firewall, não na rede em si. Se nem o `ping` funciona, o problema é mais fundamental (rede, DNS, ou o host está de fato fora do ar).

## 16.3 Cenário 2: Aplicação Lenta

**Sintoma:** usuários reportam lentidão.

**Possíveis causas:** CPU ou memória no limite; I/O de disco saturado; latência de rede; consulta lenta no banco de dados; dependência externa lenta (API de terceiro).

```bash title="Comandos"
top / htop                      # identifica processo consumindo CPU/memória
free -h                         # verifica pressão de memória (uso de swap)
iostat -x 1                     # mostra utilização de I/O de disco
netstat -tulnp                  # conexões ativas, possíveis gargalos de rede
tail -f /var/log/app.log        # erros ou lentidão reportada nos logs da app
```

**Interpretação:** priorize o recurso mais próximo do limite (CPU vs memória vs disco vs rede). Geralmente apenas um deles é o gargalo real, e otimizar os outros não resolve nada até que o gargalo verdadeiro seja tratado.

## 16.4 Cenário 3: Aplicação Não Consegue Acessar o Banco

**Sintoma:** erro de conexão com banco de dados.

**Possíveis causas:** DNS do banco não resolve; rota de rede incorreta entre subnets; porta bloqueada pelo Security Group; credenciais incorretas ou expiradas; serviço do banco parado.

```bash title="Comandos"
dig banco.interno.exemplo.com                # o nome do banco resolve corretamente?
telnet banco.interno.exemplo.com 5432        # a porta do banco está acessível?
psql -h host -U usuario -d banco             # testar conexão/credenciais diretamente
```

**Interpretação:** se a porta não abre via `telnet`, o problema é de rede/Security Group, não de credencial. Credenciais só importam depois que a conexão de rede já foi estabelecida com sucesso.

## 16.5 Cenário 4: Servidor Sem Espaço

**Sintoma:** erro de `no space left on device`.

**Possíveis causas:** logs crescendo sem rotação; arquivos temporários não limpos; volumes/imagens Docker órfãs acumulando espaço; crescimento legítimo de dados sem planejamento de capacidade.

```bash title="Comandos"
df -h                      # visão geral de uso por partição
du -sh /var/log/*          # quais diretórios de log ocupam mais espaço
docker system df           # espaço ocupado por imagens/volumes Docker
docker system prune -a     # remove imagens e volumes não utilizados
```

**Interpretação:** `df -h` mostra o sintoma (qual partição está cheia); `du -sh` localiza a causa (quais diretórios específicos consomem o espaço). Nunca limpe algo sem antes confirmar o que é, especialmente em produção.
