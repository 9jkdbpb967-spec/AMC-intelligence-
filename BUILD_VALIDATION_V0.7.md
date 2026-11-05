# AMC-EOS v0.7 Build Validation

## Static validation completed
- Repository copied from v0.6 and versioned to 0.7.0.
- New source files and documentation are present.
- Prisma schema contains tenant-scoped background jobs.
- AppModule includes sessions, jobs, storage, and scan verification providers.
- OpenAPI bootstrap is configured.
- Document workflow blocks downloads until malware clearance.

## Required external validation
Run in a normal Node/Docker environment:
```bash
npm install
npm run prisma:generate
npm run ci
```
Then create and review a Prisma migration. Do not deploy or enter sensitive data until compilation, migrations, authorization integration tests, private-object storage, backup restoration, and security review pass.
