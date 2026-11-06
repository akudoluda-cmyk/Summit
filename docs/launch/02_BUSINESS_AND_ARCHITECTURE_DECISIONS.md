# ADR 02 — Business and architecture decisions

Decisions recorded 4 November 2026; documentation completed 6 November 2026, Africa/Lagos. Repository: `akudoluda-cmyk/Summit`; app root `/workspace/Summit`. Starting commit: `b241141011ba4833e65e5836e9f33696fce5653b`; branch `dev/1751-step02`. Original source tag: `baseline/1751-step01`.

## Scope, authority and verdict

This is Step 02, **planning only**. The user's explicit decisions and follow-up answers are authoritative. The attached `1751-step-02.txt` supplies the requested decision-record structure; it does not authorize later implementation or deployment. Those decisions resolve the attachment's previously open Community and free/paid Summit choices. “No membership” means no on-site customer identity, member account or hosted discussion system; it does not prohibit the explicitly requested external-community registration records and statuses.

**Step 02 contract record: PASS. READY for scoped Step 03 review and ongoing development; feature activation/production launch remains BLOCKED where specified below.** The five public sections, Selar-only Store responsibilities, cart fallback, external Community registration mode, admin-selected free/paid Summit modes and Selar as paid-Summit provider are settled. The owner explicitly deferred the production domain and Community platform. Neither deferral blocks unrelated development. Multi-product Selar capability, paid-Summit verification/seat reconciliation and operating policies remain unconfirmed; their feature-specific gates are labelled BLOCKED rather than invented.

This document specifies target behavior. No application routes were disabled, no forms were implemented, no data/schema was changed and no integrations were activated by this documentation commit. The existing application still has the Step 01 conflicts. A planned feature gate is not a claim about current runtime enforcement.

## 1. Confirmed owner decisions

| Decision | Binding contract | Remaining boundary |
| --- | --- | --- |
| Public visitors | Home, Summit, Store, Community and About are browsable without accounts, signup, login, passwords, profiles or on-site membership. | Remove conflicting customer routes in a later authorized implementation while protecting staff identity and historical records. |
| Staff identity | Only authorized staff authenticate to private `/admin`, protected by MFA and server-side permissions. | Initial staff assignments and hosted identity acceptance remain operational prerequisites. |
| Name/domain | **1751 Digital** is the official website name. No production domain has been purchased/registered; production domain is **TBC**. Development/testing will use Cloudflare's temporary `pages.dev` staging origin. | Domain purchase/final configuration is a production-launch task, not a development blocker. Use the actual assigned staging hostname when available; no invented permanent or temporary hostname. Keep APP_ORIGIN, canonical URLs, cookie/auth redirects and provider callbacks configurable per environment. |
| Store | 1751 showcases products and working public demos; **Selar is authoritative for Store payments, sale records and delivery**. | No parallel native Store checkout, financial ledger as authority, entitlement or delivery system. |
| Cart | Preserve existing Add to Cart presentation and selection behavior. Investigate supported Selar multi-product checkout; use individual checkout links when support is unavailable or cannot be verified. | No invented combined checkout, line-item URL parameters or native payment fallback. |
| Summit | Authorized admins choose free or paid registration for each offering; **Selar is the selected paid-Summit provider**. | Paid flows remain disabled/unpublished in the target plan until Selar payment verification and seat reconciliation are approved and tested. Provider and modes are resolved; the financial workflow is not. |
| Community | The actual community is external. The website collects guest registrations in Supabase and exposes them to the existing admin dashboard. | No hosted social network, public posts/comments, public member directory or customer account. |
| Invitations | Administrators approve and send invitations/add members through supported external-platform mechanisms. Manual invitations are the baseline. Owner chose **decide platform later; keep invitations unpublished**. | Automatic admission requires proven platform support and a separately approved integration; it is not assumed. Platform deferral does not block development of the guest registration/admin design. |
| Community statuses | Pending, Invited and Joined, with Joined recorded only where confirmation is available. | Form submission is not admission; sending/clicking an invitation is not proof of joining. |
| Consent separation | Summit details are not automatically reused for Community registration. | Separate explicit visitor consent is required; marketing/newsletter consent is not bundled into event or Community participation. |

