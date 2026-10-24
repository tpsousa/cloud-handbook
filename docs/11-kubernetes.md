# 11. Kubernetes

!!! info "Contexto complementar"

    Os fundamentos de Kubernetes apresentados nesta seção são contexto complementar, incorporados para completar a visão de ponta a ponta de uma arquitetura moderna de containers em escala. Não representam prática direta ainda realizada.

**Kubernetes** é uma plataforma de orquestração de containers: resolve o problema de rodar, escalar e manter disponíveis centenas ou milhares de containers de forma automatizada, algo inviável de gerenciar manualmente com comandos Docker isolados.

## 11.1 Conceitos Fundamentais

| Termo | Definição |
|---|---|
| Cluster | Conjunto de máquinas (nodes) gerenciadas como uma unidade |
| Node | Uma máquina (física ou virtual) que faz parte do cluster |
| Pod | Menor unidade implantável; um ou mais containers que compartilham rede e armazenamento |
| Deployment | Define o estado desejado de um conjunto de pods (quantas réplicas, qual imagem) |
| Service | Ponto de acesso estável para um conjunto de pods, mesmo que eles mudem de IP |
| Namespace | Espaço lógico para isolar recursos dentro do mesmo cluster |
| ConfigMap | Armazena configuração não sensível, desacoplada da imagem |
| Secret | Armazena dados sensíveis (senhas, tokens), com controle de acesso mais restrito |
| Ingress | Gerencia acesso externo HTTP/HTTPS aos services do cluster |

## 11.2 Scaling, Scheduling e Health Checks

O **scheduler** do Kubernetes decide em qual node cada pod deve rodar, com base em recursos disponíveis. O cluster pode fazer scaling automático do número de pods (*Horizontal Pod Autoscaler*) conforme a carga observada. **Health checks** (*liveness* e *readiness probes*) permitem que o Kubernetes detecte pods travados ou ainda não prontos, substituindo-os automaticamente quando necessário: o mesmo princípio do health check de um Load Balancer, aplicado no nível de container.
