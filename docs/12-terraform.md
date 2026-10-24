# 12. Terraform

## 12.1 Por que IaC é importante

Imagine precisar provisionar manualmente 20 VMs, 10 redes, 5 load balancers e 30 regras de firewall, uma por uma, clicando em um console. Além de lento, o processo é propenso a erro humano e impossível de replicar de forma idêntica em outro ambiente.

**Infrastructure as Code (IaC)** resolve isso definindo toda a infraestrutura em arquivos de código, versionados como qualquer código de aplicação:

- **Replicabilidade:** o mesmo código recria o ambiente idêntico em qualquer lugar.
- **Versionamento:** com Git, é possível rastrear cada mudança na infraestrutura ao longo do tempo.
- **Redução de erro humano:** o mesmo processo automatizado roda de forma consistente toda vez.

## 12.2 Conceitos do Terraform

| Termo | Definição |
|---|---|
| Provider | Plugin que conecta o Terraform a uma plataforma (AWS, Azure, etc.) |
| Resource | Um componente de infraestrutura a ser criado (uma VM, uma rede) |
| Variable | Parâmetro de entrada, reutilizável entre execuções |
| Output | Valor exposto após a criação (ex: IP público gerado) |
| State | Arquivo que registra o estado atual real da infraestrutura gerenciada |
| Module | Conjunto reutilizável de recursos, agrupados como um bloco |

```hcl title="Exemplo simplificado de configuração Terraform"
provider "aws" {
  region = "sa-east-1"
}

variable "instance_type" {
  default = "t3.micro"
}

resource "aws_instance" "servidor_web" {
  ami           = "ami-0123456789abcdef"
  instance_type = var.instance_type

  tags = {
    Name = "servidor-web"
  }
}

output "ip_publico" {
  value = aws_instance.servidor_web.public_ip
}
```

```bash title="Fluxo básico de comandos"
terraform init      # baixa providers e inicializa o projeto
terraform plan      # mostra o que será criado/alterado/destruído
terraform apply     # aplica as mudanças de fato
terraform destroy   # remove toda a infraestrutura criada
```

## 12.3 Drift e Organização em Módulos

**Drift** acontece quando o estado real da infraestrutura diverge do que está definido no código, por exemplo, quando alguém altera algo manualmente pelo console, fora do fluxo do Terraform. O comando `terraform plan` detecta esse desalinhamento antes de aplicar novas mudanças.

Em projetos maiores, a infraestrutura costuma ser organizada em módulos separados por responsabilidade:

```text title="Organização típica de um projeto Terraform"
terraform/
  network/        -> VPC, subnets, route tables
  compute/        -> instâncias EC2
  storage/        -> volumes, buckets
  load_balancer/  -> load balancers e target groups
  firewall/       -> security groups
```
