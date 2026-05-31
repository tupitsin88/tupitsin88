# MerchCRM Case Study

MerchCRM is an internal CRM project for managing corporate merch inventory and issuance workflows. The original repository is private, so this case study describes the architecture, responsibilities, and engineering decisions without exposing source code, credentials, internal URLs, or business data.

## Project Context

The project targets a common operational problem: merch data is often stored in scattered Excel and CSV files, which makes it difficult to track recipients, issued items, office ownership, duplicates, and unresolved records.

The MVP is designed as a modular monolith with a Go backend, PostgreSQL storage, Redis-backed sessions, Liquibase migrations, Docker Compose infrastructure, and a frontend client connected to the backend API.

## My Scope

My contribution focused on backend authentication, session management, infrastructure, and developer workflow.

- Implemented Yandex OAuth login flow with state cookie validation, callback handling, PostgreSQL user creation/upsert, session cookie issuing, and logout.
- Moved application sessions to Redis with TTL, lookup by session token, and deletion on logout.
- Added auth middleware with explicit route policies for public, authenticated, superadmin, and office-scoped routes.
- Built a Docker Compose startup pipeline for PostgreSQL, Redis, Liquibase, backend, and frontend.
- Added healthchecks and service dependencies so the backend starts only after PostgreSQL, Redis, and migrations are ready.
- Configured Sourcecraft CI checks for backend formatting, tests, static analysis, build validation, Liquibase validation, and Docker Compose config validation.

## Architecture Snapshot

```text
client
  -> frontend
  -> backend API
       -> auth middleware
       -> domain handlers/services
       -> PostgreSQL
       -> Redis session store

Liquibase applies DB migrations before backend startup.
Docker Compose coordinates infrastructure and application readiness.
```

## Authentication Flow

```text
1. User starts Yandex OAuth login.
2. Backend generates state and stores it in a state cookie.
3. Yandex redirects back to the backend callback.
4. Backend validates the state from query params against the cookie.
5. Backend exchanges the auth code for a Yandex access token.
6. Backend fetches Yandex user info.
7. Backend creates or updates the local PostgreSQL user.
8. Backend creates a Redis session with TTL.
9. Backend returns a session cookie to the client.
10. Auth middleware resolves the current user from Redis on protected routes.
```

## Infrastructure Flow

Docker Compose coordinates the local environment:

- PostgreSQL stores users and domain data.
- Redis stores application sessions.
- Liquibase validates and applies database migrations.
- Backend exposes the API and health endpoint.
- Frontend depends on a healthy backend.

The backend service depends on:

```text
postgres: service_healthy
redis: service_healthy
liquibase: service_completed_successfully
```

This prevents the application from starting before its required runtime dependencies and schema migrations are ready.

## CI Checks

The CI workflow runs on pull requests targeting `main` and validates both backend code and platform configuration.

Backend checks:

- `gofmt` formatting check
- `go test ./...`
- `go vet ./...`
- `go build ./cmd/app`

Platform checks:

- Liquibase changelog validation
- Docker Compose config validation using `.env.example`

## Technologies

- Go
- PostgreSQL
- Redis
- Liquibase
- Docker Compose
- Yandex OAuth
- Sourcecraft CI

## What Is Intentionally Omitted

This public case study does not include:

- private repository links
- production or internal URLs
- source code from the private project
- secrets, tokens, env values, or OAuth credentials
- business data or real user data
- implementation details owned by other contributors

## Resume Summary

Implemented the backend authentication and infrastructure foundation for an internal merch CRM: Yandex OAuth, Redis-backed sessions, route-level auth middleware, Docker Compose orchestration for PostgreSQL/Redis/Liquibase/backend/frontend, and CI checks for backend and platform quality gates.
