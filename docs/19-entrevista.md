# 19. Perguntas e Respostas por Nível

As respostas a seguir buscam refletir compreensão real do conceito: explicando o raciocínio por trás, não apenas repetindo uma definição decorada.

## 19.1 Nível Básico: Fundamentos

??? question "O que acontece quando você digita um domínio no navegador?"

    **Resposta ideal:** o navegador primeiro resolve o domínio via DNS, seguindo a hierarquia até obter o IP do servidor autoritativo. Com o IP em mãos, estabelece uma conexão TCP (handshake de 3 vias) e, se for HTTPS, negocia TLS para criptografar a comunicação. Depois, envia a requisição HTTP, que pode passar por um Load Balancer antes de chegar ao servidor de aplicação, que processa e retorna a resposta.

    **O que se avalia:** visão de ponta a ponta, conectando DNS, TCP, TLS e HTTP como camadas de um mesmo fluxo.

??? question "O que é DNS?"

    **Resposta ideal:** sistema que traduz nomes de domínio legíveis por humanos em endereços IP usados pelas máquinas para se comunicar, seguindo uma hierarquia de servidores (root, TLD, autoritativo).

    **O que se avalia:** clareza na explicação e conhecimento do fluxo de resolução, não apenas a definição superficial.

??? question "Qual a diferença entre TCP e UDP?"

    **Resposta ideal:** TCP é orientado a conexão, com handshake e garantia de entrega ordenada, usado onde confiabilidade importa mais que velocidade (HTTP, SSH). UDP não estabelece conexão prévia, é mais rápido mas sem garantias, usado em streaming e chamadas de voz, onde perder um pacote é preferível a atrasar.

    **O que se avalia:** capacidade de explicar o porquê de cada protocolo existir, com exemplo prático de uso.

??? question "O que é CIDR?"

    **Resposta ideal:** notação (`IP/prefixo`) usada para representar um bloco de endereços IP, onde o número após a barra indica quantos bits definem a parte de rede. O restante define quantos endereços estão disponíveis dentro daquele bloco.

    **O que se avalia:** entendimento prático, incluindo capacidade de calcular ou estimar quantos endereços um bloco específico oferece.

??? question "O que é uma subnet, e qual a diferença entre pública e privada?"

    **Resposta ideal:** subnet é uma subdivisão lógica de uma rede maior (VPC), com seu próprio bloco CIDR. Subnet pública tem rota para um Internet Gateway (entrada e saída de tráfego); subnet privada não recebe conexão externa diretamente, mas pode ter saída via NAT Gateway.

    **O que se avalia:** a nuance de que privada não significa ausência total de internet, apenas ausência de conexão de entrada.

## 19.2 Nível Intermediário: Troubleshooting

??? question "O que é NAT Gateway?"

    **Resposta ideal:** recurso que permite que instâncias em subnets privadas iniciem conexões de saída à internet (para atualizações, chamadas de API externas), sem expô-las a conexões de entrada vindas de fora. Um único NAT Gateway pode atender múltiplas instâncias privadas.

    **O que se avalia:** entendimento do fluxo assimétrico (saída sim, entrada não), e não apenas "ele dá internet pra rede privada".

??? question "O que é Security Group?"

    **Resposta ideal:** firewall associado diretamente a um recurso (não à subnet como um todo), definindo quais conexões de entrada e saída são permitidas. Diferente de subnet, que define onde o recurso está e quais rotas possui, Security Group define quem pode se conectar a ele.

    **O que se avalia:** clareza na distinção entre os dois conceitos, que costumam ser confundidos.

??? question "Como você investigaria um servidor inacessível?"

    **Resposta ideal:** seguir uma metodologia estruturada: primeiro confirmar se é problema de DNS (`dig`), depois de rede/porta (`ping`, `telnet`), depois se o serviço está de fato ativo (`systemctl status`), e por último revisar logs em busca de erro específico. Isolar camada por camada evita presumir a causa antes de confirmar evidência.

    **O que se avalia:** metodologia de investigação, não apenas conhecimento isolado de comandos.

??? question "Como você investigaria uma aplicação lenta?"

    **Resposta ideal:** verificar CPU, memória, I/O de disco e rede, identificando qual recurso está próximo do limite (geralmente há um único gargalo real). Cruzar isso com logs da aplicação para ver se há erro ou lentidão explícita reportada, e considerar dependências externas (banco de dados, APIs de terceiros) como possível origem do atraso.

    **O que se avalia:** capacidade de priorizar hipóteses em vez de investigar tudo aleatoriamente.

??? question "Container é uma VM?"

    **Resposta ideal:** não. VM virtualiza hardware completo, com sistema operacional próprio isolado; container compartilha o kernel do sistema operacional hospedeiro, isolando apenas processos. Por isso é muito mais leve e rápido de iniciar, porém com isolamento de segurança mais fraco que uma VM.

    **O que se avalia:** precisão técnica na diferença, evitando a confusão comum de tratar os dois como sinônimos.

## 19.3 Nível Avançado: Arquitetura e Incidentes

??? question "O que é Infrastructure as Code, e por que é melhor que configuração manual?"

    **Resposta ideal:** prática de definir infraestrutura em código (via ferramentas como Terraform), trazendo replicabilidade (recriar ambientes idênticos), versionamento (rastrear mudanças via Git) e redução de erro humano, especialmente relevante quando o número de recursos gerenciados cresce (dezenas de VMs, redes e regras).

    **O que se avalia:** capacidade de ir além de "é mais rápido", citando os três benefícios estruturais.

??? question "Como você investigaria um incidente em produção?"

    **Resposta ideal:** seguir a metodologia sintoma → hipótese → coleta de evidências → isolamento → diagnóstico → correção → validação → prevenção. Priorizar restaurar o serviço (mitigação) antes de necessariamente entender 100% da causa raiz, se o impacto for crítico, e só depois investigar a fundo para prevenir recorrência.

    **O que se avalia:** equilíbrio entre agir rápido sob pressão e não pular etapas de investigação de forma descuidada.

??? question "O que é Kubernetes, e quando ele se justifica em relação a rodar containers 'soltos' com Docker?"

    **Resposta ideal:** Kubernetes é uma plataforma de orquestração que automatiza a execução, escalonamento e recuperação de containers em escala. Faz sentido quando a quantidade de containers e a necessidade de alta disponibilidade tornam inviável o gerenciamento manual. Para poucos containers em ambiente simples, a complexidade adicional do Kubernetes pode não se justificar.

    **O que se avalia:** senso crítico sobre quando uma ferramenta complexa é justificada, evitando a resposta ingênua de "sempre use Kubernetes".
