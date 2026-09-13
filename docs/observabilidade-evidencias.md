# Observabilidade e evidências

## Objetivo

Comprovar que a solução permite acompanhar disponibilidade, desempenho e falhas durante a passagem de uma requisição pelos componentes.

## Cobertura esperada no New Relic

| Área | Evidência esperada |
|---|---|
| APIs | Latência, throughput, erros HTTP e disponibilidade |
| Kubernetes | CPU, memória, nós, pods, namespace e HPA |
| Saúde | Startup, liveness, readiness e monitor sintético |
| Ordens de serviço | Volume diário e falhas de processamento |
| Etapas da OS | Tempo médio em diagnóstico, execução e finalização |
| Integrações | Falhas em API Gateway, Lambda, RDS e notificações |
| Correlação | Logs JSON com `correlationId` ou `traceId` |
| Tracing | Caminho da requisição entre API Gateway, Lambda e Backend |

## Links para evidências após a execução

Preencher somente depois de reconstruir e validar o ambiente:

- **Dashboard geral de homologação:** inserir link.
- **Dashboard geral de produção:** inserir link.
- **Volume diário de ordens de serviço:** inserir link ou imagem.
- **Tempos médios por etapa:** inserir link ou imagem.
- **Falhas de ordens e integrações:** inserir link ou imagem.
- **CPU e memória do Kubernetes:** inserir link ou imagem.
- **Healthcheck e disponibilidade:** inserir link ou imagem.
- **Logs estruturados correlacionados:** inserir link ou imagem.
- **Trace distribuído:** inserir link ou imagem.

## Critério de validação

1. Execute um fluxo autenticado completo.
2. Preserve o `correlationId` ou `traceId` retornado ou registrado.
3. Localize a requisição no APM e nos logs.
4. Confirme o trajeto entre API Gateway, Lambda e Backend.
5. Confira métricas do pod durante a execução.
6. Valide a atualização dos widgets de ordens e falhas.
7. Registre links ou imagens para o PDF e o vídeo.

## Segurança das evidências

Não publique CPF completo, JWT, senhas, chaves, tokens, conexão JDBC ou conteúdo de secrets. Logs e screenshots devem mascarar dados pessoais e credenciais.

## Referências

- [Infraestrutura e observabilidade](https://github.com/tiagomiele/kubernetes/blob/documentation/docs/infraestrutura-observabilidade.md)
- [RFC de observabilidade](decisions/rfc/0004-observabilidade-new-relic.md)
- [ADR de logs e correlação](decisions/adr/0004-logs-correlacao-traces.md)
