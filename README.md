<h1 align="center">Timofey Tupitsin</h1>

<p align="center"><strong>Go backend · API · надёжность и производительность</strong></p>

<p align="center">Здесь — проекты, в которых можно посмотреть, как я решаю backend-задачи: атомарность, обработку событий, работу под нагрузкой и восстановление после сбоев.</p>

<p align="center">
  <a href="https://go.dev/"><img src="https://img.shields.io/badge/Go-00ADD8?style=flat&amp;logo=go&amp;logoColor=white" alt="Go"></a>
  <a href="https://www.postgresql.org/"><img src="https://img.shields.io/badge/PostgreSQL-316192?style=flat&amp;logo=postgresql&amp;logoColor=white" alt="PostgreSQL"></a>
  <a href="https://redis.io/"><img src="https://img.shields.io/badge/Redis-DC382D?style=flat&amp;logo=redis&amp;logoColor=white" alt="Redis"></a>
  <a href="https://kafka.apache.org/"><img src="https://img.shields.io/badge/Kafka-231F20?style=flat&amp;logo=apachekafka&amp;logoColor=white" alt="Kafka"></a>
  <a href="https://www.docker.com/"><img src="https://img.shields.io/badge/Docker-2496ED?style=flat&amp;logo=docker&amp;logoColor=white" alt="Docker"></a>
  <a href="https://github.com/features/actions"><img src="https://img.shields.io/badge/GitHub_Actions-2088FF?style=flat&amp;logo=githubactions&amp;logoColor=white" alt="GitHub Actions"></a>
  <a href="https://www.openapis.org/"><img src="https://img.shields.io/badge/OpenAPI-6BA539?style=flat&amp;logo=openapiinitiative&amp;logoColor=white" alt="OpenAPI"></a>
  <a href="https://prometheus.io/"><img src="https://img.shields.io/badge/Prometheus-E6522C?style=flat&amp;logo=prometheus&amp;logoColor=white" alt="Prometheus"></a>
  <a href="https://grafana.com/"><img src="https://img.shields.io/badge/Grafana-F46800?style=flat&amp;logo=grafana&amp;logoColor=white" alt="Grafana"></a>
</p>

---

## Проекты

### 🚦 [Rate Limiter](https://github.com/tupitsin88/ratelimiter)

Распределённый Token Bucket на Go и Redis. Lua-скрипт атомарно проверяет и списывает токены; если Redis недоступен, сервис переключается на локальный лимит.

- **Производительность:** p99 снизился с 1,3 до 0,2 мс при 10 000 запросах/с благодаря локальному кэшу и шардированным блокировкам.
- **В проекте:** HTTP middleware, метрики Prometheus и нагрузочные прогоны через `vegeta`.
- **Смотреть:** [`tiered.go`](https://github.com/tupitsin88/ratelimiter/blob/main/tiered.go) · [`token_bucket.lua`](https://github.com/tupitsin88/ratelimiter/blob/main/token_bucket.lua) · [результаты нагрузочного тестирования](https://github.com/tupitsin88/ratelimiter/blob/main/RESULTS.md)

### 🍲 [StillGood Backend](https://github.com/tupitsin88/stillgood-backend)

Backend командного MVP для бронирования еды со скидкой. Моя зона — авторизация, роли и API-контракты.

- JWT access-токены и refresh-сессии в PostgreSQL с отзывом сессий между экземплярами API.
- Unit-тесты на Go с Testify и проверки в CI.
- **Смотреть:** [`internal/auth`](https://github.com/tupitsin88/stillgood-backend/tree/main/internal/auth) · [OpenAPI-контракт](https://github.com/tupitsin88/stillgood-backend/blob/main/docs/openapi.yaml) · [CI workflows](https://github.com/tupitsin88/stillgood-backend/tree/main/.github/workflows)

### 🛒 [Gozon Async Shop](https://github.com/tupitsin88/Gozon-async-shop)

Учебная e-commerce система с отдельными сервисами заказов и платежей. Проект показывает асинхронный обмен событиями и обновление статуса заказа через WebSocket.

- Transactional Outbox, Inbox-дедупликация и идемпотентная обработка событий.
- **Смотреть:** [`orders`](https://github.com/tupitsin88/Gozon-async-shop/tree/main/orders) · [`payments`](https://github.com/tupitsin88/Gozon-async-shop/tree/main/payments) · [`docker-compose.yml`](https://github.com/tupitsin88/Gozon-async-shop/blob/main/docker-compose.yml)

---

**Ещё:** [Antiplagiat](https://github.com/tupitsin88/Antiplagiat) · [LogsParser](https://github.com/tupitsin88/LogsParser) · [MerchCRM — case study](https://github.com/tupitsin88/tupitsin88/blob/main/merchcrm-case-study)

<p align="center">
  <a href="https://t.me/same_one1"><img src="https://img.shields.io/badge/Telegram-связаться-26A5E4?style=flat&logo=telegram&logoColor=white" alt="Написать в Telegram"></a>
</p>
