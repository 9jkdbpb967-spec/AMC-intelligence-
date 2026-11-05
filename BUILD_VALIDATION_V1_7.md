# Build Validation — AMC-EOS Enterprise v1.7

## Completed static checks
- Repository copied from the v1.6 pilot-admissions baseline.
- Resident Prisma models and indexes are present.
- ResidentsController is registered in AppModule.
- Admission workflow creates/reactivates a resident and admission timeline event in the existing transaction.
- Resident web routes are present.
- OpenAPI YAML parses successfully.
- PROJECT_STATE.json parses successfully.
- Archive file inventory and SHA-256 manifest were regenerated.

## Not executed in this artifact environment
- npm install
- Prisma client generation
- Prisma migration generation or application
- TypeScript compilation
- Jest unit/integration tests
- Testcontainers PostgreSQL tests
- Playwright browser tests
- Docker Compose startup
- Penetration or security testing

## Promotion gate
Do not enter protected resident, Medicaid, medical, employee, or financial information until all unexecuted checks pass in a controlled environment and the deployment receives privacy, security, operational, and regulatory review.
