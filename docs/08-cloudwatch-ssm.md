# 8. CloudWatch e SSM

**CloudWatch** é o serviço de monitoramento e logs da AWS: coleta métricas (CPU, memória via agente, tráfego de rede), permite configurar alarmes, e centraliza logs de aplicações e serviços. É a peça central para conectar infraestrutura com sustentação e reporte de incidentes: sem métricas e logs centralizados, diagnosticar um problema em produção vira adivinhação.

**SSM** (*Systems Manager*) permite gerenciar instâncias EC2 remotamente (executar comandos, aplicar patches, ou até acessar um terminal) sem precisar de acesso SSH direto exposto à internet, o que reduz superfície de ataque.
