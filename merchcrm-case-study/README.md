# MerchCRM: backend/infra кейс

MerchCRM - приватный внутренний CRM-проект для учета корпоративного мерча, остатков, выдач и офисной принадлежности данных. Исходный репозиторий закрыт, поэтому здесь описаны только архитектура, зона моей ответственности и инженерные решения без исходного кода, секретов, внутренних URL и бизнес-данных.

## Контекст проекта

В исходном процессе данные по мерчу хранились в разрозненных Excel/CSV-файлах. Это усложняло контроль получателей, остатков, офисов, дублей и записей, требующих ручной проверки.

MVP был спроектирован как модульный монолит: backend на Go, PostgreSQL для доменных данных, Redis для сессий, Liquibase для миграций, Docker Compose для локального и серверного запуска, frontend-клиент поверх backend API.

## Моя зона ответственности

Я отвечал за аутентификацию на backend, управление сессиями, инфраструктуру запуска и CI-проверки.

- Реализовал вход через Yandex OAuth: генерация state, state-cookie, callback-проверка, обмен auth code на access token, получение профиля пользователя и создание/обновление пользователя в PostgreSQL.
- Вынес пользовательские сессии в Redis: session token, TTL, получение текущего пользователя по сессии и удаление сессии при logout.
- Настроил auth middleware с явными правилами доступа для public, authenticated, superadmin и office-scoped маршрутов.
- Собрал Docker Compose pipeline для PostgreSQL, Redis, Liquibase, backend и frontend.
- Добавил healthchecks и зависимости сервисов, чтобы backend стартовал только после готовности PostgreSQL, Redis и успешного применения миграций.
- Настроил Sourcecraft CI: форматирование, тесты, static analysis, backend build, Liquibase validation и Docker Compose config validation.

## Архитектура

```text
client
  -> frontend
  -> backend API
       -> auth middleware
       -> handlers/services
       -> PostgreSQL
       -> Redis session store

Liquibase applies DB migrations before backend startup.
Docker Compose coordinates service readiness.
```

## Поток авторизации

```text
1. Пользователь начинает вход через Yandex OAuth.
2. Backend генерирует state и записывает его в state-cookie.
3. Yandex возвращает пользователя на backend callback.
4. Backend сравнивает state из query params со state-cookie.
5. Backend обменивает auth code на Yandex access token.
6. Backend получает профиль пользователя из Yandex.
7. Backend создает или обновляет локального пользователя в PostgreSQL.
8. Backend создает Redis-сессию с TTL.
9. Backend возвращает session cookie клиенту.
10. Auth middleware получает текущего пользователя через Redis на защищенных маршрутах.
```

## Инфраструктурный запуск

Docker Compose поднимает весь runtime-пайплайн:

- PostgreSQL хранит пользователей и доменные данные.
- Redis хранит application sessions.
- Liquibase валидирует и применяет миграции БД.
- Backend отдает API и health endpoint.
- Frontend зависит от healthy backend.

Backend service стартует только после:

```text
postgres: service_healthy
redis: service_healthy
liquibase: service_completed_successfully
```

Это убирает нестабильный старт приложения, когда API поднимается раньше базы, Redis или миграций.

## Проверки CI

CI workflow запускается на pull request в `main` и проверяет backend-код вместе с инфраструктурной конфигурацией.

Backend-проверки:

- `gofmt`
- `go test ./...`
- `go vet ./...`
- `go build ./cmd/app`

Инфраструктурные проверки:

- Liquibase changelog validation
- Docker Compose config validation using `.env.example`

## Технологии

- Go
- PostgreSQL
- Redis
- Liquibase
- Docker Compose
- Yandex OAuth
- Sourcecraft CI

## Что намеренно не раскрыто

- ссылки на приватный репозиторий
- production/internal URL
- исходный код приватного проекта
- секреты, токены, env-значения и OAuth credentials
- бизнес-данные и реальные пользовательские данные
- детали реализации, за которые отвечали другие участники

## Кратко для резюме

Реализовал backend authentication и infrastructure foundation для внутренней merch CRM: Yandex OAuth, Redis-backed sessions, route-level auth middleware, Docker Compose orchestration для PostgreSQL/Redis/Liquibase/backend/frontend и CI quality gates для backend/platform checks.
