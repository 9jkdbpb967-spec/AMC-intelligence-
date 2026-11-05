git init
git branch -M main
git remote remove origin 2>/dev/null || true
git remote add origin https://github.com/9jkdbpb967-spec/AMC-intelligence-.git

git add .
git commit -m "Add AMC-EOS v10.52 First-Green Hardened"

git pull origin main --rebase
git push -u origin main
# AMC\-EOS Enterprise v3\.9 — Daily Service Delivery

# AMC\-EOS Enterprise v2\.3 — Production Repository Baseline

See `docs/PRODUCTION_REPOSITORY_GUIDE.md` and `docs/RELEASE_READINESS_MATRIX.md` before running or deploying\.

# AMC\-EOS Enterprise v2\.2

Workforce Readiness & Scheduling Controls release\. See `RELEASE_2_2.md` and `START_HERE_FOR_AI.md`\.

# AMC\-EOS v0\.5 — Engineering Hardening

A development MVP for referral relationship management, supported\-living intake operations, task control, user administration, and audit visibility\.

## Added in v0\.3

- Organization detail workspace with contacts and relationship timeline
- Public\-contact creation and activity logging
- User administration for CEO, Admin, HR, Referral, Operations, Finance, DSP, and Quality roles
- Task Center with due dates and completion workflow
- Read\-only audit\-log viewer for authorized roles
- Secure\-document metadata model and storage abstraction endpoint
- Expanded audit events for users, contacts, activities, and documents
- Updated navigation and CRM profile links

## Existing capabilities

- JWT authentication and seeded administrator
- Role\-based authorization foundation
- Referral organization CRM and CSV import
- Referral/client intake creation
- Kanban intake pipeline
- Executive dashboard
- PostgreSQL/Prisma data model
- Docker Compose local environment

## Run locally

```bash
cp .env.example .env
# Replace all example credentials and secrets.
docker compose up --build
```

Open `http://localhost:3000/login`\.

Development login:

- Email: `admin@amceos.local`
- Password: value of `SEED_ADMIN_PASSWORD`

## Important document\-storage note

The v0\.3 API stores document metadata only\. It does not persist uploaded file bytes\. Production implementation should connect the `storageKey` field to encrypted private object storage, malware scanning, signed download URLs, retention rules, and access logging\.

## Production warning

This repository is a development MVP\. Do not store real resident health, Medicaid, personnel, or financial data\. Before production, complete the controls in `PRODUCTION_READINESS.md`, obtain legal/security/privacy review, add MFA or SSO, use managed secrets, validate backups, implement encrypted private file storage, and confirm current Washington program requirements\.

## Version 0\.4 — IP and AI Handoff Edition

This release adds a full blueprint for continuing development with another AI coding service\. Begin with `docs/AI_BUILD_BLUEPRINT.md` and `docs/ai-prompts/MASTER_CONTINUATION_PROMPT.md`\.

### Intellectual Property Package

- `IP_ASSET_REGISTER.md`
- `NOTICE_PROPRIETARY.md`
- `docs/COMMERCIALIZATION_BLUEPRINT.md`

### Engineering Blueprint

- Product vision and architecture
- Domain model and controlled vocabulary
- Security/privacy release gates
- Definition of done and test strategy
- Prioritized backlog and module specifications
- AI change protocol and reusable prompts

## Version 0\.6 engineering controls

- API routes use the `/api` prefix; health endpoints remain `/health` and `/ready`\.
- Unknown request fields are rejected to reduce accidental mass assignment\.
- Every response includes an `x-request-id`; errors return the request ID for support tracing\.
- Run `npm run ci` before merging changes\.
- Follow `docs/release/MIGRATION_WORKFLOW.md` for all schema changes\.
- Review `docs/PERMISSION_MATRIX.md` before adding endpoints or screens\.

## Version 0\.6 highlights

Tenant isolation, membership\-scoped roles, rotating refresh sessions, login throttling foundation, document quarantine lifecycle, and AI\-ready security blueprints\. This remains a development system and is not approved for real protected health information\.

## v3\.1 executable validation

The `pilot-runtime` now includes two demo tenants, idempotent referral creation, session revocation, referral activity history, and four passing end\-to\-end tests\.

```bash
cd pilot-runtime
python3 -m unittest -v tests/test_vertical_slice.py
```

## v4\.5 AI Knowledge & Executive Assistance

The runnable pilot now includes governed AI assistants grounded in approved tenant\-scoped knowledge sources, citation history, human approvals, usage tracking, and a deterministic no\-network provider\. See `docs/product/AI_KNOWLEDGE_EXECUTIVE_ASSISTANCE_V4_5.md`\.
