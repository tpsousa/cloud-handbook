# 1. Introdução à Infraestrutura Moderna

Antes de falar de nuvem, vale entender o que ela substitui e o que preserva. Infraestrutura é o conjunto de recursos físicos e lógicos (servidores, rede, armazenamento) que sustenta uma aplicação rodando e disponível para quem precisa dela.

## 1.1 Infraestrutura tradicional vs. Cloud

Na infraestrutura tradicional (*on-premises*), a empresa compra, instala e mantém fisicamente seus próprios servidores num datacenter próprio ou alugado. Isso significa: investimento alto adiantado, tempo de provisionamento medido em semanas, e capacidade ociosa (você compra pensando no pico de uso, e o resto do tempo esse hardware fica subutilizado).

Na Cloud, um provedor (AWS, Azure, GCP, ou plataformas nacionais como a Locaweb Cloud) mantém datacenters massivos e aluga capacidade computacional sob demanda. Isso inverte a lógica: você paga pelo que usa (*pay-as-you-go*), provisiona recursos em minutos, e escala para cima ou para baixo conforme a necessidade real.

| Aspecto | Tradicional | Cloud |
|---|---|---|
| Investimento | Alto, adiantado (CAPEX) | Sob demanda (OPEX) |
| Tempo de provisionamento | Dias a semanas | Minutos |
| Escalabilidade | Limitada ao hardware comprado | Elástica |
| Manutenção física | Responsabilidade da empresa | Responsabilidade do provedor |
| Capacidade ociosa | Comum (dimensionado para o pico) | Minimizada (paga-se o uso real) |

## 1.2 Servidores e Datacenters

Um **servidor** é, em essência, um computador dedicado a atender requisições de outros computadores (clientes). Um **datacenter** é uma instalação física que abriga milhares desses servidores, com energia redundante, refrigeração, conectividade de rede de alta capacidade e segurança física.

## 1.3 Recursos Computacionais

Todo *workload* (uma aplicação web, um banco de dados ou um script de automação) consome quatro tipos fundamentais de recurso:

- **CPU:** capacidade de processamento, medida em núcleos (cores) e frequência.
- **Memória (RAM):** espaço volátil onde dados em uso ficam disponíveis rapidamente para a CPU.
- **Armazenamento (Storage):** espaço persistente em disco, onde dados sobrevivem a reinicializações.
- **Rede:** capacidade de comunicação entre sistemas, medida em largura de banda e latência.

*Workload* é o termo usado para descrever qualquer carga de trabalho computacional (uma aplicação, um banco de dados, um job de processamento) rodando sobre esses recursos.
