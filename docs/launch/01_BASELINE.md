# 1751 Digital — Step 01 baseline audit

Date: 4 November 2026, Africa/Lagos. Scope: the user explicitly authorized the attached `1751-step-01.txt` after clarification. This is a source/provenance audit and local preservation step. No application logic, tests, dependency declarations, lockfiles, migrations or visual assets were changed. No deployment, database operation, real transaction, external message, push or PR was performed.

## Verdict

**PASS — Step 01 baseline gate. READY to receive and review Step 02.** The correct full source is identified, inventory and discrepancies are documented, and an untouched rollback point exists. Step 02 instructions have not been supplied; no later implementation is authorized by this verdict. **Launch and business-contract alignment remain BLOCKED** by the account/membership and Paystack/Selar conflicts and owner decisions in [the issues register](01_ISSUES.md).

## Exact source identity

| Item | Verified value |
| --- | --- |
| Configured repository | `akudoluda-cmyk/Summit` on `github.com` |
| Sanitized origin | `https://github.com/akudoluda-cmyk/Summit.git` |
| App root | `/workspace/Summit` (capital S) |
| Entry Git state | Unborn local branch `work`; no commit SHA existed |
| Remote state | Fresh `git ls-remote origin` succeeded with no advertised refs; requested `main` does not yet have a remote baseline |
| Source baseline commit | `47082a340ac207f7476bfeb485fc5ca5571b76ee` |
| Source tag | `baseline/1751-step01` (annotated; resolves to the baseline commit) |
| Audit/development branch | `dev/1751-step01`, created from the source baseline |
| Source package | User-uploaded `summit-cloudflare-sandbox-package (1).zip`; outer root `summit-cloudflare-sandbox-package/` |
| Confirmed full-source inner package | `1751_WRANGLER_FULL_SOURCE_DO_NOT_UPLOAD_TO_DASHBOARD.zip`; root **`1751-cloudflare-pages/`** |
| Runtime | Node 24.19.0; lockfile-pinned dependencies; system Chromium; Wrangler 4.150.0 |

The full-source inner ZIP has 152 files. All **114 shared files** are byte-identical to the working source. Its other 38 files are 36 prebuilt dist files and two historical evidence logs. The outer upload has 126 files: its 12 extra files are three named ZIPs and checksums, the sandbox setup guide, and five UI-review outputs. All 126 source files remain byte-identical to the user upload. Exact hashes and path differences are in [01_SOURCE_COMPARISON.json](01_SOURCE_COMPARISON.json); the complete per-file size/hash inventory is [01_INVENTORY.md](01_INVENTORY.md).

This is the full application, demonstrated by `functions/`, `backend/`, `admin/`, `supabase/`, `jobs/`, tests, manifests and server configuration. `1751_DASHBOARD_UPLOAD_STATIC_ONLY.zip` and generated `static-preview/` are separate labelled demonstrations with disabled data-backed actions. They were not selected as the application baseline.

## Comparison with the historical audits

`docs/STAGE3_AUDIT.md` describes the older Stage 2 gaps and planned Stage 3 work. Current `backend/admin.js`, `backend/uploads.js`, `backend/render.js` and the second migration implement the later MFA/RBAC, CMS, upload quarantine, history and rendering work. Its launch-gate caveats still apply. `docs/CLOUDFLARE_AUDIT.md` (14 October) selected Pages source Functions; `wrangler.toml`, `functions/` and the current build match that selection.

`docs/UI_RECONSTRUCTION.md`, `docs/CLOUDFLARE_PACKAGE_SEPARATION.md` and the README reflect the 17 October UI and package separation. Current `reference.css`/`reference.js` layer that presentation onto the original vanilla platform. No newer application delta exists between the two supplied source packages or between the upload and this baseline; there is no Git history from which to infer earlier authorship or chronology. Historical links to `davidakudolu-dev/summit` do not establish a relationship with the configured `akudoluda-cmyk/Summit` remote.

The older `docs/SANDBOX_SETUP.md` and `scripts/package-sandbox.py` remain alongside the newer Pages flow; they are not authoritative deployment instructions. `docs/API.md` also overstates some admin route names (issue 07). Historical QA results, advisory audits, Lighthouse figures and hosted-access statements are prior evidence, not fresh measurements. The new customer-free/Selar business contract is a material change from the account/Paystack architecture described in those audits.