## 2. Guest visitor journeys

### Browse and inquire

Visitors browse the existing five sections and public product/event information, stories, approved demos and About/service content. Preserve the vanilla HTML/CSS/JS design, assets, navigation and existing accessible form patterns. No customer signup, session or account dashboard is required to browse, choose products, register interest or submit an authorized guest form. Existing inquiry/newsletter consent controls remain distinct. Public working demos must not expose purchased files or secrets.

### Store to Selar

1. Visitor reviews a 1751 product and any approved public demo, then uses Add to Cart.
2. Cart retains selected products and remove controls. Guest selection must not depend on a Supabase customer account; the existing local selection approach can be preserved during later implementation, subject to the approved privacy notice.
3. Each purchasable item has an owner-verified HTTPS Selar product/checkout destination. A local product ID maps to its genuine Selar destination/ID; no ID or link is fabricated.
4. Until combined checkout is proven, cart offers **“Buy this item on Selar”** per item and explains that items are purchased separately. It does not show a single “Pay cart total” action implying one transaction. Unsupported quantities, local promotions, tax/shipping promises or cart discounts must not be forwarded or represented as accepted by Selar.
5. Selar conducts checkout, records the sale and manages delivery using the seller's configured capabilities. 1751 neither collects payment details nor creates native Store orders/entitlements to simulate this flow.
6. A return to 1751 or outbound-link click does not prove payment or delivery. Do not mark a local sale paid, clear all selections as purchased or issue files from a return parameter. Any optional locally displayed purchase reference must be explicitly derived from a supported, verified Selar source and is not an independent financial authority.

No cart behavior will be silently changed merely to hide the existing native checkout. Implementation must preserve the UI while making its actual checkout capability clear.

### Community registration and invitation

1. Visitor clicks **Join Community** and a form opens in the existing visual language.
2. Collect full name and email (required), phone number required **when the chosen community is WhatsApp**, and affirmative consent to be contacted and invited. Do not require phone for other platforms without an approved need. Do not collect a password or create an auth.users/customer profile record.
3. On successful persistence, Supabase stores a private registration with status **Pending**, the target external community/platform, and the relevant consent evidence. Show a truthful registration acknowledgment, not “you have joined.” A failed save must not show success. Proposed minimum audit evidence includes consent text/version and timestamp; exact retention/notice remain owner decisions.
4. Authorized administrators view and review registrations in the existing `/admin` dashboard. The user requested dashboard receipt; an email/SMS notification service is not implicitly authorized or assumed.
5. Staff approve the invitation, use the external platform's supported process, and record **Invited** only after the invitation/addition action actually occurred. Keep acting staff/time and appropriate non-sensitive evidence. No automatic admission or mass-message campaign is implied.
6. Staff record **Joined** only with actual supported external confirmation or a verified manual confirmation. If confirmation is unavailable, retain **Invited** and show that external membership is unconfirmed. Do not infer Joined from a link click, form success or elapsed time.

The current Community is inactive; do not represent it as an active on-site community. The initial external platform/group and its owner are still BLOCKED. Until a real destination, notices and invitation operations are approved, keep the registration/invitation feature unpublished in the target rollout. This does not remove the approved public Community section.

Public curated Community information and a private registration form are the selected mode. The only guest submission is registration, not public posts or comments. Platform moderation of actual conversations occurs externally. Website administrators manage registration access, consent and invitation records; further external-community rules are owner-approved operating policy.

## 3. Source of truth and service responsibilities

