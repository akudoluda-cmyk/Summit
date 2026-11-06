# Launch readiness and owner requirements

Updated 6 November 2026 for the [Step 02 business contract](launch/02_BUSINESS_AND_ARCHITECTURE_DECISIONS.md).
Local development can continue while feature-specific and production-launch gates remain open.
The official website name is **1751 Digital**. The production domain is **TBC**; none has been
purchased/registered. Use Cloudflare's actual assigned temporary **pages.dev** staging origin for
development/testing. Do not invent a hostname or hardcode a permanent domain. No actual hosted
staging URL has been verified in this audit. Publishing the Codex environment is separate from
deploying the website; Step 02 performs neither action.

## Historical local evidence — not acceptance of the new contract

The checked items below are retained from the supplied Stage 3 reports. See
[Step 01](launch/01_BASELINE.md) for independently rerun checks and their scope. They do not prove
the new guest/Selar/Community contract is implemented. No application tests were rerun for the
Step 02 documentation change.

- [x] Additive schema, administration, MFA/RBAC and transactional API implementation.
- [x] Products/order history, publishing, events, moderation, support and controlled settings simulations.
- [x] Backend security/transaction regression, public/admin browser and responsive checks.
- [x] PostgreSQL 17 concurrency tests; isolated encrypted restore and post-restore grants/relationships.
- [x] Static build and Cloudflare Pages worker compilation; secret-free configuration templates.
- [x] Actual lab performance/accessibility reports; limits explicitly recorded.
- [x] Admin manual, security review, backup/recovery and deployment/rollback runbooks.
- [x] Original ten artwork files and Stage 1 stylesheet verified byte-identical.

## Owner decisions and access — launch blockers

- [ ] At production launch: purchase/register the owner-selected domain, confirm canonical hostname,
      DNS/Cloudflare ownership and release approver. Domain remains TBC and does not block ongoing development.
- [ ] Keep domain-dependent configuration per environment: actual pages.dev staging origin now;
      production APP_ORIGIN/canonical URLs, staff Auth redirects/cookies and supported provider callbacks later.
      Verify exact allowed origins on transition; do not broaden them to arbitrary sites.
- [ ] Separate approved staging/production Supabase projects and server keys; real hosted preview.
- [x] Owner supplied enquiry and administrator email: **1751edits@gmail.com**.
- [ ] Verify the designated administrator email, assign approved staff roles and enroll MFA;
      establish recovery responsibility. The recorded email alone grants no access.
- [ ] Verified Selar catalogue/product checkout links, seller responsibility, supported delivery,
      receipt/refund workflow and display-price freshness. Selar is the authority for Store payments,
      sale records and delivery; no parallel native Store payment or fulfillment platform.
- [ ] Preserve cart UI; use individual Selar checkout links unless the exact multi-product handoff is
      proven supported. Do not treat the earlier blocked research as proof of unsupported functionality.
- [ ] Admins can choose free or paid Summit registration; paid provider is Selar. Keep paid registration
      disabled/unpublished until authenticated payment verification, idempotent settlement and seat
      reconciliation (including expired holds, failed/late/duplicate payments) are approved and tested.
- [ ] Configure enquiry recipient `TEAM_INBOX` as **1751edits@gmail.com** and verify enquiry delivery.
- [ ] Verify the outbound SMTP/Resend sender separately; confirm operational-alert routing (`OPS_INBOX`)
      and independent alert destination. The enquiry/admin address is not proof of sender verification.
- [ ] Approved real catalogue, prices/currencies matching verified Selar data, licensed demos/delivery assets,
      event dates/speakers and stories. Do not infer current prices or currencies from old fixtures.
- [ ] Community guest registration uses private Supabase records and the existing MFA-protected admin dashboard:
      name/email required, phone required for WhatsApp, affirmative contact/invitation consent.
      Select the external platform/destination later; keep invitations unpublished until selected/approved.
- [ ] Community Pending/Invited/Joined states reflect actual actions, with Joined only when confirmed;
      manual admin-approved invitations are the baseline. Any automation needs supported platform evidence.
- [ ] Guest Summit fields, duplicate/transfer rules, waitlisting, check-in and cancellation/verification
      operations are approved; Summit information is not reused for Community registration without consent.
- [ ] Owner-supplied and explicitly approved privacy, terms, cookies, refunds, digital delivery,
      community guidelines and event terms. These remain blockers at the user's direction.
- [ ] Owner-approved financial/PII retention, deletion review/purge procedure, purchase-access policy,
      backup retention/lifecycle, recovery point/time objectives and responsible operator.
- [ ] If retained private document-upload features are enabled, verify their scanner/quarantine controls.
      Do not require native Store delivery as a substitute for the approved Selar delivery flow.
- [ ] Independent private remote backup bucket/access, key custody and verified hosted staging restore.
- [ ] Required exact service/network hostnames and encrypted secure value entry in environment settings.
- [ ] Reviewed/pushed source release, branch protections, CI evidence and release artifact checksum.

## Hosted acceptance before production approval

- [ ] Home, Summit, Store, Community and About work on phones/tablets/desktops without customer
      accounts, signup, login, passwords, profiles or on-site memberships; preserve the approved vanilla design.
- [ ] Staff-only identity: MFA enrollment/recovery, protected cookies, role permissions and session
      revocation work after customer journeys are removed. No public staff signup is implied.
- [ ] Permission/RLS denial and private registration boundaries; revoked/archived/unpublished content is protected.
- [ ] Selar Store handoff and supported delivery/receipt/refund behavior verified with approved test arrangements;
      client redirects cannot manufacture payment, sales records, native entitlements or delivery.
- [ ] Store reporting distinguishes verified Selar records from historical native records and catalogue clicks.
- [ ] Paid Summit failure/retry/late/duplicate settlement and seat reconciliation pass before paid activation;
      no redirect, screenshot or client claim alone confirms a paid seat.
- [ ] Event concurrency, free/paid capacity, waitlists, schedule-change/cancellation mail and attendance.
- [ ] Community registration has separate consent, conditional phone validation and truthful save feedback;
      staff review/status permissions work. Actual community interaction occurs externally. Invitations remain
      unpublished while the platform is deferred; a click or submission never proves external membership.
- [ ] Staff content previews/revisions/publication and settings; no exposed deployment secrets.
- [ ] Inquiry delivery and newsletter confirmation/unsubscribe/suppression; real job/outbox recovery.
- [ ] External uptime/job failure alerts; complete database/Storage/secret recovery and measured RPO/RTO.
- [ ] TLS certificate, HTTP-to-HTTPS and canonical-host redirects, complete HSTS policy and security headers.
- [ ] Human keyboard/screen-reader/accessibility acceptance and deployed performance targets agreed.
- [ ] Staging rollback drill, approved Selar payment reconciliation and preservation of historical/audit data.
- [ ] Explicit approval to deploy publicly. Enable indexing only on the accepted production origin.

No credentials should be pasted into chat or included in a downloadable archive. Save them through
secure deployment/environment settings. Saved environment setup instructions do not apply runtime
values or publish a snapshot/site by themselves.
