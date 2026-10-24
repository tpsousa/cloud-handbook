# 17. Laboratórios Realizados

## 17.1 Laboratório 1: Script de Monitoramento de Disco (Python)

=== "Objetivo"

    Detectar automaticamente quando o uso de disco ultrapassa um limite crítico, registrando um alerta com data e hora.

=== "Arquitetura e pré-requisitos"

    Script Python standalone, executado manualmente ou via cron, escrevendo em um arquivo de log local. Requer Python 3; nenhuma biblioteca externa (usa apenas `shutil` e `datetime`, da biblioteca padrão).

=== "Implementação"

    Função única que consulta `shutil.disk_usage("/")`, calcula o percentual usado, e condicionalmente grava um alerta em log. O código completo está no [capítulo 14](14-python.md#142-script-real-monitoramento-de-disco).

    ```bash
    python3 disco_monitor.py
    ```

=== "Testes e erros"

    Validado com o limite normal (90%) e temporariamente reduzido para 1% para forçar a geração do alerta e confirmar a escrita correta no log.

    **Possíveis erros:** falha de permissão para escrever o arquivo de log; caminho de disco inexistente no ambiente onde o script roda.

!!! success "O que aprendi"

    A importância de tratar erro em automação de infraestrutura, e como formatar corretamente data/hora para registros de log legíveis (`strftime`).

`shutil.disk_usage` retorna uma tupla nomeada com total, usado e livre em bytes; a proporção entre usado e total independe da unidade. O bloco `try/except` captura qualquer exceção e imprime mensagem descritiva, evitando que o script quebre silenciosamente.

## 17.2 Laboratório 2: Script de Verificação de Serviço (Bash)

=== "Objetivo"

    Verificar se um serviço gerenciado pelo systemd está ativo, registrando alerta em log quando não estiver.

=== "Arquitetura e pré-requisitos"

    Script Bash standalone, usando `systemctl is-active` como fonte de verdade do status do serviço. Requer Linux com systemd e permissão de execução do script.

=== "Implementação"

    A condicional `if systemctl is-active --quiet $SERVICO` decide entre mensagem de sucesso ou gravação de alerta com timestamp. O código completo está no [capítulo 13](13-bash.md#135-script-real-verificacao-de-servico-com-alerta).

    ```bash
    chmod +x verifica_servico.sh && ./verifica_servico.sh
    ```

=== "Testes e erros"

    Executado tanto com um serviço ativo quanto com um serviço inexistente/parado, confirmando os dois caminhos do `if/else`.

    **Possíveis erros:** nome do serviço incorreto; falta de permissão de execução do script.

!!! success "O que aprendi"

    A diferença entre escrever código Bash direto no terminal (que quebra com estruturas de múltiplas linhas) e salvar como arquivo `.sh` executado de uma vez.

A flag `--quiet` suprime a saída do comando, usando apenas o código de saída (0 = ativo) na condicional. Para troubleshooting, rodar `systemctl status nome-servico` manualmente confirma o nome exato do serviço antes de automatizar a verificação.

## 17.3 Laboratório 3: Arquitetura Conceitual de VPC

=== "Objetivo"

    Consolidar o entendimento de como organizar uma VPC em camadas (tiers) de segurança, com base em material estudado sobre a arquitetura da Locaweb Cloud.

=== "Arquitetura e pré-requisitos"

    VPC única dividida em três subnets: tier web (pública), tier app (privada) e tier DB (privada), cada uma com seu bloco CIDR próprio. Requer entendimento prévio de CIDR, Internet Gateway, NAT Gateway e Security Groups.

=== "Implementação (conceitual)"

    Internet Gateway associado à subnet pública; NAT Gateway compartilhado atendendo as subnets privadas; Security Groups em camada, liberando apenas o tráfego estritamente necessário entre tiers. Veja o diagrama no [capítulo 9](09-vpc.md).

    Exercício conceitual de desenho de arquitetura, não provisionado em ambiente real neste momento.

=== "Possíveis erros"

    Esquecer de configurar a rota da subnet privada para o NAT Gateway (resultando em recursos privados sem saída à internet). Validar as route tables de cada subnet individualmente confirma se a rota esperada (Internet Gateway ou NAT Gateway) está de fato associada.

!!! success "O que aprendi"

    Que Security Group e subnet resolvem problemas diferentes e complementares: confundir os dois é um erro conceitual comum. A separação em tiers segue o princípio de menor exposição: apenas o que precisa ser público (o balanceador de carga) fica exposto; aplicação e banco ficam isolados.
