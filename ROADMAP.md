# Roadmap — openfin-lab

Plano de evolução do projeto. Cada fase fecha um marco versionável no GitHub.

## Níveis de fidelidade

O quão "fiel" à regulação queremos chegar. Cada nível é um marco completo.

- **Nível 1 — MVP didático:** OAuth2/OIDC com Keycloak, consentimento + APIs de contas com schemas reais, tudo em HTTP. Foco em arquitetura e no fluxo funcionando ponta a ponta.
- **Nível 2 — realista:** assinatura de payloads (JWS), headers FAPI (`x-fapi-interaction-id`), DCR simplificado, paginação e erros no padrão.
- **Nível 3 — fiel à regulação:** mTLS com certificados, *certificate-bound tokens*, PAR e, opcionalmente, rodar contra a suíte de conformidade.

> Estamos começando pelo **Nível 1**.

## Fases

- [ ] **Fase 1 — Fundação**
  - [ ] Mono-repo + `git init`
  - [ ] README e ROADMAP
  - [ ] Convenções de commit (Conventional Commits) e estratégia de branches
  - [ ] Repositório no GitHub + primeiro push

- [ ] **Fase 2 — Transmissora: scaffold + API de contas**
  - [ ] Projeto Quarkus gerado
  - [ ] Endpoint `GET /accounts` com dados em memória
  - [ ] Dev mode e hot reload validados

- [ ] **Fase 3 — Domínio + arquitetura hexagonal**
  - [ ] Camadas `domain` / `application` / `infrastructure`
  - [ ] Contextos `accounts` e `consent`
  - [ ] Entidades e value objects

- [ ] **Fase 4 — Persistência**
  - [ ] PostgreSQL + Hibernate ORM with Panache
  - [ ] Migrations com Flyway
  - [ ] Repositórios

- [ ] **Fase 5 — Consentimento**
  - [ ] Ciclo de vida: `AWAITING_AUTHORISATION → AUTHORISED → CONSUMED/REJECTED`
  - [ ] API `/consents` seguindo o schema oficial

- [ ] **Fase 6 — Segurança / OIDC**
  - [ ] Keycloak via Dev Services
  - [ ] Recursos protegidos por escopo
  - [ ] Fluxo `authorization_code`
  - [ ] Receptora consumindo os dados ponta a ponta

- [ ] **Fase 7 — Testes**
  - [ ] Unitários no domínio (JUnit 5 + Mockito)
  - [ ] Integração com Testcontainers (Postgres + Keycloak) e RestAssured
  - [ ] Teste de contrato contra o OpenAPI
  - [ ] Cobertura com JaCoCo

- [ ] **Fase 8 — Docker**
  - [ ] Dockerfile multi-stage (JVM)
  - [ ] `docker-compose` com as duas apps + Keycloak + Postgres
  - [ ] Build nativo (GraalVM/Mandrel)

- [ ] **Fase 9 — Realismo Open Finance (Nível 2)**
  - [ ] JWS nos payloads
  - [ ] Headers FAPI
  - [ ] DCR simplificado
  - [ ] Tratamento de erros padronizado

- [ ] **Fase 10 — CI/CD + avançado**
  - [ ] GitHub Actions (build + testes + imagem)
  - [ ] Observabilidade (health, métricas, logs)
  - [ ] Debug em container
  - [ ] Opcional: mTLS / conformância (Nível 3)