| Subject | Authority / intended responsibility | Implementation constraint or BLOCKED decision |
| --- | --- | --- |
| 1751 presentation and product catalogue mapping | Approved catalogue/content in 1751; staff curate descriptions, demos and the mapping to Selar. | Add genuine Selar destinations/IDs later; current model has none. Local UUIDs remain local identifiers, not Selar IDs. |
| Payable Store price, currency, availability and sale product identity | Selar checkout/catalogue for the actual sale. This follows the owner's Selar authority decision. | Website display prices must match owner-verified Selar data or clearly defer to Selar. The sync mechanism is unconfirmed; do not claim an API/feed exists or invent polling. Stale/mismatched data must not be presented as a guaranteed payable total. |
| Store transaction/sale record | Selar. | Native Paystack/internal order rows must not become the authority for new Store sales. Preserve old financial/history records without relabelling them as Selar sales. |
| Receipts/payment confirmation | Selar's supported seller/buyer workflow. | Do not generate a parallel 1751 proof-of-payment receipt. Exact configured receipt format and delivery behavior require seller-side verification. |
| Store delivery/access | Selar's supported delivery workflow. | No new native Store signed downloads/entitlements. Confirm every product's actual Selar delivery settings before publication. Public demos remain separate. |
| Store refunds | Refund processing/transaction status through Selar's supported seller process. | Refund eligibility, approval owner, time limits and support contact are **BLOCKED**. No assumed automatic refund endpoint or native Paystack refund fallback. |
| Admin Store reporting | Selar is the financial authority; any verified display/import in 1751 is labelled with provenance, scope and freshness. | No invented sales sync. If none is approved, refer authorized staff to Selar; count catalogue views/clicks separately from sales and preserve historical native data distinctly. |
| Summit registration, capacity and attendance | Supabase guest-registration records and authorized event administrators; **Selar** is the explicitly selected paid-Summit provider. | Verify genuine Selar settlement before seat confirmation; the event/payment/seat reconciliation design remains gated. |
| Community registration/consent/invitation records | Supabase and authorized 1751 administrators. | These are operational records, not a hosted identity/membership system. |
| Community interaction and actual membership | The external community platform. | Record local Joined only when confirmed; never present the website as hosting the conversations. |
| Staff identity and permissions | Existing private Supabase-backed staff identity/MFA and server-side authorization. | Preserve these controls while removing customer identity dependencies; “no customer accounts” is not permission to disable all authentication. |

## 4. Selar multi-product investigation

On 4 November 2026, attempted read-only access through the environment's configured proxy to the main Selar site and candidate help destination:

```sh
curl --head --location --max-time 25 --silent --show-error https://selar.com/
curl --head --location --max-time 25 --silent --show-error https://help.selar.com/
```

Both returned curl exit 56, **CONNECT tunnel failed, HTTP 403**. At that attempt, runtime policy was restricted to the package-manager preset with no custom Selar allowlist entries. No documentation content was retrieved. No credentials were requested or supplied, and no destination-policy bypass was attempted.

**Finding: multi-product support is UNVERIFIED, not proven unsupported.** This applies to a supported handoff of an external 1751 cart, not merely whether Selar might offer a cart within its own hosted store. No endpoint, product-ID format, cart parameter, quantity feature, webhook or API permission is claimed.

The owner's approved fallback is individual genuine Selar checkout links. A combined checkout can replace that fallback only after first-party documentation or approved seller evidence demonstrates the exact seller/account/product capabilities, item/quantity/currency handling, authoritative pricing and supported handoff mechanism, followed by safe staging validation. A screenshot of unrelated checkout or an unverified URL pattern is insufficient.

To resume research, allow the precise required first-party destinations through **environment settings → network access** and retry; at minimum the attempted hosts were `selar.com` and `help.selar.com`. Confirm any redirected/help host before adding it. No network draft or runtime policy was changed by Step 02. Owner-provided official documentation/product links can also establish the next research target. No merchant login, purchase or live transaction was attempted.

## 5. Summit: free and paid guest registration

**Mode is resolved:** admins choose free or paid for each offering. Selecting paid is not permission to publish an unverified checkout. Existing `price_minor` and registration flags are implementation evidence, not a complete approved financial contract.

### Common requirements

