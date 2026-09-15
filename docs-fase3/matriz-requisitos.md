# Matriz de requisitos acadêmicos

| Requisito oficial | Documento principal | Evidência ou estado |
|---|---|---|
| Contexto, funcionalidades e evolução | [Visão de negócio e engenharia](evidencias/visao-negocio-e-engenharia.md) | Jornada da OS e evolução Fase 2 → Fase 3 |
| Modelo arquitetural e práticas | [Visão de negócio e engenharia](evidencias/visao-negocio-e-engenharia.md#5-modelo-arquitetural-por-aplicação) | Clean Architecture, serverless e Infrastructure as Code |
| API Gateway e rotas protegidas | [Componentes](architecture/componentes.md) | Implementado no projeto Auth |
| Function Serverless por CPF | [Autenticação](architecture/autenticacao.md) | Validação, consulta do cliente e emissão JWT |
| Quatro projetos independentes | [README central](../README.md#aplicações-da-solução) | Backend, Auth, Database e Kubernetes |
| CI/CD em cada projeto | [Ciclos CI/CD](evidencias/02-cicd/cicd-promocao.md) | Workflows e runs em [Evidências](evidencias.md) |
| `main` protegida e uso de PR | [Ciclos CI/CD](evidencias/02-cicd/cicd-promocao.md) | Confirmação final deve ser anexada |
| Homologação e produção | [Ciclos CI/CD](evidencias/02-cicd/cicd-promocao.md) | Ambientes, branches e workspaces separados |
| Kubernetes, HPA e alta disponibilidade | [ADR 0003](decisions/adr/0003-alta-disponibilidade-hpa.md) | EKS, HPA, PDB, probes e distribuição |
| Banco gerenciado e justificativa | [RFC 0002](decisions/rfc/0002-postgresql-rds.md) | PostgreSQL 16 no RDS privado |
| Modelo relacional e ER | [Database docs](https://github.com/tiagomiele/database) | Modelo, cardinalidades, consistência e índices |
| Diagrama de componentes | [Arquitetura integrada](architecture/componentes.md) | Nuvem, APIs, EKS, RDS, Lambda e New Relic |
| Sequência de autenticação | [Fluxo de autenticação](architecture/autenticacao.md) | Diagrama Mermaid |
| Sequência de abertura da OS | [Fluxo de abertura](architecture/abertura-ordem-servico.md) | Diagrama Mermaid |
| RFCs e ADRs | [README central](../README.md#decisões-arquiteturais) | Nuvem, banco, autenticação, observabilidade, comunicação, HPA e logs |
| Monitoramento e observabilidade | [Observabilidade](evidencias/07-Monitoramento/observabilidade-evidencias.md) | New Relic; evidências finais pendentes |
| Logs JSON e correlação | [ADR 0004](decisions/adr/0004-logs-correlacao-traces.md) | Links de logs e traces pendentes |
| Swagger ou Postman | [Evidências](evidencias.md#apis) | Swagger, Postman e OpenAPI |
| Testes e E2E | [Evidências](evidencias.md) | CI, Newman, E2E e k6 |
| Bootstrap reproduzível | [Bootstrap AWS](bootstrap-aws-do-zero.md) | Preparação, deploy, promoção e validação |
| Vídeo de até 15 minutos | [Evidências finais](evidencias.md#evidências-finais-ainda-necessárias) | Pendente |
| PDF único da entrega | [Evidências finais](evidencias.md#evidências-finais-ainda-necessárias) | Pendente |
| Usuário `soat-architecture` | [Evidências finais](evidencias.md#evidências-finais-ainda-necessárias) | Confirmação pendente |

> URLs e evidências do AWS Academy devem ser atualizadas depois da última execução utilizada na apresentação.
