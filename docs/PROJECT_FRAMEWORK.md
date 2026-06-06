# Project Framework

This document records the high-level structure of this repository after the fork customization.

## Overview

Sub2API is a full-stack AI API gateway. The backend is a Go service that handles setup, authentication, billing, routing, account scheduling, upstream protocol compatibility, and persistence. The frontend is a Vue 3 single-page application for public pages, user workflows, and admin operations. Production deployment is handled by Docker Compose on the server and GitHub Actions in this fork.

## Top-Level Layout

| Path | Purpose |
| --- | --- |
| `.github/workflows/` | CI, release, security scan, CLA, and fork-specific production deployment workflows. |
| `backend/` | Go backend service, Ent schema/generated code, migrations, embedded web assets, services, repositories, handlers, and shared packages. |
| `frontend/` | Vue 3 + Vite frontend application, including routes, views, components, stores, composables, i18n, and public static assets. |
| `deploy/` | Dockerfiles, Compose files, service files, environment templates, and deployment scripts. |
| `docs/` | Long-form project documentation and local architecture notes. |
| `tools/` | Maintenance scripts used by CI or local checks. |

## Backend Layers

| Layer | Main Paths | Responsibility |
| --- | --- | --- |
| Entry | `backend/cmd/server/` | Parses CLI flags, runs setup mode, loads config, initializes dependencies, and starts the HTTP server. |
| Routing | `backend/internal/server/`, `backend/internal/handler/` | Registers API routes and maps HTTP requests to handler methods. |
| Services | `backend/internal/service/` | Holds business logic for auth, billing, gateway routing, scheduling, payments, notifications, quotas, and operational dashboards. |
| Repositories | `backend/internal/repository/` | Encapsulates database, Redis, cache, migration, backup, and persistence access. |
| Domain and DTOs | `backend/internal/domain/`, `backend/internal/handler/dto/` | Shared domain constants, transport DTOs, and API-facing shapes. |
| Packages | `backend/internal/pkg/` | Protocol adapters, OAuth helpers, OpenAI/Claude/Gemini compatibility code, logging, pagination, proxy parsing, and utilities. |
| Persistence | `backend/ent/`, `backend/migrations/` | Ent-generated database access and SQL migrations. |
| Web Embedding | `backend/internal/web/` | Serves the built frontend when embedded into the backend binary/image. |

## Frontend Layers

| Layer | Main Paths | Responsibility |
| --- | --- | --- |
| App Shell | `frontend/src/main.ts`, `frontend/src/App.vue` | Creates the Vue app and installs router, stores, and global setup. |
| Routing | `frontend/src/router/` | Defines public, user, admin, setup, and auth routes. The public instruction page is `/instruction`. |
| Views | `frontend/src/views/` | Page-level screens for public docs, auth, user dashboard, admin tools, setup, payments, and usage. |
| Components | `frontend/src/components/` | Reusable UI for layout, account management, admin forms, charts, payments, keys, and icons. |
| API Client | `frontend/src/api/` | Axios-based API access and typed request helpers. |
| State and Utilities | `frontend/src/stores/`, `frontend/src/composables/`, `frontend/src/utils/` | Shared UI state, reusable workflows, formatting, clipboard, onboarding, refresh, and validation helpers. |
| Localization | `frontend/src/i18n/` | English and Chinese interface copy. |
| Public Assets | `frontend/public/` | Static files served at the site root, including logos and instruction guide images. |

## Public Instruction Page

The public user manual at `/instruction` is implemented by:

| Item | Path |
| --- | --- |
| Route | `frontend/src/router/index.ts` |
| Page component | `frontend/src/views/public/InstructionView.vue` |
| Guide images | `frontend/public/img/codex-guide/` |

The QQ group contact image is stored at `frontend/public/img/codex-guide/qq-group.jpg` and referenced directly from the instruction page.

## Configuration and Setup Flow

The backend starts in one of two modes:

| Mode | Trigger | Behavior |
| --- | --- | --- |
| Setup mode | First run without completed setup | Starts the setup wizard and serves setup routes. |
| Auto setup | Docker deployment with `AUTO_SETUP=true` | Reads environment variables and prepares initial runtime configuration automatically. |
| Normal server | Setup already complete | Loads config, initializes dependencies, starts scheduled work and API routes. |

Important deployment configuration lives in:

| Path | Purpose |
| --- | --- |
| `deploy/.env.example` | Environment variable template for Docker Compose. |
| `deploy/docker-compose.yml` | Main Compose deployment with app, PostgreSQL, and Redis. |
| `deploy/docker-compose.local.yml` | Local-directory data layout for easier migration. |
| `deploy/config.example.yaml` | Full backend config example. |

## Runtime Data Flow

1. A client calls the frontend or API endpoint.
2. The router and middleware validate route, auth, request body, and security headers.
3. Handlers translate HTTP requests into service calls.
4. Services apply business rules, quota checks, account selection, billing, provider compatibility, and upstream forwarding.
5. Repositories persist state in PostgreSQL and cache fast-changing data in Redis.
6. Gateway services normalize upstream responses and record usage/operational metrics.

## Deployment Flow

This fork deploys through `.github/workflows/deploy.yml`:

1. Push to `main` triggers the Deploy workflow.
2. GitHub Actions builds a Docker image and pushes it to GHCR.
3. The deploy job connects to the server by SSH.
4. The server writes `docker-compose.deploy.override.yml` with the newly built image.
5. Docker Compose pulls the image and runs `sub2api`, PostgreSQL, and Redis.

Current server-side deployment directory:

```text
/opt/sub2api
```

## Fork Customization Notes

This fork currently keeps local changes on top of upstream:

| Area | Purpose |
| --- | --- |
| Production workflow | Build and deploy the fork image from GitHub Actions to the configured VPS. |
| Public instruction page | Replace user-support contact details with the current QQ group image and group number. |
| Root README files | Cleared intentionally for a private/minimal fork presentation. |
| Local docs | Architecture notes live in this `docs/` directory. |
