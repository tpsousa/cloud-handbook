# Introdução

Este handbook nasceu de um processo simples: curiosidade encontrando um problema real e não soltando mais.

Minha trajetória começou no desenvolvimento de software: construindo APIs, integrando sistemas, resolvendo regras de negócio. Foi lidando com um problema aparentemente pequeno, containers Docker que simplesmente não se comunicavam por causa de um comportamento específico do sistema operacional, que percebi que o que mais me atraía não era só construir a aplicação, mas entender o ambiente em que ela roda: o sistema operacional por baixo, a rede que conecta as peças, a infraestrutura que sustenta tudo funcionando.

Este material reúne os fundamentos que estudei nessa jornada em direção à Cloud Engineering: sistemas operacionais, redes, virtualização, computação em nuvem, arquitetura de VPC, containers, automação, observabilidade e a mentalidade de sustentação de ambientes críticos.

Não pretendo aparentar domínio completo de todos os temas aqui presentes, isso seria desonesto com o estágio real da minha formação. O objetivo deste documento é outro: registrar de forma organizada e tecnicamente rigorosa aquilo que venho estudando, de modo que sirva tanto como material de revisão pessoal quanto como evidência de uma forma de pensar que estou desenvolvendo.

!!! warning "Atenção"

    Sempre que um conceito exigir conhecimento complementar àquele que venho estudando e praticando diretamente, isso será identificado explicitamente em caixas de **Contexto Complementar**, para manter clareza entre o que foi vivenciado na prática e o que é apresentado para completar a compreensão técnica do assunto.

A jornada documentada aqui segue uma progressão lógica:

```mermaid
flowchart LR
    A[Aplicação] --> B[Sistema Operacional] --> C[Rede] --> D[Virtualização] --> E[Cloud]
```

E, a partir daí, para automação, observabilidade e sustentação: as camadas que transformam infraestrutura funcionando em infraestrutura confiável.

> "Um bom profissional de infraestrutura não apenas sabe executar comandos. Ele entende o sistema, formula hipóteses, coleta evidências, identifica a causa raiz e toma decisões baseadas em dados."