## Component status and preservation decisions

“Implemented” means source exists and local evidence supports the stated behavior, not production acceptance. Multiple statuses can apply to one component.

| Area | Current source/evidence | Status | Preserve / limitation |
| --- | --- | --- | --- |
| Five public sections | `index.html:56,298,454,494,545`; `reference.css`; `reference.js`; `stage1.*`; `assets/` | Implemented; safe to preserve | Home, Summit, Store, Community, About; vanilla HTML/CSS/JS. No framework change or redesign. |
| Additional views | `index.html:594,603,608`; `stage2.js`; `backend/render.js:9` | Implemented; account view conflicting | Account, story, discussion; detail routes for products/events/posts and legal/SEO. Keep five-section design; later work must reconcile account-related entry points. |
| Public/API routing | `functions/[[path]].js`; `functions/api/[[path]].js`; `backend/api.js` | Implemented; locally tested | SSR and asset fallback plus a central API dispatcher; complete route groups below. |
| Admin identity | `admin/`; `backend/admin.js:65`; second migration | Implemented; safe to preserve; hosted unverified | Verified Supabase identity, TOTP/AAL2, role permissions, recent-MFA sensitive operations, protected cookies, session revocation and audit. Public identity shares this infrastructure; do not remove it wholesale. |
| Database | `supabase/migrations/202610130001_platform.sql`; `202610130002_admin.sql` | Implemented; local disposable DB tested; hosted unverified | Platform schema then additive admin schema; restricted client grants/RLS, service RPCs, transactional capacity/history. Existing historical data must be preserved by future additive migrations. |
| Store/cart | `stage2.js:154`; `backend/api.js:339`; platform migration | Implemented; conflicting; Selar incomplete | Existing cart and guest ordering are real application code. Internal Paystack test checkout and Supabase downloads conflict with the Selar contract. No supported Selar combined checkout has been established. |
| Summit | `backend/api.js:377`; platform migration register/payment actions | Implemented; conflicting; policy unverified | Account-required registration; free confirmation, paid pending state, capacity/waitlist/cancellation rules. Paid settlement uses authoritative verification, not redirect confirmation. Owner free/paid policy missing. |
| Community | `stage2.js`; `backend/api.js:394`; platform migration | Implemented; conflicting | Public view plus membership/identity-based posting, comments, reports and moderation. Account-free scope requires owner direction. |
| Forms/email/jobs | `backend/api.js` inquiries/newsletter/jobs; `jobs/worker.js`; `jobs/wrangler.toml` | Implemented; hosted unverified | Consent, newsletter capabilities, outbox/Resend, job bearer secret and five-minute scheduled Worker. No external mail sent; fixtures simulate providers. |
| Uploads/delivery | `backend/uploads.js`; `supabase/storage*.sql` | Implemented; safe controls to preserve; delivery conflict | Bounded uploads, MIME/signature checks, randomized keys, hash-verified scanner and quarantine; public site-media/private digital-products. Scanner absent; product delivery ownership must move to the approved Selar design later. |
| Operations/recovery | `scripts/backup*.mjs`; `scripts/restore.mjs`; `.github/workflows/backups.yml` | Implemented; incomplete operational verification | Encrypted backup and guarded isolated restore tooling exist. No remote backup/hosted restore was exercised in Step 01. |
| Cloudflare deployment | `wrangler.toml`; `scripts/build.mjs`; `scripts/wrangler.mjs` | Implemented; local build verified; hosted unverified | Pages source Functions; dist has assets and `_routes.json`, no `_worker.js`. Scheduled jobs are a separate Worker. No deployment was performed. |
| Mocked/demo behavior | `tests/helpers.mjs`; `tests/cloudflare-runtime.mjs`; `demo/reference-fixtures.js`; `scripts/build-static.mjs` | Mocked explicitly in tests/demo | Test doubles stand in for Auth, payments, email and Storage; fixtures are not approved inventory. Production handlers do not become operational merely because fixture tests pass. |
| Policy/content | `docs/LAUNCH_CHECKLIST.md`; legal/settings schema | Incomplete/unverified | Owner content, Summit policy, legal/retention, initial admin and staging acceptance remain outstanding. |

## API inventory from current dispatchers

