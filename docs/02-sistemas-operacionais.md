# 2. Sistemas Operacionais

O sistema operacional é a camada que faz a ponte entre o hardware físico e as aplicações. Em ambientes de sustentação e Cloud, o Linux é o padrão de mercado: a imensa maioria dos servidores em nuvem roda alguma distribuição Linux (Ubuntu, Amazon Linux, Debian, entre outras).

## 2.1 Processos e Threads

Um **processo** é uma instância de um programa em execução, com seu próprio espaço de memória isolado. Uma **thread** é uma linha de execução dentro de um processo: várias threads podem rodar dentro do mesmo processo, compartilhando memória entre si, o que as torna mais leves que processos completos, porém mais suscetíveis a condições de corrida se mal sincronizadas.

## 2.2 Memória

O kernel do Linux gerencia a memória disponível entre processos, incluindo o uso de **swap**: espaço em disco usado como extensão da RAM quando ela se esgota. Uso excessivo de swap é sinal de alerta: significa que o sistema está sob pressão de memória e a performance provavelmente está degradada, já que disco é ordens de magnitude mais lento que RAM.

## 2.3 Sistema de Arquivos e Permissões

A estrutura de diretórios do Linux segue um padrão (*Filesystem Hierarchy Standard*):

| Caminho | Finalidade |
|---|---|
| `/` | Raiz do sistema de arquivos |
| `/home` | Diretórios pessoais dos usuários |
| `/etc` | Arquivos de configuração do sistema |
| `/var/log` | Logs do sistema e de serviços |
| `/bin`, `/usr/bin` | Binários executáveis |
| `/tmp` | Arquivos temporários |

Permissões seguem o modelo `rwx` (leitura, escrita, execução), aplicado em três níveis: dono do arquivo, grupo, e demais usuários.

```console title="Permissões: leitura de um exemplo"
$ ls -l script.sh
-rwxr-xr-- 1 thiago devops 512 Set 6 10:00 script.sh
```

Nesse exemplo: o dono (`thiago`) tem leitura, escrita e execução; o grupo (`devops`) tem leitura e execução; outros usuários têm apenas leitura.

```bash title="Comandos de permissão mais usados"
chmod +x script.sh        # adiciona permissão de execução
chmod 755 script.sh       # define rwx para dono, r-x para grupo/outros
chown usuario:grupo arq   # muda o dono e o grupo do arquivo
```

## 2.4 Usuários, Grupos e Serviços (systemd)

O Linux moderno usa o **systemd** como sistema de inicialização e gerenciador de serviços. Ele controla o ciclo de vida de serviços (*daemons*) como servidores web, bancos de dados e agentes de monitoramento.

```bash title="Gerenciamento de serviços com systemctl"
systemctl status nginx              # ver status atual do serviço
systemctl start nginx               # iniciar o serviço
systemctl stop nginx                # parar o serviço
systemctl restart nginx             # reiniciar o serviço
systemctl enable nginx              # habilitar início automático no boot
systemctl is-active --quiet nginx   # retorna código de saída (uso em scripts)
```

## 2.5 Gerenciamento de Pacotes

```bash title="Gerenciadores de pacote comuns"
# Debian / Ubuntu
apt update && apt install nome-pacote

# Amazon Linux / RHEL / CentOS
yum install nome-pacote
dnf install nome-pacote
```

## 2.6 Logs

Logs são a principal fonte de evidência em troubleshooting. A maioria dos serviços grava logs em `/var/log`, e o próprio systemd centraliza logs via `journalctl`.

```bash title="Investigando logs"
tail -f /var/log/syslog              # acompanhar log em tempo real
journalctl -u nginx -f               # logs de um serviço específico, em tempo real
journalctl --since "10 min ago"      # logs recentes
grep -i "error" /var/log/app.log     # filtrar linhas com "error"
```

## 2.7 Processos em Execução e Troubleshooting

```bash title="Comandos essenciais de diagnóstico"
ps aux          # lista todos os processos em execução
top             # visão em tempo real de CPU/memória por processo
htop            # versão mais amigável do top (se instalado)
df -h           # espaço em disco, formato legível
free -h         # uso de memória RAM e swap
netstat -tulnp  # portas abertas e processos associados
ss -tulnp       # alternativa moderna ao netstat
kill -9 PID     # força o encerramento de um processo (último recurso)
crontab -l      # lista tarefas agendadas do usuário atual
```

!!! warning "Atenção"

    `kill -9` envia o sinal SIGKILL, que encerra o processo imediatamente, sem chance de limpeza (fechar arquivos, liberar recursos). Prefira sempre um `systemctl restart` ou um `kill` padrão (SIGTERM) primeiro, e reserve o `-9` para quando o processo realmente não responde a mais nada.

Um conceito importante para entrevistas técnicas é a diferença entre um **processo zumbi** e um **processo travado**: um zumbi já terminou sua execução, mas seu processo pai ainda não coletou seu código de saída (fica "pendurado" na tabela de processos, sem consumir CPU de fato); um processo travado continua rodando, geralmente preso em algum loop ou aguardando um recurso que nunca chega, e pode consumir CPU ativamente.
