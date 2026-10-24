# 15. Monitoramento e Observabilidade

## 15.1 Métricas, Logs, Traces e Eventos

| Pilar | O que representa |
|---|---|
| Métricas | Valores numéricos ao longo do tempo (CPU %, memória, latência) |
| Logs | Registros textuais e discretos de eventos específicos |
| Traces | Rastreamento do caminho de uma requisição através de múltiplos serviços |
| Eventos | Marcos pontuais relevantes (deploy, reinicialização, alteração de configuração) |
| Alertas | Notificações disparadas quando métricas cruzam limites definidos |

## 15.2 Monitoramento vs. Observabilidade vs. Troubleshooting

- **Monitoramento:** responde "o sistema está saudável agora?", baseado em métricas e alertas predefinidos.
- **Observabilidade:** vai além, permitindo investigar "por que isso está acontecendo?" mesmo para problemas nunca previstos antes, cruzando métricas, logs e traces.
- **Troubleshooting:** o processo ativo de investigação humana, usando as ferramentas de observabilidade disponíveis, para chegar à causa raiz de um problema específico.

??? question "Por que uma empresa investiria em observabilidade se já tem monitoramento básico funcionando?"

    Porque monitoramento só avisa sobre problemas previstos previamente (ex: "CPU acima de 90%"). Observabilidade permite investigar problemas nunca antes vistos, correlacionando múltiplas fontes de dado, algo essencial à medida que sistemas crescem em complexidade e falhas deixam de ser sempre óbvias.
