# Evidências da entrega

Este documento centraliza links reproduzíveis. URLs do AWS Academy devem ser atualizadas após a reconstrução dos ambientes.

## APIs

| Evidência | Link |
|---|---|
| Swagger e instruções locais | [README do Backend](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-backend#executar-localmente) |
| Collection Postman | [Fluxos integrados](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-backend/blob/main/tests/postman/oficina-weeks4-5.postman_collection.json) |
| Ambiente Postman de exemplo | [Homologação](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-backend/blob/main/tests/postman/oficina-homolog.postman_environment.example.json) |
| OpenAPI da autenticação | [Contrato Auth](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-auth-serverless/blob/main/docs/openapi/oficina-auth.yaml) |
| Swagger ativo de homologação | Inserir após o deploy |
| Swagger ativo de produção | Inserir após o deploy |
| API Gateway ativo | Inserir após o deploy |

## Testes automatizados

| Projeto | Cobertura |
|---|---|
| Backend | JUnit 5, integração, RestAssured, ArchUnit, JaCoCo, Spotless, SBOM, Trivy e Gitleaks |
| Auth | JUnit, arquitetura, pacote Lambda, Terraform e segurança |
| Database | Terraform, testes Python, Checkov, Trivy e Gitleaks |
| Kubernetes | Terraform, Python, scripts, Helm, actionlint e segurança |

Links dos workflows:

- [CI Backend](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-backend/actions/workflows/ci.yml)
- [CI Auth](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-auth-serverless/actions/workflows/ci.yml)
- [CI Database](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-database-infra/actions/workflows/ci.yml)
- [CI Kubernetes](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-kubernetes-infra/actions/workflows/ci.yml)

## Deploys utilizados como evidência

- [Backend CD](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-backend/actions/runs/34538895450)
- [Auth deploy](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-auth-serverless/actions/runs/34543127750)
- [Database apply](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-database-infra/actions/runs/34529053307)
- [Kubernetes production](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-kubernetes-infra/actions/runs/34524817503)

## Validação E2E

- [Workflow E2E](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-backend/actions/workflows/e2e.yml)
- [Execução E2E de referência](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-backend/actions/runs/34544086642)
- [Collection executada pelo Newman](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-backend/blob/main/tests/postman/oficina-weeks4-5.postman_collection.json)
- [Carga controlada k6](https://github.com/tiagomiele/fiap-tech-challenge-fase3-oficina-backend/blob/main/tests/k6/smoke-load.js)

O E2E deve demonstrar autenticação por CPF, geração e uso do JWT, rotas protegidas, privacidade entre clientes e fluxo de ordens de serviço.

## Observabilidade

Os locais para anexar dashboards, logs, traces e prints estão em [Observabilidade e evidências](observabilidade-evidencias.md).

## Evidências finais ainda necessárias

- [ ] URLs ativas após a última reconstrução AWS.
- [ ] Dashboard com volume diário de ordens de serviço.
- [ ] Dashboard com tempo médio de diagnóstico, execução e finalização.
- [ ] Dashboard com falhas de ordens e integrações.
- [ ] Logs JSON com correlação visível.
- [ ] Trace distribuído entre API Gateway, Lambda e Backend.
- [ ] Vídeo de até 15 minutos no YouTube ou Vimeo.
- [ ] Confirmação de `soat-architecture` nos quatro projetos.
- [ ] PDF único com todos os links da entrega.
