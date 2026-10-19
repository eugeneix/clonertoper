# F33 — техническая документация
**Статус реализации:** не начато.
## План
- Docker-образы: php-fpm+nginx (Laravel), queue worker (Horizon), scheduler, reverb, next.js, gotenberg, meilisearch.
- staging: 1 VM, Docker Compose. production: VM(ы) + управляемый PostgreSQL + Redis + S3.
- Terraform в `infra/`. GitHub Actions: `ci.yml` (lint, phpstan, tests, build), `deploy-staging.yml` (на push в main), `deploy-prod.yml` (вручную/по тегу).
- Мониторинг: health-check, ошибки (Sentry-совместимый self-hosted или облачный в РФ), uptime, алерты.
## Секреты (будут в GitHub Secrets)
Список составлю перед первым деплоем.