- Guest registration never creates a customer account or requires login. Proposed minimal attendee contact is full name/email; exact Summit field set, notices and duplicate/transfer policy remain owner decisions distinct from the already approved Community fields.
- Preserve authoritative capacity checks, transaction locking, idempotency and registration-close rules. Repeated submissions and simultaneous last-seat requests must not create extra confirmed seats. Guest deduplication cannot continue to rely on `(session_id,user_id)` where user_id is absent.
- Check-in is staff-only, audited and based on an eligible registration, not an untrusted receipt image or URL. Repeat check-in must not create extra attendees. Private registration data must not be enumerable via sequential/public references.
- Guest self-service changes/cancellation require a separately designed scoped verification mechanism, such as a private capability, rather than a customer login. Its delivery, expiry/recovery and identity-verification policy are **BLOCKED** pending review; no email-only public edit/cancel endpoint is acceptable. Admin-assisted actions must also have an approved identity-check policy.
- Free cancellation eligibility, deadlines, waitlist use/promotion, transfers and staff overrides require explicit event policy. Preserve historical records and audit who changed state. No destructive migration or automatic identity deletion is part of this plan.

### Free branch

When guest registration and policy are implemented and approved, free registration confirms only after the server has durably saved an eligible record and atomically obtained capacity. Full/closed events return an honest result; waitlisting occurs only if enabled under approved policy. No fake payment/order or provider transaction is needed for a free seat. Registration acknowledgment and confirmed-seat status must be distinguishable where a pending review exists.

### Paid branch — BLOCKED and disabled/unpublished in the target rollout

The owner approved paid offerings as an admin option and explicitly selected **Selar** for paid Summit registration. The financial workflow and settlement operations are still unapproved/unverified. Existing Paystack code is legacy implementation evidence, not the selected future provider. Before activation, approve and test:

1. The selected Selar seller/account responsibility, supported event/product mapping, amount/currency, taxes/fees and guest contact flow.
2. The order of seat reservation and payment, hold/expiry timing, release on failed/abandoned payment, duplicate attempts, late settlement after capacity changes and reconciliation of paid-but-unseated attendees.
3. Server-side authenticated payment verification with event/reference/customer/amount/currency matching, replay protection and idempotent settlement. A redirect, query parameter, checkout click or client claim never confirms payment or a seat.
4. Capacity reconciliation so one verified settlement confirms at most one eligible registration and retries cannot oversell. Overpayment, duplicate/late payment and unresolved payment status go to review, not automatic admission.
5. Cancellations/refunds/chargebacks, attendee communications, waitlist promotion and staff permissions/audit. Refund completion must come from the approved provider workflow, not a checkbox pretending to move money.

Safe interim rollout: browsing and approved free registration only; no paid checkout or “paid seat confirmed” UI until every paid-workflow gate passes. Because this commit is documentation-only, enforcing that feature gate requires a later implementation task.

## 6. Consent, retention and private administration

Community consent specifically covers being contacted and invited to the named external community/platform. It must be affirmative, not prechecked or silently reused from an event submission. Registration notices must explain the relevant data handoff to an external platform and its purpose. Platform selection determines whether a phone number is necessary. Summit registration must not automatically create a Community record, send a Community invitation or subscribe someone to marketing.

Collect only approved fields; keep registrations non-public and permission-bound. Avoid personal data in analytics URLs, frontend bundles, public logs or exported public assets. Validate and rate-limit guest submissions, preserve spam/CSRF safeguards appropriate to the endpoint, and prevent public listing/guessing of attendee or community records. Duplicate handling must not disclose whether another person registered. Invitation approval and state changes require staff permissions and audit history.

**BLOCKED owner policy:** privacy/consent copy, retention periods for registrations and consent/audit records, withdrawal/deletion handling, participant eligibility, notification/support identities and any legal retention obligations. No duration or legal conclusion is invented. Until approved, keep new data-collection features unpublished in the target rollout; do not run indefinite collection under an assumed policy or purge historical records. These policies are separate from private staff authentication.

## 7. Keep / change / retire matrix against current source

“Retire” means remove from new public behavior in a later reviewed change, not delete historical data or destroy source now. Every row is a plan; this commit edits no application files.

