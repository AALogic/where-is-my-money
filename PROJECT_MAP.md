# PROJECT_MAP.md

## Proposed system shape

The product should be built as a modular web application with explicit boundaries between user interface, domain logic, data ingestion, graph analytics, AI enrichment, reporting, and infrastructure adapters.

## Recommended technical direction

Use a stack that enterprise development teams can maintain while still supporting a rich graph UI:

```text
Frontend: React + TypeScript
Backend: ASP.NET Core / .NET
Database: PostgreSQL
Bulk analytics/import helper: DuckDB for Parquet where useful
Background jobs: .NET worker/job runner
Auth: Microsoft Entra ID adapter, with local development fallback
AI: provider adapter, initially OpenAI-compatible
```

This is a recommendation, not yet a final lock. The reason to prefer .NET on the backend is maintainability, enterprise integration support, background-job maturity, and authentication ecosystem fit. The reason to keep React/TypeScript on the frontend is graph/UI ecosystem strength.

## Major subsystems

### Web UI

User-facing interface for search, filters, entity pages, graph exploration, AI sessions, and reports.

Must not:

- connect directly to the database,
- perform procurement normalization,
- run AI/web research directly,
- contain core analytics logic that belongs in backend/domain services.

### Backend API

Application boundary used by the web UI. Owns request validation, authorization, orchestration, and response shaping.

### Domain services

Core business logic for procurement analytics:

- buyer/supplier analysis,
- tender and award interpretation,
- category/technology aggregation,
- relationship and graph context construction,
- report context preparation.

### Data ingestion

Adapters and jobs for importing or querying public procurement data. Each source should have its own adapter and mapping layer.

Initial adapters:

- Atlas REST adapter,
- Atlas dataset import adapter,
- BZP fallback adapter placeholder,
- TED fallback adapter placeholder.

### Database/repositories

Persistent storage for normalized procurement data, users, analysis sessions, AI findings, evidence, and reports.

PostgreSQL is the recommended primary database. DuckDB can be used as an import/analytics helper for Parquet, but should not be the main application database.

### Graph service

Builds graph-ready data from domain entities and analytics context. The visualization library should be replaceable.

### AI enrichment service

Coordinates AI tasks and web research against a bounded context. AI provider, browser/search tools, and prompts should be replaceable.

Prompts should be treated as versioned task definitions. The product should support adding future prompts without redesigning the application.

### Report service

Turns structured analysis sessions into exportable reports, likely PDF in the first release.

Reports should be template-driven so the same session can later produce different outputs: full account report, meeting questions, pain-discovery questions, or action plan.

### Auth adapter

Hides the selected auth provider. Microsoft SSO is likely but not final.

## Dependency direction

Preferred flow:

```text
Web UI -> Backend API -> Domain services -> Repositories/adapters
                         -> Graph service
                         -> AI enrichment service
                         -> Report service
```

Adapters are edges of the system:

- procurement source adapter,
- AI provider adapter,
- auth provider adapter,
- report renderer adapter,
- graph renderer adapter,
- web research/search adapter.

## Extension points

Future changes should be possible without rewriting the product:

- add another procurement data source,
- add another scraper,
- add another graph view,
- switch AI provider,
- switch auth provider,
- add another report type,
- extend beyond IT into other industries.

## Architectural guardrails

- Keep raw external data separate from normalized domain data.
- Keep AI findings separate from verified procurement facts.
- Every AI finding should carry evidence and timestamps.
- Do not let AI enrichment mutate core procurement records directly.
- Prefer background jobs for long imports, scraping, enrichment, and report generation.
- Keep graph model selection as a deliberate design decision, not an accidental UI library choice.
- Keep external source access behind backend adapters, so provider behavior and operational controls stay outside the UI.
- Preserve `id`, `processId`, source URLs, and source names for all procurement records.
