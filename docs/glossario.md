# Glossário Técnico

| Termo | Definição e contexto |
|---|---|
| **AMI** | Imagem base usada para lançar uma instância EC2 na AWS. |
| **Availability Zone** | Datacenter fisicamente isolado dentro de uma região de nuvem. |
| **CIDR** | Notação de bloco de endereços IP (IP/prefixo). |
| **CloudWatch** | Serviço de monitoramento e logs da AWS. |
| **Container** | Processo isolado, empacotado com suas dependências, compartilhando o kernel do host. |
| **Cron** | Agendador de tarefas periódicas no Linux. |
| **Deployment (K8s)** | Define o estado desejado de um conjunto de pods no Kubernetes. |
| **DNS** | Sistema que traduz nomes de domínio em endereços IP. |
| **Drift (Terraform)** | Divergência entre o estado real da infraestrutura e o definido em código. |
| **EBS** | Armazenamento em bloco persistente da AWS, separado do ciclo de vida da instância. |
| **EC2** | Serviço de máquinas virtuais sob demanda da AWS. |
| **Elasticidade** | Capacidade de um ambiente se ajustar automaticamente à demanda. |
| **Fault Tolerance** | Capacidade do sistema continuar operando mesmo com falha de um componente. |
| **Firewall** | Filtro de tráfego de rede baseado em regras. |
| **Gateway** | Ponto de saída de uma rede local para outras redes. |
| **Handshake (TCP)** | Processo de três vias (SYN, SYN-ACK, ACK) que estabelece uma conexão TCP. |
| **Health Check** | Verificação periódica usada por Load Balancers/Kubernetes para detectar falhas. |
| **Hypervisor** | Software que gerencia máquinas virtuais sobre um hardware físico. |
| **IaaS** | Modelo de nuvem onde o provedor entrega infraestrutura bruta (VMs, rede). |
| **IaC** | Infrastructure as Code: definir infraestrutura via código. |
| **IAM** | Serviço de gerenciamento de identidade e permissões da AWS. |
| **Internet Gateway** | Componente que conecta uma VPC à internet. |
| **IOPS** | Operações de entrada/saída por segundo que um armazenamento processa. |
| **Kernel** | Núcleo do sistema operacional, compartilhado entre containers no mesmo host. |
| **Load Balancer** | Distribui requisições entre múltiplas instâncias. |
| **NAT Gateway** | Permite saída à internet para recursos em subnet privada, sem expor entrada. |
| **Namespace (K8s)** | Espaço lógico de isolamento dentro de um cluster Kubernetes. |
| **Node (K8s)** | Máquina que faz parte de um cluster Kubernetes. |
| **Observabilidade** | Capacidade de investigar problemas cruzando métricas, logs e traces. |
| **PaaS** | Modelo de nuvem onde o provedor entrega plataforma pronta para rodar código. |
| **Pod (K8s)** | Menor unidade implantável no Kubernetes, um ou mais containers. |
| **Policy (IAM)** | Documento que define quais ações são permitidas ou negadas. |
| **Provider (Terraform)** | Plugin que conecta o Terraform a uma plataforma específica. |
| **Region** | Área geográfica onde um provedor de nuvem mantém infraestrutura. |
| **Role (IAM)** | Identidade temporária assumível por usuários ou serviços. |
| **Route Table** | Define para onde o tráfego de uma subnet é direcionado. |
| **SaaS** | Modelo de nuvem onde o provedor entrega software pronto para uso final. |
| **Scaling Horizontal** | Adicionar mais máquinas para suportar mais carga. |
| **Scaling Vertical** | Aumentar os recursos de uma única máquina. |
| **Security Group** | Firewall associado diretamente a um recurso de nuvem. |
| **Service (K8s)** | Ponto de acesso estável a um conjunto de pods. |
| **Shared Responsibility** | Modelo que define os limites entre segurança do provedor e do cliente. |
| **Snapshot** | Ponto de restauração de um disco/VM em determinado momento. |
| **State (Terraform)** | Arquivo que registra o estado real da infraestrutura gerenciada. |
| **Subnet** | Subdivisão lógica de uma rede maior (VPC). |
| **systemd** | Sistema de inicialização e gerenciamento de serviços do Linux moderno. |
| **TCP** | Protocolo de transporte confiável, orientado a conexão. |
| **Template (Virtualização)** | Imagem base usada para criar novas VMs rapidamente. |
| **TLS** | Protocolo de criptografia usado para proteger comunicações (base do HTTPS). |
| **TTL (DNS)** | Tempo que uma resposta DNS permanece em cache. |
| **UDP** | Protocolo de transporte sem conexão, mais rápido e sem garantia de entrega. |
| **VPC** | Rede virtual privada e isolada dentro de um provedor de nuvem. |