| Keep / change / retire | Current exact paths | Required later change and preservation boundary |
| --- | --- | --- |
| Keep | `index.html`; `reference.css`; `reference.js`; `stage1.css`; `stage1.js`; `assets/` | Preserve vanilla design, five public sections, accessible navigation, assets/licenses and working public demos. Adapt only the necessary journey controls. |
| Change | `stage2.js:154`; `stage2.js:167`; `shared/admin-model.js:2` | Preserve cart presentation and local selections; replace native checkout with verified Selar destinations/individual-link fallback. Catalogue mapping/price freshness need supported design. |
| Retire for new Store sales | `backend/api.js:147`; `backend/api.js:339`; `backend/api.js:366`; `backend/admin.js:131`; `backend/admin.js:135` | Native Paystack Store initialization/verification/refund and Supabase delivery must not remain a competing live Store platform. Do not remove shared payment logic blindly before the separate Summit plan is approved. Preserve old records as historical. |
| Retire customer journeys; preserve staff identity | `stage2.js` account/auth form handlers; `index.html:594`; `backend/api.js:266`; `backend/api.js:300`; `backend/render.js:9`; `admin/admin.js`; `backend/admin.js:65` | Remove public signup/login/profile/account dependencies and stale links. Trace shared auth endpoints used by `/admin` before separating or narrowing them. Keep MFA/RBAC, revocation, protected cookies and server authorization. |
| Change guest Summit path | `stage2.js` openRegister; `backend/api.js:377`; `shared/admin-model.js` sessions; `supabase/migrations/202610130001_platform.sql:290` | Replace sign-in redirect and actor-bound registration with approved guest logic, capacity and cancellation identity checks; add an enforced paid-feature gate. |
| Change with additive migrations | `supabase/migrations/202610130001_platform.sql`; `supabase/migrations/202610130002_admin.sql:40` | Profiles, carts, registrations and memberships reference auth.users. Stage 3 already made registration user_id nullable, but API/RPC authentication and uniqueness remain customer-bound; nullability alone does not implement guest registration. Preserve staff foreign keys/audits and historical financial relationships. |
| Change Community; retire hosted social mutations | `stage2.js` loadCommunities/membership/post/comment handlers; `backend/api.js:394`; `index.html:608`; `shared/admin-model.js` communities; both migration files | Keep public section and Join Community button; add private guest registration and staff Pending/Invited/Joined records. Retire public on-site membership/post/comment routes in the target journey; preserve old data for reviewed retention. |
| Change admin operational records | `admin/admin.js`; `backend/admin.js:92`; `backend/admin.js:125`; `supabase/migrations/202610130002_admin.sql:145` | Add guest Community queue/consent/status actions and guest Summit handling. Current memberships view joins user profiles; do not relabel that existing model as the new external-community workflow. |
| Change reporting | `supabase/migrations/202610130002_admin.sql:145`; `supabase/migrations/202610130002_admin.sql:155`; `backend/admin.js` orders/refunds/analytics | Distinguish Selar-origin sale evidence, historical native Store records, Summit registration/payment data and catalogue clicks. Existing local orders/payments totals are not authoritative new Selar sales. No fabricated conversion/revenue metrics. |
| Keep controls; change references | `backend/uploads.js`; `backend/api.js` email templates/jobs; `jobs/worker.js`; `scripts/backup.mjs`; `scripts/restore.mjs` | Preserve protected media, quarantine, audit and recovery controls. Revise account-dashboard/receipt/delivery copy and scheduled native reconciliation only after the intended flows are approved; no messages/jobs run now. |
| Keep and adapt tests later | `tests/platform.test.mjs`; `tests/admin.test.mjs`; `tests/admin-integrity.test.mjs`; `tests/browser.mjs`; `tests/admin-browser.mjs`; `tests/cloudflare-runtime.mjs` | Preserve security/capacity assertions while replacing customer-account/Paystack Store expectations with the accepted contract. Test doubles must remain explicit and separate from hosted provider acceptance. |

