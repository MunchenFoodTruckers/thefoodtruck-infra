# TheFoodTruck Infra

Local development infrastructure for TheFoodTruck microservices.

Includes:
- Traefik reverse proxy (HTTP entrypoint, dashboard)
- PostgreSQL (16-alpine)
- Redis (7-alpine)
- Service containers for web and users-service (more services can be added similarly)

Directory layout expectation (sibling repos):

- ../thefoodtruck-web
- ../thefoodtruck-users-service
- ../thefoodtruck-menu-service
- ../thefoodtruck-orders-service
- ../thefoodtruck-payments-service
- ../thefoodtruck-schedule-service
- ../thefoodtruck-offers-service
- ../thefoodtruck-diet-plan-service
- ../thefoodtruck-referrals-service
- ../thefoodtruck-notifications-service

Usage

1) Copy env files in component repos from their `.env.example` and adjust.
2) Start the stack:

   docker compose -f infra/docker-compose.yml up -d --build

3) Initialize the Users DB (run from users repo or with docker exec):

   pnpm --dir ../thefoodtruck-users-service prisma:generate
   pnpm --dir ../thefoodtruck-users-service prisma:migrate-dev
   pnpm --dir ../thefoodtruck-users-service prisma:seed

Traefik
- Dashboard: http://localhost:8080 (no auth in dev)
- Web site: http://localhost/
- Users API: http://localhost/api/users/*
