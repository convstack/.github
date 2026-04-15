<img width="1400" height="400" alt="1400x400" src="https://github.com/user-attachments/assets/bdd25a18-c192-48a9-add1-8ada7b8edc69" />

> **Warning**
> This project is under active development and not yet ready for production use.

# Convention Apps

A modular, self-discovering application platform for managing conventions, events, and communities. Built as a collection of independent services that automatically integrate through a shared identity provider and dynamic dashboard.

## The Vision

Convention Apps follows the OpenStack model: a central identity provider (Lanyard) manages authentication and maintains a service catalog, while a dynamic dashboard renders all UI from JSON manifests provided by registered services. New services plug in automatically — no dashboard code changes needed.

```
                    ┌─────────────────────┐
                    │     Dashboard       │
                    │  (Dynamic UI Shell) │
                    └─────────┬───────────┘
                              │ OIDC + API Proxy
                    ┌─────────┴───────────┐
                    │      Lanyard        │
                    │ (Identity + Catalog)│
                    └─────────┬───────────┘
                              │ Service Discovery
              ┌───────────────┼───────────────┐
              │               │               │
         ┌────┴────┐     ┌────┴────┐     ┌────┴────┐
         │Service A│     │Service B│     │Service C│
         │(Backend)│     │(Backend)│     │(Backend)│
         └─────────┘     └─────────┘     └─────────┘
```

## Services

### Lanyard (Identity Provider)

The backbone of the platform. Handles user authentication (email, social, 2FA, passkeys), OIDC provider functionality, and the service catalog where backend services register themselves with UI manifests.

### Dashboard (UI Shell)

A stateless, auto-discovering frontend that authenticates via Lanyard and dynamically renders all UI from service manifests. Supports data tables, forms, detail views, file uploads, action bars, and specialized sections for 2FA and passkey management.

### Future Services

The platform is designed so that any backend service can register with Lanyard and instantly appear in the Dashboard. Planned services for convention management include ticketing, scheduling, vendor management, attendee check-in, and more.

## Tech Stack

- **Runtime:** Bun
- **Framework:** TanStack React Start (Vite + React 19)
- **Database:** PostgreSQL via Drizzle ORM
- **Auth:** Better Auth with OIDC provider
- **Storage:** S3-compatible (MinIO for local dev)
- **Styling:** Tailwind CSS v4
- **Linting:** Biome
- **Infrastructure:** Docker Compose, Kubernetes

## Repository Structure Example

```
convention-apps/
├── lanyard/          # Identity provider + service catalog
├── dashboard/        # Auto-discovering UI shell
├── guidebook/        # Markdown based Wiki
```

Each service is its own standalone project with its own Dockerfile, dependencies, and configuration.

## Getting Started

See the individual service READMEs for setup instructions. You can find them here:

- [convstack](../../../../convstack)

---

Made and maintained with 🧡 by [Headpat](https://headpat.space)