## 8. Acceptance tests for later implementation (not executed in Step 02)

| ID | Scenario | Required observable result |
| --- | --- | --- |
| A01 | Guest visits each public section and approved demo at phone/tablet/desktop widths | Five sections and preserved design work without customer signup/login/profile or a session requirement. |
| A02 | Anonymous/ordinary user directly calls private admin operations | Access denied; authorized staff still need MFA/permissions, including after customer endpoints are removed. |
| A03 | Guest adds two products, refreshes, removes one and uses checkout | Cart selection remains useful; unverified combined checkout is absent; each Buy action resolves to the correct verified Selar destination with separate-purchase messaging. |
| A04 | Product URL/ID is missing, price is stale or unsupported quantities/discounts are supplied | No fabricated checkout/total; item unavailable or visitor clearly directed to verified Selar pricing. Source mismatch cannot create a native charge. |
| A05 | Visitor returns from Selar with forged success/reference parameters | No native paid Store record, entitlement, receipt, delivery or sale count is created from the client claim. |
| A06 | Staff reviews Store revenue/refunds | Selar-derived information has actual verified provenance/freshness, or staff use Selar directly. Native historical figures and outbound clicks are not presented as current Selar sales. |
| A07 | Guest submits Community form without required name/email/consent; WhatsApp target lacks phone | Validation rejects submission. Other platforms do not demand phone absent an approved reason; no auth.users/profile is created. |
| A08 | Valid Community form saves, fails or is retried | Durable private Pending record and honest acknowledgment on success; no success after failed persistence; safe idempotency/deduplication without leaking another person's registration. |
| A09 | Staff processes Community record | Only permitted staff can approve/update; Invited requires an actual invitation action; Joined requires confirmation. Unsupported automatic admission is absent. |
| A10 | Visitor completes Summit registration without Community opt-in | No Community record/invitation or marketing subscription is created. Independent affirmative consent is required for any later transfer. |
| A11 | Two guests compete for the last free seat; a request retries | At most one new confirmed registration; repeated submission is idempotent; approved full/waitlist behavior and closure rules hold. |
| A12 | Admin selects paid mode before provider/seat workflow approval | Offering cannot expose a paid checkout or confirm a paid seat. Free mode remains distinct and creates no fake payment. |
| A13 | After later paid activation, redirect/webhook replay/wrong amount/late or duplicate payment occurs | Client success never confirms a seat; authenticated matched settlement is idempotent; unresolved paid/capacity states require reconciliation without overselling. |
| A14 | Unauthorized guest guesses a registration reference or requests cancellation/check-in | No private disclosure or mutation; approved scoped verification and staff permissions are required. Valid cancellation applies approved rules and is audited. |
| A15 | Consent withdrawal, retention expiry and data export are exercised in staging | Only approved policy is applied, with permitted access/audit and preserved required history; no invented retention or destructive purge. |
| A16 | Migration runs on a disposable copy of the baseline | Additive guest changes preserve existing staff MFA/RBAC, history and relationships. Source/static build contains no credentials or private registration data. |

## 9. Open decisions and safe defaults

These items are genuinely unresolved; previously confirmed decisions are not being asked again.

