# PRODUCT_SPEC.md

## Summary

The product is a web-based market intelligence application for analyzing Polish public procurement. It combines structured procurement data, graph exploration, AI-assisted web research, and report generation. The first target domain is IT sales into public-sector buyers in Poland.

## Users and jobs

### Salesperson

Wants to understand a buyer, supplier, technology area, or market segment before planning outreach.

Needs:

- fast search and filtering,
- clear relationship view,
- evidence-backed insights,
- practical questions and next steps.

### Sales leader

Wants to understand market structure, concentration, recurring winners, spending trends, and account opportunities.

Needs:

- segmentation,
- ranking and aggregation,
- repeatable reports,
- historical comparisons.

### Technical operator/admin

Wants to maintain data imports, AI provider configuration, auth, and future integrations.

Needs:

- documented architecture,
- clear adapters,
- reliable jobs,
- verification commands.

## Data concepts

The product should model at least:

- public buyer / contracting authority,
- private supplier / contractor,
- tender or procurement notice,
- award / result,
- contract value and currency,
- dates and time periods,
- CPV/category/domain classification,
- detected technology/product/service terms,
- relationship between buyer and supplier,
- graph node and graph edge,
- AI enrichment finding,
- source evidence,
- analysis session,
- generated report.

## Functional capabilities

### Data ingestion

The app imports and queries public procurement data. The first source strategy is Atlas Przetargow first, with BZP/e-Zamowienia and TED as fallback/verification layers.

Expected behavior:

- fetch data through Atlas REST API for fresh operational queries,
- import Atlas GitHub Parquet/CSV data where useful for historical analytics,
- store normalized records in the local database,
- normalize them into internal entities,
- preserve raw/source references where useful,
- avoid duplicate imports,
- expose import status and errors.

See `DATA_SOURCES.md` for the detailed source strategy.

### Market analytics

The app should answer questions such as:

- which suppliers win most often for a buyer,
- how much money flows between a buyer and suppliers,
- what categories or technologies dominate a buyer or segment,
- which suppliers dominate a category,
- what changed over time,
- where repeated relationships suggest sales-relevant patterns.

### Graph exploration

The app should display relationships between buyers, suppliers, awards, categories, and technologies as a dynamic graph. The user should be able to start from a buyer NIP, contractor NIP, category, technology, or tender where supported. The graph should change its visible layers when the selected entity/context changes.

The exact graph model and visualization style are not chosen yet and require a separate design conversation.

The graph must be useful for business analysis, not just visually impressive.

### AI enrichment

The app should allow the user to ask AI to enrich the selected context. Example tasks:

- research supplier websites,
- identify partners and solutions,
- inspect public job postings,
- find relevant people or roles,
- summarize likely vendor capabilities,
- identify gaps, pains, or conversation angles.

The first release should provide infrastructure for prompt-driven AI enrichment rather than hardcoding final prompts. Prompts should be versioned/configurable, attached to a task type, and able to require evidence, sources, and output structure.

AI output must include source evidence when the prompt requires external claims and should remain tied to the analysis session.

### Reporting

The app should generate a report, likely PDF in the first release, based on:

- selected procurement data,
- graph context,
- AI enrichment findings,
- user questions and answers,
- generated sales strategy.

The first release should provide reporting scaffolding. Report templates should be configurable so future report types can transform the same session into different outputs, for example:

- whole-session summary,
- first-meeting questions,
- questions that create doubt or reveal pain,
- account strategy,
- operational next-step plan.

The report should help a salesperson decide how to approach an organization.

### Authentication

The app should support organization login. Microsoft Entra ID / Microsoft SSO is the preferred direction if implementation stays straightforward. The architecture should keep auth provider-specific logic behind an adapter so local development login or another provider can be used if needed.

### Deployment context

The app is intended for controlled internal deployment. Provider credentials, auth secrets, and AI/API configuration should be supplied through environment variables or a secret-management system, not committed to the repository.

## First-release acceptance criteria

The first release should be accepted only when:

- a user can log in,
- Atlas REST API can be queried through the backend,
- the local database can store normalized procurement records and source references,
- Atlas Parquet/CSV import path is supported or explicitly deferred,
- buyer/supplier/tender data can be searched and filtered,
- core market aggregations are visible,
- at least one useful graph view exists,
- AI enrichment can run against selected context through a provider adapter,
- prompt definitions can be added or changed without rewriting core application logic,
- AI findings can include evidence/source metadata,
- at least one report template can be generated from an analysis session,
- the app has a database and migration story,
- the project has clear setup documentation and verification commands.

## Open product decisions

- exact graph model and graph visualization style,
- final first user workflow and default entry point,
- required fields for procurement records,
- exact Microsoft SSO vs local-dev-login implementation path,
- hosting/deployment target,
- report format and template,
- legal/compliance boundaries for AI web research.
