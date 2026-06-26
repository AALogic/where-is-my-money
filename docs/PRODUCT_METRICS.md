# Product Metrics

## Measurement Philosophy

The product is measured by one thing above all: whether it helps a salesperson move from raw procurement data to a concrete sales decision.

Usage alone is not enough. A user can click through many tenders and still leave without a better next move.

## North Star Metric

**Completed account intelligence sessions.**

A completed session means:

- a buyer, supplier, region, or segment was selected,
- procurement data was explored,
- the graph was used,
- the user saved an insight, ran AI enrichment, or generated a report.

## Activation Metrics

Activation tells us whether a new user reaches the first useful moment.

Suggested signals:

- first buyer NIP search completed,
- buyer profile loaded,
- graph opened after search,
- top suppliers viewed,
- first supplier drill-down completed,
- time from first search to first graph view.

## Engagement Metrics

Engagement tells us whether the product supports actual analysis rather than one-off lookup.

Suggested signals:

- graph layer toggles per session,
- supplier drill-downs per session,
- tender detail views per session,
- region or segment expansion rate,
- AI enrichment prompts run per session,
- saved findings per session,
- report generation rate.

## Outcome Metrics

Outcome metrics connect the product to sales work.

Suggested signals:

- report downloaded,
- report shared internally,
- first-meeting question pack generated,
- account strategy report generated,
- user returns to the same account before a meeting,
- user creates a follow-up analysis from the same buyer or supplier.

## Quality Metrics

Quality metrics protect the product from becoming a generic dashboard or an unreliable AI note generator.

Suggested signals:

- percentage of AI findings with source evidence,
- unsupported finding rate,
- prompt usefulness rating,
- report section deletion or edit rate,
- repeated failed searches,
- zero-result buyer or supplier searches,
- mismatch between selected intent and generated report type.

## Friction Signals

Friction signals show where the user loses momentum.

Useful examples:

- search started but no entity selected,
- buyer profile opened but graph not used,
- graph opened but no node clicked,
- AI prompt selected but not run,
- AI enrichment completed but not saved,
- report preview opened but not downloaded,
- filters changed repeatedly without reaching a report.

## Product Learning Questions

Metrics are there to answer product questions:

- Do users start from buyers, suppliers, regions, or segments?
- Which graph layers produce the most useful drill-down?
- Which prompts lead to report-worthy findings?
- Which report templates are reused?
- Where do users stop before creating a useful output?
- Which data gaps block the next step?

## Example Event Model

```json
{
  "event": "graph_node_opened",
  "session_id": "session_123",
  "user_role": "salesperson",
  "entity_type": "supplier",
  "entity_id": "supplier_nip_or_internal_id",
  "active_layer": "cash_flow",
  "source_view": "buyer_profile",
  "timestamp": "event_time"
}
```

The event model is privacy-aware and avoids storing unnecessary sensitive data.