| ID | Owner decision/evidence still required | Status and safe default |
| --- | --- | --- |
| B01 | Production domain purchase/registration, final origin/DNS ownership and production configuration | **DEFERRED TO PRODUCTION LAUNCH, not a development blocker.** Official name is 1751 Digital; permanent domain TBC. Develop/test with the actual assigned Cloudflare `pages.dev` staging origin and flexible environment configuration. No staging site is created by this ADR. |
| B02 | Initial external platform, actual community destination, responsible staff and confirmation process | **OWNER-DEFERRED; BLOCKED only for activation.** Invitations stay unpublished until selected/approved. Manual admin-approved invitations remain the baseline; destination/consent policy gate public collection. Unrelated development continues. |
| B03 | Selar financial/seat workflow, including verified settlement and hold/expiry/late-payment rules | **BLOCKED for paid registration activation.** Selar and admin free/paid choice are approved; paid execution remains disabled/unpublished until that workflow passes its gates. |
| B04 | Verified Selar product destinations/account capabilities and price-refresh process; receipts/support/refund policy owner | **BLOCKED for real Store transactions/publication of unverified products.** Keep cart and choose per-item links; do not invent combined checkout or a native fallback. |
| B05 | Privacy/consent text, retention/withdrawal policy, participant eligibility and named operational contacts | **BLOCKED for new data collection/launch.** Keep new forms unpublished pending approved notices and policy. No fixed retention period is assumed. |
| B06 | Summit guest fields, duplicate/transfer rules, cancellation deadlines/identity checks, waitlist policy and check-in operations | **BLOCKED for those production behaviors.** Preserve capacity/security requirements in design; do not infer policies from old account-based defaults. |
| B07 | Official evidence of an external-cart multi-product Selar handoff | **BLOCKED capability investigation, not a requirement to invent the feature.** Approved individual-link fallback remains selected while evidence is unavailable. |

Owner replies received on 4 November: retain **1751 Digital**, production domain **TBC**, continue development/testing on Cloudflare `pages.dev` with flexible domain configuration; **defer Community platform and keep invitations unpublished**; use **Selar for paid Summit registration**. These answers supersede the earlier questions and must not be requested again. The remaining questions concern verified Selar capabilities/destinations, payment/seat operations, consent/retention and event operational policy, not the already settled provider or modes.

## 10. Exact Step 03 readiness gate

The settled contract is **READY for Step 03 scope review and continued development**. Supply the actual Step 03 instructions before implementing that step, and check them against this record. B01 is a production-launch gate only; B02 is an explicitly deferred feature-activation gate. Do not block unrelated development on domain purchase or Community platform selection. B03–B06 gate only the features/operations to which they apply. Unrestricted activation/production launch remains **BLOCKED**.

A constrained next step may develop and test guest forms, admin workflows and disabled integrations in isolated staging with synthetic data. It must exclude deployment/publication and activation of unresolved data-collection, paid-Summit or unverified commerce behavior unless separately authorized and gated. Multi-product checkout is not a required blocker when the approved individual-link fallback is used. Community mode and admin free/paid mode are resolved; unanswered platform/payment details gate feature activation, not unrelated development.

To enable each feature later: resolve its applicable B-items, implement and enforce its gates, run the corresponding A-tests on isolated staging with approved data/provider access, and record actual results. Passing old tests is insufficient because they exercise the old account/Paystack business model. No step may infer public deployment authorization from this ADR.

## 11. Changes, verification and delivery

Changed files: this ADR, the Step 01 issues register (updated to point to resolved owner choices and remaining blockers), and `docs/LAUNCH_CHECKLIST.md` (production-domain task and updated contract gates). Current code, SQL, lockfile, tests and visual assets are untouched. Starting tree was clean; branch created with `git switch -c dev/1751-step02` from the recorded starting commit.

On 6 November the user resumed Step 02 after publishing the cloud environment. Inspection confirmed the existing branch, three prior commits and the uncommitted ADR survived restoration. Completed edits were retained; only the outstanding documentation work was finished. No environment configuration was reapplied, no environment was published and no website was deployed by this step.

Inspection used `git status --short --branch`, `git rev-parse HEAD`, and targeted `rg`/`sed` reads of `stage2.js`, `backend/api.js`, `backend/admin.js`, `shared/admin-model.js` and both SQL migrations. The two exact Selar curl commands/results are recorded in section 4. Documentation validation uses `git diff --check` and a diff path check proving only the three documentation files changed. No application suite was rerun for this planning-only change; section 8 lists future acceptance tests, not claimed passes.

Commit SHA is supplied in the final handoff; resolve the documentation tip with `git rev-parse dev/1751-step02`. No push or PR was created. The Step 01 tag and backups remain intact. Owner actions are limited to answering the B-items relevant to the next step and, if desired, enabling precise research destinations in environment settings. No production dashboard action is required or authorized here.
