# ethic-engine — the fork (Step 0 hygiene record)

> **ethic** — aakaar's contract/deliberation layer (sub-brand; ships at `ethic.aakaar.build`
> pending that registration; "ettiqus" reserved as the collision-free legal name). Founding
> text + scout reports live on the aakaarsaarathi umbrella (`ethic/`). This repo is the
> FORK-AND-TUNE base per `OPEN-SOURCE-FIT-2026-09-03.md`; ethic's own additions are
> **Apache-2.0** (owner decision 2026-09-03) and live in their own packages as they land.

## Fork point (pinned — the MIT grant on this commit is irrevocable)
- Upstream: `activepieces/activepieces` @ `67a3e3b4a76f9d8558b83a3b54dfb86c58627c43`
  (v0.90.0, 2026-09; tag `fork-point` in this repo).
- Licence posture: upstream is **MIT for everything OUTSIDE** `packages/ee/` and
  `packages/server/api/src/app/ee` (those two are proprietary "Enterprise" — see upstream
  LICENSE). **Both are DELETED in this commit** — this fork ships no proprietary content.
  Relicensing/abandonment risk (n8n precedent) is mitigated by the pin + keeping ethic code
  in its own packages.

## What the deleted `ee/` covered (feature audit at deletion — 26 areas)
agent · alerts · api-keys · app-connections · app-credentials · appsumo · audit-logs ·
authentication (managed/SAML parts) · billing-usage-report · connection-keys · database (ee
migrations) · embed-subdomain · flags · global-connections · helper · managed-authn ·
oauth-apps · pieces (ee registry) · platform (multi-tenant admin) · platform-webhooks ·
projects (multi-project limits) · scim · secret-managers · signing-key · template · users.
Anything ethic needs from these areas gets re-implemented cleanly in ethic's Apache-2 packages
— never restored from ee/.

## De-EE worklist (build is NOT green yet — deliberate)
40 community-side server files import from the deleted `ee/` paths and must be stubbed or
de-EE'd (the fit report's Step-0 budget, 3–5 builder-days). The list, frozen at deletion:

```
packages/server/api/src/app/ai/ai-provider-service.ts
packages/server/api/src/app/analytics/platform-analytics.module.ts
packages/server/api/src/app/app-connection/app-connection-service/app-connection-service.ts
packages/server/api/src/app/app-connection/app-connection-service/oauth2/oauth2-util.ts
packages/server/api/src/app/app-connection/app-connection-service/oauth2/services/credentials-oauth2-service.ts
packages/server/api/src/app/app-connection/app-connection-worker-controller.ts
packages/server/api/src/app/app.ts
packages/server/api/src/app/authentication/otp/otp-service.ts
packages/server/api/src/app/core/canary/canary-routing.middleware.ts
packages/server/api/src/app/core/security/v2/authn/authenticate.ts
packages/server/api/src/app/core/security/v2/authz/authorize.ts
packages/server/api/src/app/core/websockets.service.ts
packages/server/api/src/app/database/database-connection.ts
packages/server/api/src/app/database/postgres-connection.ts
packages/server/api/src/app/database/seeds/role-seed.ts
packages/server/api/src/app/file/file.module.ts
packages/server/api/src/app/flags/flag.service.ts
packages/server/api/src/app/flows/flow-run/flow-run-ai-usage-tracker.ts
packages/server/api/src/app/flows/flow-run/flow-run-hooks.ts
packages/server/api/src/app/flows/flow-version/piece-upgrade.service.ts
packages/server/api/src/app/flows/flow/flow.controller.ts
packages/server/api/src/app/flows/pre-warm-workers.ts
packages/server/api/src/app/helper/embed-security.ts
packages/server/api/src/app/mcp/mcp-permissions.ts
packages/server/api/src/app/mcp/oauth/mcp-oauth.controller.ts
packages/server/api/src/app/pieces/metadata/piece-metadata-controller.ts
packages/server/api/src/app/pieces/metadata/piece-metadata-service.ts
packages/server/api/src/app/platform/platform.controller.ts
packages/server/api/src/app/platform/platform.service.ts
packages/server/api/src/app/tables/table/table.controller.ts
packages/server/api/src/app/tables/table/table.service.ts
packages/server/api/src/app/template/template.controller.ts
packages/server/api/src/app/template/template.service.ts
packages/server/api/src/app/user-invitations/user-invitation.module.ts
packages/server/api/src/app/user-invitations/user-invitation.service.ts
packages/server/api/src/app/user/user-service.ts
packages/server/api/src/app/workers/job-queue/interceptors/rate-limiter-interceptor.ts
packages/server/api/src/app/workers/job-queue/job-queue.ts
packages/server/api/src/app/workers/machine/machine-service.ts
packages/server/api/src/app/workers/rpc/worker-rpc-service.ts
```

## Step 0 remaining (after this PR)
de-EE the 40 imports → CI green → bind auth to aakaar identity (OAuth-only posture per the
counsel-workspace precedent) → gate every trigger endpoint (CW-4 discipline: authed + metered,
no open endpoints) → deploy on the approved Docker host. Then P1 (Accord/Concerto contract
object) · P2 (threshold votes → session seeding) · P3 (effort/rights ledger) per the fit
report's tuning plan. The Security Auditor gates this surface like any collaborator-facing one.
