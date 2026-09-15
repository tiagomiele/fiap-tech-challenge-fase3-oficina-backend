# Evidências de Atendimento aos Requisitos Obrigatórios — Oficina Fase 3

Este documento centraliza as evidências de atendimento aos requisitos obrigatórios do Tech Challenge — Oficina Fase 3.

## Projetos da solução

| Projeto | Repositório |
|---|---|
| Backend — aplicação principal | [fiap-tech-challenge-fase3-oficina-backend](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-backend) |
| Auth Serverless | [fiap-tech-challenge-fase3-oficina-auth-serverless](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-auth-serverless) |
| Kubernetes Infra | [fiap-tech-challenge-fase3-oficina-kubernetes-infra](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-kubernetes-infra) |
| Database Infra | [fiap-tech-challenge-fase3-oficina-database-infra](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-database-infra) |

## 1. Autenticação Serverless e API Gateway

A autenticação por CPF valida a existência e o status ativo do cliente, emite um JWT e protege as rotas sensíveis por meio do API Gateway.

### Evidências de implementação

- [Arquitetura do Auth](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-auth-serverless/blob/main/docs/arquitetura.md)
- [RFC da autenticação por CPF e JWT](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-backend/blob/main/docs/decisions/rfc/0003-autenticacao-cpf-jwt.md)
- [Terraform do API Gateway](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-auth-serverless/blob/main/apigateway.tf)
- [Terraform das funções Lambda](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-auth-serverless/blob/main/lambda.tf)
- [Contrato OpenAPI do Auth](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-auth-serverless/blob/main/docs/openapi/oficina-auth.yaml)

### Evidências de execução

| Ambiente ou contexto | Tipo | Execução |
|---|---|---|
| Homologação | CI | [Run 34794303074](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-auth-serverless/actions/runs/34794303074) |
| Homologação | Deploy Terraform | [Run 34794302992](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-auth-serverless/actions/runs/34794302992) |
| Homologação | Reexecução manual do deploy | [Run 34796371489](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-auth-serverless/actions/runs/34796371489) |
| Produção | CI | [Run 34799909581](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-auth-serverless/actions/runs/34799909581) |
| Produção | Deploy Terraform | [Run 34799909603](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-auth-serverless/actions/runs/34799909603) |
| Produção | Reexecução manual do deploy | [Run 34802109160](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-auth-serverless/actions/runs/34802109160) |
| Execução a partir de `homolog` | Validação funcional E2E | [Run 34796659485](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-backend/actions/runs/34796659485) |
| Execução a partir de `main` | Validação funcional E2E | [Run 34770966649](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-backend/actions/runs/34770966649) |

Os runs foram concluídos com sucesso. As validações E2E executam a collection Postman/Newman e comprovam a emissão e o uso do JWT na integração entre Auth Serverless, Backend e Database.

### Perfis de acesso

A matriz deve ser demonstrada sem publicar tokens, CPFs ou outros dados pessoais.

| Perfil | Acesso esperado |
|---|---|
| `CLIENTE` | Acessa somente as rotas destinadas ao cliente e os recursos que lhe pertencem; não acessa rotas administrativas ou técnicas. |
| `TECNICO_DA_OFICINA` | Acessa as rotas técnicas; não acessa rotas administrativas nem rotas exclusivas de cliente. |
| `FUNCIONARIO_DA_OFICINA` | Acessa rotas administrativas e, pela hierarquia de papéis, também rotas técnicas; não acessa rotas exclusivas de cliente. |

A autenticação deve ser chamada por `POST`. Abrir apenas a URL base no navegador envia uma requisição `GET` e não valida esse fluxo.

### Evidências complementares

