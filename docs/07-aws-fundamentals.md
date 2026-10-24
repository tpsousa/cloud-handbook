# 7. AWS Fundamentals

Esta seção organiza os principais serviços e conceitos da AWS estudados, sempre seguindo a progressão: **o que é → por que existe → como funciona → quando usar → problemas comuns → como diagnosticar**.

## 7.1 Contas, Regiões e Availability Zones

Uma **conta AWS** é a unidade administrativa e de cobrança. Dentro dela, recursos são criados em **regiões** específicas (ex: `sa-east-1` para São Paulo), e cada região contém várias **Availability Zones** isoladas entre si fisicamente.

## 7.2 IAM: Identity and Access Management

**O que é:** serviço de gerenciamento de identidade e permissões da AWS.
**Por que existe:** para controlar precisamente quem (pessoa ou sistema) pode fazer o quê, sobre quais recursos.
**Como funciona:** através de users, groups, roles e policies.

| Elemento | Função |
|---|---|
| User | Identidade de uma pessoa ou aplicação específica |
| Group | Coleção de users, para aplicar permissões em lote |
| Role | Identidade temporária, assumível por serviços ou usuários, sem credenciais fixas |
| Policy | Documento JSON que define quais ações são permitidas ou negadas |
| MFA | Autenticação multifator, camada extra de segurança no login |

**Quando usar Role em vez de credenciais fixas de User:** sempre que possível. Roles geram credenciais temporárias, reduzindo o risco de uma chave de acesso vazada continuar válida indefinidamente.

```json title="Exemplo simplificado de IAM Policy"
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::meu-bucket/*"
    }
  ]
}
```

Essa policy permite apenas a ação de leitura (`GetObject`) sobre objetos dentro de um bucket S3 específico, exemplo do **princípio de menor privilégio**: conceder exatamente o necessário, nada além disso.

**Problemas comuns:** permissões excessivamente amplas (`"Action": "*"`); usuários com credenciais fixas antigas nunca rotacionadas; falta de MFA em contas privilegiadas.

**Como diagnosticar:** revisar policies anexadas a um user/role via console ou CLI, verificar o IAM Access Analyzer para identificar acessos públicos ou entre contas não intencionais.

## 7.3 EC2: Elastic Compute Cloud

**O que é:** serviço de máquinas virtuais sob demanda da AWS, o equivalente direto a uma VM tradicional.
**Por que existe:** fornecer capacidade de processamento configurável, sem necessidade de hardware próprio.

| Conceito | Descrição |
|---|---|
| AMI | Imagem base (sistema operacional + configurações) usada para lançar a instância |
| Instance Type | Combinação de CPU, RAM e rede disponível (ex: `t3.micro`, `m5.large`) |
| EBS | Volume de armazenamento persistente anexado à instância |
| Key Pair | Par de chaves SSH para acesso seguro à instância |
| User Data | Script executado automaticamente na primeira inicialização |

## 7.4 EBS: Elastic Block Store

**O que é:** armazenamento em bloco, separado do ciclo de vida da instância EC2. É possível desanexar um volume EBS de uma instância e anexar em outra, preservando os dados.

!!! warning "Atenção"

    Sistema operacional é diferente de dados da aplicação. Uma boa prática arquitetural é separar o *root disk* (onde vive o SO) do *data disk* (onde vivem os dados persistentes da aplicação), facilitando backup, migração e resposta a incidentes sem depender do estado exato do disco de sistema.

Um indicador de performance de storage relevante é o **IOPS** (*Input/Output Operations Per Second*): quantas operações de leitura/escrita o armazenamento consegue processar por segundo. Cargas de trabalho com muitas transações pequenas e frequentes (bancos de dados, por exemplo) costumam exigir volumes com IOPS mais altos.
