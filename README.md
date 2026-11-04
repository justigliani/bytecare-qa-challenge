# ByteCare QA - Sprint 4 (ClyvoVet)

Este repositório contém os artefatos de automação de testes de API (Postman) e a documentação completa de garantia de qualidade desenvolvida para o sistema ClyvoVet.

---

## 🚀 Artefatos de Automação (Postman)

- **Collection:** `ByteCare - Automação QA Sprint 4.postman_collection.json`
- **Environment:** `ByteCare-Azure.postman_environment.json`

### 📋 Variáveis do Ambiente (`ByteCare-Azure`)

| Variável | Descrição | Valor Inicial (Git) |
| :--- | :--- | :--- |
| `baseUrl` | URL base da API implantada no Azure | `https://clyvo-sprint4-rm564361.azurewebsites.net` |
| `password` | Senha de autenticação do usuário `admin` | *(em branco por segurança)* |
| `jwt_token` | Token Bearer preenchido automaticamente via script | *(preenchido dinamicamente)* |

---

## 🛠️ Como Executar a Automação no Postman

1. Faça o download ou clone a branch `develop` deste repositório.
2. No Postman, utilize a opção **Import** para carregar os arquivos da Coleção e do Ambiente (`.json`).
3. Selecione o ambiente **ByteCare-Azure** no canto superior direito.
4. Preencha a variável `password` no campo `Current Value` com a senha do usuário `admin`.
5. Abra a coleção **ByteCare - Automação QA Sprint 4** e clique em **Run collection**.
6. Clique no botão **Start run** para executar a suíte automatizada (todas as 7 asserções retornarão `PASS`).

---

## 📊 Matriz de Execução e Status dos Test Cases (Azure DevOps)

| ID / CT | Descrição do Caso de Teste | Status | Observações / Defeitos Relacionados |
| :--- | :--- | :--- | :--- |
| **CT-01 a CT-04** | Suíte de Testes Manuais e Regressivos da Aplicação | `PASSED` | Testes de regressão executados com sucesso nas Sprints anteriores. |
| **CT-05** | Validar triagem clínica de urgência e histórico por IA | `FAILED` | **Bug #72:** As rotas `GET /api/RecomendacaoIa` e `/animal/{id}` retornaram lista vazia `[]` após criação da avaliação. |
| **CT-06** | Validar autenticação JWT e bloqueio de rota sem token | `FAILED` | **Bug #73:** O Passo 1 falhou pois a rota `GET /api/Animal` (e demais GETs) retornou `200 OK` sem o envio do cabeçalho `Authorization`. |

---

## 🔗 Links do Projeto

- 📌 **Azure Boards (Planejamento, Test Cases e Bugs):** <https://dev.azure.com/bytecare-challenge2026/ByteCare%20Challenge%202026/_boards/board/t/ByteCare%20Challenge%202026%20Team/Backlog%20items>
- 🌐 **Swagger UI (Documentação da API):** https://clyvo-sprint4-rm564361.azurewebsites.net/swagger/index.html
- 🚀 **Postman
