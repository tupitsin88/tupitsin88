# Тимофей Тупицин

**Go Backend Developer Intern**  
ФКН НИУ ВШЭ, Программная инженерия `2024-2028`

Пишу backend-сервисы на Go. Основной фокус: REST API, PostgreSQL, Redis, Docker, CI/CD, миграции, auth-сценарии и асинхронная обработка событий.

## Стек

![Go](https://img.shields.io/badge/Go-00ADD8?style=flat&logo=go&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-316192?style=flat&logo=postgresql&logoColor=white)
![Redis](https://img.shields.io/badge/Redis-DC382D?style=flat&logo=redis&logoColor=white)
![Kafka](https://img.shields.io/badge/Kafka-231F20?style=flat&logo=apachekafka&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat&logo=docker&logoColor=white)
![GitHub Actions](https://img.shields.io/badge/GitHub_Actions-2088FF?style=flat&logo=githubactions&logoColor=white)
![OpenAPI](https://img.shields.io/badge/OpenAPI-6BA539?style=flat&logo=openapiinitiative&logoColor=white)

## Ключевые backend-проекты

Для командных и закрытых проектов ниже разделяю общий масштаб проекта и мою зону ответственности.

| Проект | Роль / контекст | Backend | Что посмотреть |
|---|---|---|---|
| [StillGood Backend](https://github.com/tupitsin88/stillgood-backend) | Командный backend MVP food-sharing платформы. Моя зона: auth/users, email/OTP flows, refresh-сессии, часть инфраструктуры и API-контрактов. | В проекте также есть restaurants, offers, orders, partner flows, analytics, notifications, admin API/UI, media storage. | OpenAPI, migrations, Docker Compose, GitHub Actions, unit/integration tests. |
| [Gozon Async Shop](https://github.com/tupitsin88/Gozon-async-shop) | Учебная e-commerce система с асинхронной обработкой заказов. | Два Go-сервиса, Kafka, PostgreSQL, API Gateway, WebSocket-статусы, Transactional Outbox и Inbox/deduplication. | Docker Compose запуск, Swagger-файлы, обработка сбоя между записью в БД и публикацией события. |
| [MerchCRM Yandex](./merchcrm-case-study) | Приватный ongoing-проект для Yandex. Код закрыт в Sourcecraft, поэтому публично показываю только безопасный backend/infra case study. | Yandex OAuth, Redis-backed sessions, auth middleware, Docker Compose orchestration, Liquibase migrations, CI quality gates. | Описание архитектуры, auth flow и infrastructure setup без исходного кода, секретов, внутренних URL и бизнес-данных. |

## Дополнительные проекты

- [Antiplagiat](https://github.com/tupitsin88/Antiplagiat) - учебная микросервисная система проверки документов: REST, Docker, PostgreSQL, background analysis, Jaccard similarity.
- [LogsParser](https://github.com/tupitsin88/LogsParser) - Go-сервис для загрузки лог-файлов, парсинга, агрегации и выдачи данных через REST API.
- [Zoo ERP System](https://github.com/tupitsin88/Zoo-ERP-system) - консольный Go-проект для отработки SOLID, interfaces, DI и unit tests.
