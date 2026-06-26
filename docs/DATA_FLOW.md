# Data Flow

## Data Strategy

The product uses a layered data strategy:

```text
Atlas REST API -> operational queries and fresh records
Atlas GitHub dataset -> bulk analytics, cache seed, historical baseline
BZP / TED -> verification and future fallback
Local database -> normalized product data and analysis sessions
AI research layer -> public web enrichment attached to session context
Report layer -> PDF output from session data
```

## High-Level Flow

```text
User input
  -> buyer/supplier/segment query
  -> procurement source adapter
  -> normalization
  -> local storage/cache
  -> analytics aggregation
  -> graph context
  -> AI enrichment context package
  -> prompt-driven public research
  -> session findings
  -> PDF report
```

## Buyer Analysis Flow

```text
buyer NIP
  -> Atlas buyer profile
  -> Atlas tender history
  -> normalize buyer, suppliers, tenders, values, CPV, dates
  -> deduplicate notices vs procedures
  -> calculate spend and supplier rankings
  -> build relationship graph
  -> store analysis session
```

## Supplier Analysis Flow

```text
supplier NIP
  -> Atlas contractor profile / tender results
  -> identify buyers and wins
  -> aggregate by region, buyer, category, and value
  -> show where the supplier is embedded
  -> compare against selected buyer or market segment
```

## Region And Segment Flow

```text
region + category/technology
  -> filtered procurement records
  -> buyer ranking
  -> supplier ranking
  -> recurring buyer-supplier relationships
  -> segment-level network view
```

## AI Research Context Flow

The AI layer receives a structured context package from the current board.

Conceptual package:

```text
analysis session
selected entity
visible graph nodes
visible graph edges
tender summaries
supplier rankings
category and technology signals
user-selected prompt
allowed research direction
required output format
```

The AI response is stored back into the session as an enrichment finding.

## Evidence Handling

AI research should distinguish:

- procurement facts from source data,
- AI-generated hypotheses,
- external public web findings,
- user notes,
- report-ready conclusions.

Each external claim should be able to carry source references when required by the prompt.

## Data Boundaries

The product should preserve the difference between:

- raw source records,
- normalized procurement entities,
- graph-ready relationships,
- AI enrichment findings,
- report text.

This keeps the product explainable and makes later extensions safer.