Paths below have `/api/` prefix. Parameter validation, rate limits, CSRF, authentication and database permission checks still apply; this is an inventory, not a promise that unconfigured endpoints work. Read directly from `backend/api.js:221–406`, `backend/admin.js:65–147` and `backend/uploads.js`.

- GET health; GET home, settings, policy, products, product, categories, summits, events, event, articles, article, search, communities, posts, post. GET dashboard/cart require a verified user; GET reports is routed through admin permissions.
- POST auth/signup, auth/login, auth/recover, auth/verify, auth/logout, auth/password; GET auth/session. Customer-facing routes conflict with the new contract.
- POST inquiries; newsletter/subscribe, newsletter/confirm, newsletter/unsubscribe.
- POST checkout, orders, payments/verify, payments/retry, downloads. POST payments/webhook verifies the raw-body signature and independently checks payment/refund data. Live Paystack keys are rejected by the current sandbox guard.
- POST registrations, registrations/cancel, registrations/check-in; profile, account/delete-request, cart, memberships; posts/create/update/delete; comments/create/update/delete; reports, moderation. Mutations are user- or staff-protected as implemented.
- POST jobs/email, jobs/reconcile, jobs/monitor, jobs/report are protected by JOB_SECRET.
- Admin bootstrap/context and MFA: admin/context; admin/mfa/factors; POST admin/mfa/enroll, admin/mfa/challenge, admin/mfa/verify. Context/factor discovery has a narrower pre-MFA staff role; business administration requires MFA.
- GET admin/overview, analytics, list, detail, revisions, orders, order_detail, registrations, reports, posts, memberships, users, user_detail, deletions, subscribers, settings, policies, health, audit, incidents, media, export.
- POST admin/save, archive, setting_save, settings_batch, roles, user_control, deletion_review, delete_account, session_cancel, session_speakers, registration_action, moderate, post_moderate, restriction, unsubscribe, order_resolve, order_reconcile, refund_prepare, incident_resolve, outbox_retry, upload, scan.

Public clean routes include `/`, `/store`, `/summit`, `/community`, `/about`, `/account`, `/stories`, `/stories/:slug`, `/products/:id`, `/events/:id`, `/community/discussion/:id`, `/community/posts/:id`, legal policy routes, robots and sitemap. The private admin shell is `/admin`; data access still requires staff identity/MFA. Browser hashes also support legacy navigation and account/payment capabilities.

## Tests and observed results

All commands use `/workspace/Summit` and `export PATH=/workspace/.summit-tools/node-v24.19.0-linux-x64/bin:$PATH`; browser checks use `CHROMIUM_PATH=/usr/bin/chromium`.

| Command/check | Outcome and evidence boundary |
| --- | --- |
| `git ls-remote origin` | Fresh success, no refs; proves scoped Git read access only. |
| ZIP member/hash comparison | Fresh success: all 126 current files equal upload; all 114 common outer/inner files equal. |
| `npm run check` | Fresh exit 0: syntax checks, Node runner reports 3 passing test files, no failures/skips, and static build. See `evidence/step01-check.txt`. Source has 44 test declarations; do not substitute historical counts for this runner's output. |
| `node --test --test-reporter=tap tests/admin-integrity.test.mjs` | Diagnostic exit 0, one passing file entry; default runner does not expose individual case results here. |
| `npm run build:functions` | Fresh exit 0, Wrangler compiled Worker successfully. |
| `npm run validate:deployment` | Fresh exit 0: 36 full static files, 39 separate preview files; routing and source separation checked. |
| `npm run test:browser` | Earlier in this same session on byte-identical source: final unmodified sequential run exit 0, 13/13 checks. First concurrent run failed mobile overflow; diagnostic and sequential reruns passed. Copied `evidence/browser.json` belongs to that final run, not a newly claimed Step 01 browser execution. |
| `npm run test:admin` | Earlier in this session on identical source: exit 0, 8/8 including automated serious/critical accessibility checks; copied `evidence/admin-browser.json`. |
| Development HTTP smoke | Earlier in this session: public/store/summit/admin/favicon 200; health configured:false/payment_mode:sandbox; `.dev.vars` and backend source paths 404. |
| Docker concurrency/recovery, Lighthouse, reference-visual/static browser suites, hosted provider acceptance, advisory audit | Not run in Step 01. Historical reports are not fresh proof; no deployment or real transaction validation is claimed. |

