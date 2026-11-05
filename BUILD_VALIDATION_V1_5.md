# Build validation — Version 1.5

Completed in the artifact environment:
- Repository copy and file-structure validation.
- JSON manifest parsing.
- Python archive and checksum validation.
- Static review of new controller/service imports and route paths.

Not executed here:
- `npm install`
- NestJS/Next.js compilation
- Prisma client generation or migration
- PostgreSQL integration tests
- Playwright browser tests
- Docker Compose startup

Required before promotion:
```bash
npm install
npm run db:generate
npm run typecheck
npm test
npm run build
npm run test:e2e
```
