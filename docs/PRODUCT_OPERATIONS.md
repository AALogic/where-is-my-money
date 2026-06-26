# Product Operations

## Purpose

Product operations describe how the product keeps learning from users.

The product is analytical by nature. Its roadmap improves when explicit feedback is combined with behavioral signals from real sessions.

See also: [Product Metrics](PRODUCT_METRICS.md).

## Feedback Backlog

The product keeps a backlog of user-reported needs.

Good backlog inputs include:

- missing buyer or supplier views,
- confusing graph interactions,
- report sections users ask for repeatedly,
- prompts users want to run,
- data fields salespeople keep asking about,
- places where users export data manually,
- cases where procurement facts need clearer explanation.

## Event Tracking

Event tracking explains how users move through the workflow.

Example events:

- buyer NIP searched,
- supplier opened,
- region filter changed,
- graph layer toggled,
- graph node expanded,
- tender detail opened,
- AI prompt selected,
- AI enrichment started,
- AI finding saved,
- report generated,
- report downloaded,
- workflow abandoned before report,
- user returned to previous graph layer.

Events are connected to a session so the team can understand the full path from search to insight to report.

## Funnel Questions

Event data answers questions that interviews alone often miss:

- where users start their analysis,
- which filters they actually use,
- which graph layers create drill-down,
- where they stop before AI enrichment,
- which prompts produce saved findings,
- which report types are downloaded,
- which steps slow users down.

## Product Learning Loop

The intended loop:

```text
user behavior
  -> event signals
  -> feedback backlog
  -> product decision
  -> roadmap item
  -> improved workflow
```

## Success Signals

Strong signals:

- users answer buyer cash-flow questions faster,
- users drill into supplier relationships,
- users run AI enrichment after building graph context,
- users export reports from completed sessions,
- users request new prompts and report templates,
- sales teams return to the product before meetings.

The strongest signal is not a page view. It is a completed account intelligence session that produces a useful saved insight, AI enrichment, or report.

## Operating Principle

The product does not evolve only from assumptions.

It evolves from the questions salespeople ask, the paths they actually take, and the moments where the tool fails to help them move to the next step.
