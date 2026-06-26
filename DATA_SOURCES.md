# DATA_SOURCES.md

## Source strategy

Recommended first-release data strategy:

```text
Atlas REST API = primary operational source
Atlas GitHub Parquet/CSV = bulk analytics, cache seed, and historical baseline
BZP/e-Zamowienia = primary-source fallback and verification
TED API = EU-notice fallback and verification
Atlas website = public market reference and source-discovery layer
SWZ/OPZ attachments = future separate document-fetching module
```

The source strategy should stay pragmatic: use Atlas where it already provides clean public-procurement structure, keep primary public sources available for verification, and avoid binding the product to one provider boundary.

## Confirmed external sources

### Atlas Przetargow website

URL: <https://atlasprzetargow.pl>

Role:

- public view of the procurement market,
- quick source discovery for buyers, suppliers, and tender examples,
- qualitative reference for how procurement entities are presented to business users.

### Atlas REST API

Integration surface:

```text
Tender search
Tender detail
Buyer profile by NIP
Supplier profile where available
```

The application should call Atlas through the backend integration layer. This keeps caching, throttling, observability, provider changes, and browser constraints outside the UI.

Important fields observed:

- `id`
- `source`
- `noticeType`
- `title`
- `buyer`
- `buyerNip`
- `contractorName`
- `contractorNationalId`
- `contractors`
- `cpvCode`
- `date`
- `createdAt`
- `estimatedValue`
- `currency`
- `noticeUrl`
- `objectId`
- `processId`
- `isDuplicate` / duplicate metadata where available

Tender detail can include richer fields such as:

- `htmlBody`
- `awardCriteria`
- `contractors`
- `noticeUrl`

### Atlas GitHub dataset

Repo: <https://github.com/atlasprzetargow/polish-tenders-dataset>

Role:

- bulk import,
- historical local analytics,
- schema reference,
- reproducible baseline.

Current README describes:

- CSV and Parquet exports,
- tender, buyer, and contractor datasets,
- BZP and TED as upstream public sources,
- recurring historical exports,
- documented schema and open licensing.

Important files:

```text
data/tenders_YYYY.csv
data/tenders_YYYY.parquet
data/buyers.csv
data/contractors.csv
schema/tenders.md
schema/buyers.md
schema/contractors.md
```

The export code uses `sqlalchemy` and `psycopg2-binary` with `DATABASE_URL`, which strongly suggests that Atlas exports from a PostgreSQL-compatible relational database. Our application should use PostgreSQL as its main database, while still using Parquet/DuckDB for efficient bulk loading and analytical checks.

### Atlas MCP server

Repo: <https://github.com/atlasprzetargow/mcp-server>

Role:

- reference for official tool boundaries,
- possible future integration for AI assistants,
- not the primary application integration for the first release.

Useful public tool ideas:

- `search_tenders`
- `get_tender`
- `get_buyer`
- `get_contractor`
- `search_entities`
- `get_category_stats`
- `get_province_stats`
- `search_cpv`

### BZP / e-Zamowienia

Role:

- primary-source fallback,
- verification layer,
- future direct ingestion if Atlas coverage or terms become limiting.

Known concern:

- direct matching by organization name is brittle,
- NIP and aliases are necessary,
- separate BZP integration would add complexity.

### TED API

Role:

- EU-notice fallback,
- verification for notices above EU thresholds,
- future source-specific enrichment.

Known concern:

- less convenient for Polish NIP-centric workflows,
- Atlas normalization is more useful for the first release.

## First-release source decision

The first release should not try to rebuild Atlas from BZP + TED directly.

The first release should:

- use Atlas REST API for fresh operational queries,
- use Atlas Parquet/CSV dataset as a bulk analytical seed where useful,
- store normalized local records in PostgreSQL,
- preserve source IDs and URLs,
- cache Atlas responses,
- separate Atlas facts from AI-enriched findings,
- keep BZP/TED adapters as future/fallback boundaries.

## Database recommendation

Use PostgreSQL as the application database.

Rationale:

- compatible with internal enterprise expectations,
- aligns with Atlas export tooling indicators,
- handles relational data, auth/session metadata, reports, and audit trails well,
- can be extended with JSONB, full-text search, trigram search, and later pgvector if needed,
- easier to hand off to internal .NET developers than DuckDB-only architecture.

Use DuckDB optionally for:

- reading Parquet,
- fast local analytical transforms,
- import validation,
- one-off aggregate checks.

Do not use DuckDB as the main application database for the first release.

## Key modeling cautions

- One procurement procedure can produce multiple notices.
- `id` identifies a notice; `processId` links notices in one procedure.
- Record counts, procedure counts, result counts, and win counts are different metrics.
- `date` means publication date; `createdAt` means Atlas ingestion/aggregation time.
- Winner/contractor fields are mostly present on result notices.
- Dataset contractor data may anonymize natural persons.
- Consortium handling requires detail/API data when full membership matters.
- Atlas API/website counts may differ because they count or deduplicate differently.
- SWZ/OPZ attachments should be treated as a separate future document module.