Fresh `npm run test:cloudflare` exited 0: actual local workerd exercised API dispatch, SSR/store, authentication/dashboard, sandbox payment verification, registration, admin MFA permissions, assets and private-file denial. Provider services were explicit test doubles.

To expose individual backend case outcomes, these exact additional commands were run separately (each exit 0):

```sh
node --test --test-isolation=none --test-reporter=tap tests/platform.test.mjs
node --test --test-isolation=none --test-reporter=tap tests/admin.test.mjs
node --test --test-isolation=none --test-reporter=tap tests/admin-integrity.test.mjs
```

They reported **26 + 16 + 2 = 44 passed**, with zero failures, skips, cancellations or todos. Complete outputs are `evidence/step01-platform-inprocess.txt`, `evidence/step01-admin-inprocess.txt`, and `evidence/step01-integrity-inprocess.txt`. No test source or assertion was changed. This resolves case-count uncertainty without treating the subprocess runner's three file entries as three individual assertions. Provider doubles remain distinct from real services. Passing existing tests validates current behavior, including behavior that conflicts with the new contract; it does not certify that contract.

## Preservation, rollback and review

Untouched backup directory: `/workspace/summit-backups/step01-prebaseline/`. `original-source.zip` is a verified byte-for-byte copy of the upload; `original-git.tar.gz` preserves the pre-commit Git metadata. `SHA256SUMS` records their digests. `source-baseline.bundle` contains the source commit/branches/tag and passed `git bundle verify`. These local backups survive source edits but are not an independently hosted backup.

For recovery, verify checksums and inspect the bundle before restoring. A fresh directory outside the active checkout can be cloned from `source-baseline.bundle` at branch `work` if recovery is needed; do not overwrite the current tree or use a destructive reset. Use the tag as the code comparison point. Do not execute `supabase/rollback.sql` or a restore script as a source rollback. No database/Storage state was backed up because no live database was accessed.

The source-only initial commit adds the original 126 uploaded files; the following audit commit adds only `docs/launch/`. Resolve the audit commit with `git rev-parse dev/1751-step01`; its SHA is reported in the final handoff rather than embedded self-referentially in this file. The final `step01-audit.bundle` in the same backup directory additionally preserves this audit branch and its evidence; its checksum is added to `SHA256SUMS`. No remote branch/PR exists. A future implementation branch should start from the reviewed audit commit, in this existing isolated checkout; no extra worktree is needed.

## Confirmed owner decision — Store authority

The owner confirmed that **Selar is the authoritative system for Store payments, sale records and delivery**. The Store remains a 1751 product showcase. Future implementation must treat Selar as the source of truth for these functions; the existing internal Paystack/order/entitlement flow does not satisfy this decision. This confirmation records the target responsibility and does not change application behavior or authorize deployment.

Verified Selar product destinations and supported cart/checkout capabilities remain to be established. Preserve Add to Cart presentation without inventing combined checkout support. This Store decision does not settle the separate Summit free/paid policy.

## Owner actions and handoff

1. Review this report and `01_ISSUES.md`. Supply the actual Step 02 instructions in this chat; no later-step scope has been invented.
2. Selar authority for Store payments, sale records and delivery is confirmed above. Clarify the account-free Community behavior, approve the free/paid Summit policy, and supply verified Selar product destinations/cart compatibility before those features are changed. The no-customer-account requirement is already part of the approved contract. Provide decisions in chat; never secret values.
3. Preserve an independent copy of the backup via the workspace file download controls where available. For remote sharing, explicitly authorize pushing the reviewed baseline/tag/development branch to `akudoluda-cmyk/Summit`; no GitHub click is required to finish this local audit, and no PR can be claimed before a push. Historical README download links point elsewhere.
4. Only for a later authorized staging task, enter credentials in environment settings (not chat/Git/frontend). No Cloudflare or Supabase dashboard action is required for Step 01. Production DNS, payments, database migrations and deployment remain outside scope.

Acceptance: correct full source/commit **PASS**; static-demo distinction **PASS**; full inventory and no application edits **PASS**; untouched backup/tag/bundle **PASS**; explicit handoff **READY for Step 02 review, launch BLOCKED**. Open issues are documented for planning; none authorize redesign or silent feature removal.
