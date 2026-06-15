# openfin-lab

Uma **simulação educacional** do ecossistema Open Finance Brasil, construída com Java + Quarkus + Docker para estudo de arquitetura, segurança (OAuth2/OIDC/FAPI) e boas práticas de engenharia.

> ⚠️ **Aviso:** projeto de aprendizado. Não se conecta ao ambiente real regulado, não processa dados reais e **não** é uma implementação certificada do Open Finance Brasil. Os schemas das APIs são baseados nas especificações públicas apenas para fins didáticos.

## Objetivos de aprendizado

- Arquitetura hexagonal (ports & adapters) e separação de contextos.
- Fluxo de consentimento e compartilhamento de dados ponta a ponta.
- Segurança com OAuth2, OpenID Connect e conceitos de FAPI.
- Quarkus na prática: dev mode, Panache, OIDC, Dev Services, build nativo.
- Containerização com Docker e `docker-compose`.
- Versionamento, testes (unitários e de integração) e CI/CD.

## Participantes simulados

| Participante      | Papel                                                          |
|-------------------|---------------------------------------------------------------|
| `transmissora`    | O "banco". Resource Server + Authorization Server. Guarda contas/transações e gerencia consentimentos. |
| `receptora`       | A fintech (TPP). Solicita consentimento e consome os dados.    |
| Keycloak          | Authorization Server (OAuth2/OIDC), provido via Dev Services.  |

## Fluxo de compartilhamento de dados (Fase 2)

1. O usuário inicia a conexão na **receptora**.
2. A receptora cria o consentimento na transmissora (`POST /consents`).
3. A receptora redireciona o usuário para a autorização (OAuth2 + OIDC).
4. O usuário se autentica no "banco" e autoriza o consentimento.
5. O Authorization Server emite o token (fluxo `authorization_code`).
6. A receptora consome as APIs de dados (`GET /accounts`, `/transactions`).
7. A transmissora valida o consentimento e o token, e devolve os dados.

## Stack

- Java 21 (LTS)
- Quarkus (linha LTS)
- PostgreSQL + Hibernate ORM with Panache + Flyway
- Keycloak (OIDC) via Quarkus Dev Services
- Docker / docker-compose
- JUnit 5, RestAssured, Testcontainers
- GitHub Actions (CI)

## Estrutura do repositório

```
openfin-lab/
├── transmissora/     # banco: APIs de contas + consentimento (Quarkus)
├── receptora/        # fintech/TPP: consome os dados (Quarkus) — entra na Fase 6
├── ROADMAP.md
└── README.md
```

## Como rodar (dev mode)

Pré-requisitos: JDK 21, Maven (ou o `mvnw` incluso), Docker.

```bash
cd transmissora
./mvnw quarkus:dev      # Windows: .\mvnw quarkus:dev
```

- Aplicação: http://localhost:8080
- Dev UI do Quarkus: http://localhost:8080/q/dev

## Roadmap

O plano completo, em níveis de fidelidade e fases, está em [ROADMAP.md](./ROADMAP.md).

## Referências oficiais

- Área do Desenvolvedor — Open Finance Brasil: https://openfinancebrasil.atlassian.net/wiki/spaces/OF
- Especificações OpenAPI (GitHub): https://github.com/OpenBanking-Brasil/openapi
- Suíte de conformidade (GitHub): https://github.com/OpenBanking-Brasil/conformance
- Open Finance no Banco Central: https://www.bcb.gov.br/estabilidadefinanceira/openfinance

## Licença

MIT (uso educacional).