- [Swagger — autenticação pelo perfil Cliente](docs-fase3/evidencias/01-autenticacao-api-gateway/Swagger-Perfil-Cliente-Oficina.pdf)
- [Swagger — autenticação pelo perfil Funcionário da Oficina](docs-fase3/evidencias/01-autenticacao-api-gateway/Swagger-Perfil-Funcionario-Oficina.pdf)
- [VÍDEO AUXILIAR: proteção de rotas sensíveis e acesso por perfis cliente e funcionários da oficina](https://vimeo.com/1226754719) — duração informada: 3min50s.

## 2. Quatro repositórios e CI/CD

A solução está dividida em quatro repositórios independentes, cada um com validações de CI e entrega automatizada para homologação e produção.

### Evidências de workflows e produção

| Projeto | Workflows | CI aprovado | Deploy aprovado |
|---|---|---|---|
| Auth | [CI](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-auth-serverless/blob/main/.github/workflows/ci.yml) · [Deploy](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-auth-serverless/blob/main/.github/workflows/terraform-deploy.yml) | [34799909581](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-auth-serverless/actions/runs/34799909581) | [34799909603](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-auth-serverless/actions/runs/34799909603) |
| Kubernetes | [CI](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-kubernetes-infra/blob/main/.github/workflows/ci.yml) · [Deploy de produção](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-kubernetes-infra/blob/main/.github/workflows/deploy-production.yml) | [34797594998](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-kubernetes-infra/actions/runs/34797594998) | [34797595003](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-kubernetes-infra/actions/runs/34797595003) |
| Database | [CI](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-database-infra/blob/main/.github/workflows/ci.yml) · [Terraform apply](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-database-infra/blob/main/.github/workflows/terraform-apply.yml) | [34798911957](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-database-infra/actions/runs/34798911957) | [34798911837](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-database-infra/actions/runs/34798911837) |
| Backend | [CI](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-backend/blob/main/.github/workflows/ci.yml) · [CD](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-backend/blob/main/.github/workflows/cd.yml) | [34800781548](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-backend/actions/runs/34800781548) | [34800781717](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-backend/actions/runs/34800781717) |

Os runs do quadro foram validados como concluídos com `success`. As execuções de homologação e produção estão consolidadas na [documentação de CI/CD](docs-fase3/evidencias/02-cicd/CI-CD.md).

## 3. Governança de branches

As branches `homolog` e `main` dos quatro repositórios possuem rulesets ativos. Eles exigem Pull Request, aprovação dos checks configurados, resolução das conversas e bloqueiam exclusão e force push. A promoção para produção ocorre por Pull Request de `homolog` para `main`.

### Rulesets ativos

| Projeto | `homolog` | `main` |
|---|---|---|
| Auth | [Ruleset de homologação](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-auth-serverless/rules/23168852) | [Ruleset de produção](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-auth-serverless/rules/23169021) |
| Kubernetes | [Ruleset de homologação](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-kubernetes-infra/rules/23075975) | [Ruleset de produção](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-kubernetes-infra/rules/23076125) |
| Database | [Ruleset de homologação](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-database-infra/rules/23075472) | [Ruleset de produção](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-database-infra/rules/23075731) |
| Backend | [Ruleset de homologação](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-backend/rules/23074518) | [Ruleset de produção](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-backend/rules/23070178) |

### Pull Requests de promoção

| Projeto | Promoção direto na main                                                                         | Histórico de Pull Requests |
|---|--------------------------------------------------------------------------------------------------|---|
| Auth | [PR #1](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-auth-serverless/pull/1)  | [Histórico](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-auth-serverless/pulls?q=is%3Apr) |
| Kubernetes | [PR #3](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-kubernetes-infra/pull/3) | [Histórico](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-kubernetes-infra/pulls?q=is%3Apr) |
| Database | [PR #2](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-database-infra/pull/2)   | [Histórico](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-database-infra/pulls?q=is%3Apr) |
| Backend | [PR #3](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-backend/pull/3)          | [Histórico](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-backend/pulls?q=is%3Apr) |

## 4. Infraestrutura em nuvem com Terraform

API Gateway, funções serverless, Amazon RDS e Amazon EKS são provisionados com Terraform para homologação e produção.

### Evidências principais

| Componente | Evidência |
|---|---|
| Rede e EKS | [network.tf](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-kubernetes-infra/blob/main/network.tf) · [eks.tf](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-kubernetes-infra/blob/main/eks.tf) |
| Add-ons Kubernetes | [kubernetes/addons](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-kubernetes-infra/tree/main/kubernetes/addons) |
| RDS PostgreSQL | [main.tf](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-database-infra/blob/main/main.tf) |
| Telemetria do RDS | [telemetry.tf](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-database-infra/blob/main/telemetry.tf) |
| API Gateway | [apigateway.tf](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-auth-serverless/blob/main/apigateway.tf) |
| Funções serverless | [lambda.tf](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-auth-serverless/blob/main/lambda.tf) |
| Notificações assíncronas | [notification.tf](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-auth-serverless/blob/main/notification.tf) |
| Backend Terraform | [versions.tf — Kubernetes](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-kubernetes-infra/blob/main/versions.tf) · [versions.tf — Database](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-database-infra/blob/main/versions.tf) · [versions.tf — Auth](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-auth-serverless/blob/main/versions.tf) |

Os deploys apresentados na seção 2 comprovam a execução automatizada do Terraform. A solução utiliza HCP Terraform e workspaces separados por componente e ambiente.

### Evidências das aplicações do HCP Terraform:

#### Produção

- [Auth — execução](docs-fase3/evidencias/04-terraform-hcp/PRD-TF-auth1.pdf)
- [Auth — reaplicação](docs-fase3/evidencias/04-terraform-hcp/PRD-TF-auth2.pdf)
- [Database](docs-fase3/evidencias/04-terraform-hcp/PRD-TF-Db.pdf)
- [Kubernetes](docs-fase3/evidencias/04-terraform-hcp/PRD-TF-kubernetes.pdf)
- [New Relic](docs-fase3/evidencias/04-terraform-hcp/PRD-TF-newrelic.pdf)

#### Workspaces

- [Workspaces da solução](docs-fase3/evidencias/04-terraform-hcp/TF-Workspaces.pdf)

#### Evidencias auxiliares da aplicabilidade do hcp terraform, em produção e homologação em:

- [Índice das evidências HCP Terraform nos ambientes de homologação e produção](docs-fase3/evidencias/04-terraform-hcp/Terraform-hcp.md)

### Dockerfile e manifestos

- [Dockerfile do Backend](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-backend/blob/main/Dockerfile)
- [Manifestos Kubernetes do Backend](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-backend/tree/main/k8s)

## 5. Aplicação principal no Kubernetes

O Backend é conteinerizado e executado no Kubernetes, com deploy automatizado, healthchecks e escalabilidade.

### Evidências principais

- [Dockerfile do Backend](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-backend/blob/main/Dockerfile)
- [Deployment Kubernetes](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-backend/blob/main/k8s/app-deployment.yaml)
- [Service Kubernetes](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-backend/blob/main/k8s/app-service.yaml)
- [Horizontal Pod Autoscaler](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-backend/blob/main/k8s/hpa.yaml)
- [Deploy de homologação aprovado](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-backend/actions/runs/34795569734)
- [Deploy de produção aprovado](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-backend/actions/runs/34800781717)
- [Collection Postman](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-backend/blob/main/tests/postman/oficina-weeks4-5.postman_collection.json)

### Evidências complementares

- [Probes e réplicas no Deployment](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-backend/blob/main/k8s/app-deployment.yaml)
- [PodDisruptionBudget](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-backend/blob/main/k8s/pdb.yaml)
- [Vídeo auxiliar — ambiente AWS, EKS e aplicação](https://vimeo.com/1226631740)
- [Diretório de evidências do Kubernetes Backend](docs-fase3/evidencias/05-kubernetes-backend/)

As réplicas, probes e o PodDisruptionBudget são evidências complementares de alta disponibilidade e resiliência. O HPA comprova a estratégia de escalabilidade exigida.

## 6. Banco de dados gerenciado e modelo relacional

A solução utiliza PostgreSQL gerenciado no Amazon RDS, com modelo relacional documentado e controles de consistência e desempenho.

### Justificativa da escolha do PostgreSQL

O PostgreSQL oferece transações ACID, integridade referencial, maturidade e suporte gerenciado no Amazon RDS. Sua integração com Spring Data JPA e Flyway atende aos requisitos da aplicação com consistência e baixo custo operacional.

### Evidências principais

- [Terraform do RDS PostgreSQL](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-database-infra/blob/main/main.tf)
- [Justificativa PostgreSQL/RDS — ADR 0001](docs-fase3/evidencias/06-banco-de-dados/ADR_0001_Banco_Relacional_PostgreSQL.docx)
- [Modelo relacional](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-database-infra/blob/main/docs/modelo-relacional.md)
- [Diagrama entidade-relacionamento](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-database-infra/blob/main/docs/diagrams/er-model.svg)
- [Índices e desempenho](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-database-infra/blob/main/docs/indices-desempenho.md)
- [ADR de consistência do modelo](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-database-infra/blob/main/docs/adr/0001-consistencia-modelo.md)
- [Apply de homologação aprovado](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-database-infra/actions/runs/34792773246)
- [Apply de produção aprovado](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-database-infra/actions/runs/34798911837)

### Evidência visual de conexão ao banco de dados PostgreSQL

- [Conexão aos bancos PostgreSQL de homologação e produção](docs-fase3/evidencias/06-banco-de-dados/Evidencia-Conexao-BD.docx)

## 7. Monitoramento, observabilidade e logs

O New Relic centraliza métricas, logs e traces do Backend, das funções serverless, do Kubernetes e do RDS. Os dashboards acompanham saúde, desempenho e requisições correlacionadas por `correlationId` e `traceId`.

### Evidências de implementação como código

- [Dashboard New Relic](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-kubernetes-infra/blob/main/observability/newrelic/dashboard.tf)
- [Alertas da plataforma](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-kubernetes-infra/blob/main/observability/newrelic/alerts.tf)
- [Alertas do RDS](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-kubernetes-infra/blob/main/observability/newrelic/rds-alerts.tf)
- [Monitor sintético](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-kubernetes-infra/blob/main/observability/newrelic/synthetics.tf)
- [Instrumentação do Auth](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-auth-serverless/blob/main/newrelic.tf)
- [Telemetria do Database](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-database-infra/blob/main/telemetry.tf)
- [Documentação de observabilidade do Backend](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-backend/blob/main/docs/observabilidade-evidencias.md)
- [ADR de logs, correlação e traces](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-backend/blob/main/docs/decisions/adr/0004-logs-correlacao-traces.md)

### Evidências operacionais

- [New Relic — consumo de CPU](docs-fase3/evidencias/07-Monitoramento/NR-CPU.png)
- [New Relic — disponibilidade da aplicação](docs-fase3/evidencias/07-Monitoramento/NR-Disponibilidade.png)
- [New Relic — falhas nas ordens de serviço](docs-fase3/evidencias/07-Monitoramento/NR-Falhas-OS.png)
- [New Relic — latência das APIs](docs-fase3/evidencias/07-Monitoramento/NR-latencia.png)
- [New Relic — logs da aplicação](docs-fase3/evidencias/07-Monitoramento/NR-Logs.png)
- [New Relic — tempo médio por status da ordem de serviço](docs-fase3/evidencias/07-Monitoramento/NR-Media-Status-OS.png)
- [New Relic — volume diário de ordens de serviço](docs-fase3/evidencias/07-Monitoramento/NR-Vol-OS-dia.png)
- [Vídeo auxiliar — dashboards, logs e traces](https://vimeo.com/1226611174) — duração informada: 4min08s.

## 8. Documentação arquitetural, RFCs e ADRs

A documentação apresenta a arquitetura, os fluxos principais e as decisões técnicas por meio de diagramas, RFCs e ADRs.

| Evidência | Link |
|---|---|
| Índice central | [docs/README.md](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-backend/blob/main/docs/README.md) |
| Diagrama de componentes | [componentes.md](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-backend/blob/main/docs/architecture/componentes.md) |
| Sequência de autenticação | [autenticacao.md](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-backend/blob/main/docs/architecture/autenticacao.md) |
| Sequência de abertura da OS | [abertura-ordem-servico.md](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-backend/blob/main/docs/architecture/abertura-ordem-servico.md) |
| RFCs | [docs/decisions/rfc](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-backend/tree/main/docs/decisions/rfc) |
| ADRs | [docs/decisions/adr](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-backend/tree/main/docs/decisions/adr) |
| Modelo relacional | [modelo-relacional.md](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-database-infra/blob/main/docs/modelo-relacional.md) |
| Diagrama ER | [er-model.svg](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-database-infra/blob/main/docs/diagrams/er-model.svg) |
| Arquitetura do Auth | [arquitetura.md](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-auth-serverless/blob/main/docs/arquitetura.md) |
| Infraestrutura e observabilidade | [infraestrutura-observabilidade.md](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-kubernetes-infra/blob/main/docs/infraestrutura-observabilidade.md) |

## 9. READMEs e contratos dos quatro repositórios

Cada repositório documenta propósito, tecnologias, pré-requisitos, execução, deploy, pipeline, arquitetura e contratos aplicáveis.

| Projeto | README |
|---|---|
| Auth | [README do Auth](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-auth-serverless/blob/main/README.md) |
| Kubernetes | [README do Kubernetes](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-kubernetes-infra/blob/main/README.md) |
| Database | [README do Database](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-database-infra/blob/main/README.md) |
| Backend | [README do Backend](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-backend/blob/main/README.md) |

### Contratos e testes de API

- [OpenAPI do Auth](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-auth-serverless/blob/main/docs/openapi/oficina-auth.yaml)
- [Collection Postman/Newman](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-backend/blob/main/tests/postman/oficina-weeks4-5.postman_collection.json)
- [Configuração OpenAPI/Swagger do Backend](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-backend/blob/main/src/main/java/br/com/oficina/infrastructure/config/OpenApiConfig.java)
- [Evidência do Swagger — perfil Cliente](docs-fase3/evidencias/01-autenticacao-api-gateway/Swagger-Perfil-Cliente-Oficina.pdf)
- [Evidência do Swagger — perfil Funcionário](docs-fase3/evidencias/01-autenticacao-api-gateway/Swagger-Perfil-Funcionario-Oficina.pdf)

As URLs operacionais anteriores do Swagger e do API Gateway não foram mantidas como evidência permanente porque os endpoints temporários da AWS Academy não estão mais resolvendo. As URLs vigentes devem ser reconfirmadas imediatamente antes da gravação e da entrega final.

## 10. Documentação central e fechamento da entrega

O repositório central reúne diagramas, decisões arquiteturais e registros de validação da solução.


consegue colocar o link para abrir a pasta [docs-fase3](docs-fase3)?
