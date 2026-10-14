# TimeAndAttendance2026

WorkTime is an employee time-registration application.

## Local setup

Use Ubuntu/WSL with .NET SDK 10.0.402 and Node.js 24.22.0 (npm 11.19.1).
The SDK is pinned in `global.json`; run `nvm use` to select the version in `.nvmrc`.

From the repository root:

```bash
dotnet build WorkTime.sln
dotnet run --project src/WorkTime.Api --no-launch-profile --urls http://localhost:5080
```

In another terminal:

```bash
curl http://localhost:5080/health
```

Expected response: `Healthy`.

## Backend structure

- Domain: business rules; no project dependencies.
- Application: use cases; references Domain.
- Infrastructure: persistence and integrations; references Application and Domain.
- API: HTTP endpoints and dependency registration; references Application and Infrastructure.

## Tests

```bash
dotnet test WorkTime.sln
```

All backend tests live in `tests/WorkTime.Tests`, organized into folders by area.
The `Integration` folder currently verifies `/health` through an in-process API host.

Domain and Application currently have no test cases because their implementations are empty.
Database integration tests will use real SQL Server when persistence is added.

## Frontend

React + TypeScript with Vite lives in `web/worktime-web`.
From the repository root:

```bash
nvm use
cd web/worktime-web
npm ci
npm run dev
```

Open http://localhost:5173. The initial page is a WorkTime placeholder.

To verify the frontend from its directory:

```bash
npm run typecheck
npm run lint
npm run build
```

Current progress: the backend skeleton, `/health`, one test project, and the React starter.
Local SQL Server setup remains in Phase 1.
