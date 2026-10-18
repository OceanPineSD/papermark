# Self-hosting notes (docs.tung.digital)

This fork runs Papermark on Replit at `docs.tung.digital`. It is not affiliated with Papermark.

## Changes from upstream

- `middleware.ts`: the app's own host (`NEXT_PUBLIC_APP_BASE_HOST`) and `*.replit.app` are no longer treated as customer custom domains. Upstream redirects them to papermark.com.
- `lib/resend.ts`: `EMAIL_FROM` overrides the hardcoded papermark.com sender.
- `pages/api/auth/[...nextauth].ts`: `ALLOWED_SIGNIN_EMAILS` limits who can create an account. Viewers never sign in.
- `trigger.config.ts`: `TRIGGER_PROJECT_REF` sets the Trigger.dev project.
- `.replit`: Replit Autoscale build and run commands.

No code under `ee/` or `app/(ee)` is changed or enabled. Those folders stay under their commercial license.

## Services

| Purpose | Service | Env vars |
|---|---|---|
| Database | Replit Postgres | `POSTGRES_PRISMA_URL`, `POSTGRES_PRISMA_URL_NON_POOLING` |
| File storage | Cloudflare R2 | `NEXT_PUBLIC_UPLOAD_TRANSPORT=s3`, `NEXT_PRIVATE_UPLOAD_*` |
| View analytics | Tinybird | `TINYBIRD_TOKEN`, `TINYBIRD_BASE_URL` |
| Rate limits, locks | Upstash Redis | `UPSTASH_REDIS_REST_*` |
| Background jobs | Upstash QStash, Trigger.dev | `QSTASH_*`, `TRIGGER_SECRET_KEY` |
| Email | Resend | `RESEND_API_KEY`, `EMAIL_FROM` |

See `.env.self-host.example` for the full list.
