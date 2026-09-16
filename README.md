# Тимофей Тупицин

**Go Backend Developer Intern**  
ФКН НИУ ВШЭ, Программная инженерия `2024-2028`

Пишу backend-сервисы на Go с фокусом на отказоустойчивость и производительность: проектирование БД и API, интеграция брокеров сообщений, кэширование, профилирование горячего пути и нагрузочное тестирование.

## Стек

![Go](https://img.shields.io/badge/Go-00ADD8?style=flat&logo=go&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-316192?style=flat&logo=postgresql&logoColor=white)
![Redis](https://img.shields.io/badge/Redis-DC382D?style=flat&logo=redis&logoColor=white)
![Kafka](https://img.shields.io/badge/Kafka-231F20?style=flat&logo=apachekafka&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat&logo=docker&logoColor=white)
![GitHub Actions](https://img.shields.io/badge/GitHub_Actions-2088FF?style=flat&logo=githubactions&logoColor=white)
![OpenAPI](https://img.shields.io/badge/OpenAPI-6BA539?style=flat&logo=openapiinitiative&logoColor=white)
![Prometheus](https://img.shields.io/badge/Prometheus-E6522C?style=flat&logo=prometheus&logoColor=white)
![Grafana](https://img.shields.io/badge/Grafana-F46800?style=flat&logo=grafana&logoColor=white)

## Ключевые backend-проекты

Ниже описаны основные проекты, стек и моя зона ответственности, а также на что стоит обратить внимание при просмотре репозиториев.

| Проект | Роль / контекст | Архитектура и стек | Что посмотреть в коде |
|---|---|---|---|
| [Rate Limiter](https://github.com/tupitsin88/ratelimiter) | Pet-проект. Распределённый сервис защиты от пиковых перегрузок. | Go, Redis, Lua. Двухуровневое кэширование (local + Redis). Отказоустойчивость при падении внешних узлов. | Использование Lua-скриптов, fallback-механизмы, метрики Prometheus/Grafana и результаты нагрузочного тестирования (vegeta). |
| [StillGood Backend](https://github.com/tupitsin88/stillgood-backend) | Командный MVP food-sharing платформы. Отвечал за ядро, авторизацию и API-контракты. | Go (Gin), PostgreSQL, Redis, S3/MinIO. JWT-сессии, ролевая модель, фоновое сжатие и загрузка медиа. | Чистую архитектуру (Clean Architecture), миграции, настройку CI/CD пайплайнов и покрытие интеграционными тестами. |
| [Gozon Async Shop](https://github.com/tupitsin88/Gozon-async-shop) | Pet-проект. Микросервисная e-commerce система с асинхронным взаимодействием. | Go, PostgreSQL, Kafka. Transactional Outbox/Inbox, идемпотентность обработки, WebSocket. | Реализацию паттернов гарантированной доставки сообщений при сбоях сети, Docker Compose и Swagger-документацию. |
| [MerchCRM Yandex](./merchcrm-case-study) | Приватный проект в рамках Яндекс-образования. Исходный код закрыт, опубликован только case study. | Yandex OAuth, Redis-сессии, auth middleware, Liquibase, пайплайны качества. | Описание архитектуры, флоу авторизации и логики дедупликации данных без привязки к внутренним бизнес-данным. |

## Дополнительные проекты

- [Antiplagiat](https://github.com/tupitsin88/Antiplagiat) - учебная микросервисная система проверки документов: REST, Docker, PostgreSQL, background analysis, Jaccard similarity.
- [LogsParser](https://github.com/tupitsin88/LogsParser) - Go-сервис для загрузки лог-файлов, парсинга, агрегации и выдачи данных через REST API.
- [Zoo ERP System](https://github.com/tupitsin88/Zoo-ERP-system) - консольный Go-проект для отработки SOLID, interfaces, DI и unit tests.
