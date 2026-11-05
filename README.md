# ByteCare QA - Sprint 4 (ClyvoVet)

Este repositório contém os artefatos de automação de testes de API (Postman) e o resumo da execução dos testes manuais, feitos para o sistema ClyvoVet (API .NET publicada no Azure).

## 🚀 Artefatos de Automação (Postman)

- Collection: `ByteCare - Automação QA Sprint 4.postman_collection.json`
- Environment: `ByteCare-Azure.postman_environment.json`

### Variáveis do ambiente (ByteCare-Azure)

| Variável | Descrição | Valor inicial (Git) |
|---|---|---|
| baseUrl | URL base da API publicada no Azure | https://clyvo-sprint4-rm564361.azurewebsites.net |
| password | Senha do usuário admin | (em branco por segurança) |
| jwt_token | Token JWT, preenchido pelo script do request 01 | (em branco) |

### Como executar

1. Baixe ou clone a branch `develop`.
2. No Postman, use **Import** para carregar a collection e o environment.
3. Selecione o ambiente **ByteCare-Azure**.
4. Preencha o campo **password** (Current value) com a senha do usuário admin.
5. Abra a collection e clique em **Run collection**, depois em **Start run**.
6. Resultado esperado: 4 requests e 7 testes passando. A primeira chamada pode demorar, porque o plano gratuito do Azure pode estar em repouso.

### Casos automatizados

| # | Request | Valida |
|---|---|---|
| 01 | POST /api/Auth/login | HTTP 200 e token JWT retornado (token guardado em jwt_token) |
| 02 | POST /api/Auth/login com senha inválida | HTTP 401 e nenhum token retornado |
| 03 | GET /api/Animal/{id inexistente} | HTTP 404 |
| 04 | GET /api/Animal/{id do Rex} | HTTP 200 e dados do Rex (nome, espécie, raça, sexo, peso) |

Observação: a API publicada não exige token nas rotas de animal (Bug #73). Por isso, os requests 03 e 04 passam com ou sem autenticação, e a collection não valida a proteção de rotas.

## 📊 Testes manuais (Azure DevOps)

Executados manualmente no Swagger em 04/11/2026 e registrados nos Test Plans do Azure Boards.

| CT | PBI | O que valida | Status | Observações |
|---|---|---|---|---|
| CT-01 | Cadastro de Perfil de Tutor e Animal | Cadastro válido de tutor e pet (HTTP 201) e consulta do animal criado | PASSED | |
| CT-02 | Cadastro de Perfil de Tutor e Animal | Rejeição de pet com data de nascimento futura (HTTP 422) | PASSED | |
| CT-03 | Agendamento de Consulta | Agendamento de consulta presencial (HTTP 201) e status "Agendada" | PASSED | |
| CT-04 | Consulta de Animal por ID | Busca por ID existente (200) e inexistente (404) | PASSED | |
| CT-05 | Cálculo de Idade e Triagem de Urgência | Triagem por IA e histórico da avaliação | FAILED | Bug #72: GET /api/RecomendacaoIa e /animal/{id} retornaram [] após criar a avaliação |
| CT-06 | Autenticação via JWT | Login válido e inválido e bloqueio de rota sem token | FAILED | Bug #73: GET /api/Animal retornou 200 sem Authorization, e DELETE /api/Animal/{id} respondeu 204 sem Authorization |

## 🔗 Links do projeto

- Azure Boards (planejamento, Test Cases e Bugs): https://dev.azure.com/bytecare-challenge2026/ByteCare%20Challenge%202026
- Swagger UI da API: https://clyvo-sprint4-rm564361.azurewebsites.net/swagger/index.html
- Vídeo da automação (Postman Runner): https://youtu.be/00Wa1t40F4c
