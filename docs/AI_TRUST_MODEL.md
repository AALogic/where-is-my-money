# AI Trust Model

## Purpose

The AI layer should make the analysis more useful without making the product less trustworthy.

Procurement records, public web findings, AI hypotheses, and recommendations must stay distinguishable.

## Claim Types

### Procurement Fact

A fact coming from structured procurement data.

Examples:

- buyer issued a notice,
- supplier won a result notice,
- tender had a known value,
- CPV code appeared in a record.

### Derived Metric

A calculation based on procurement facts.

Examples:

- top suppliers by wins,
- spend by year,
- supplier concentration,
- category share.

### External Web Finding

A finding from public internet research.

Examples:

- supplier website lists a vendor partnership,
- public job posting suggests hiring for a technology,
- public case study describes a capability.

### Hypothesis

An interpretation based on data patterns or external findings.

Examples:

- supplier may be embedded in the account,
- buyer may have recurring demand in a category,
- partnership angle may be plausible.

### Recommendation

A suggested sales action.

Examples:

- ask about renewal cycle,
- explore partnership with supplier,
- prepare cybersecurity-specific value proposition.

## Trust Labels

The product should use clear labels:

- `source fact`
- `calculated metric`
- `sourced web finding`
- `hypothesis`
- `recommendation`

These labels make it clear what kind of statement the user is reading.

## Evidence Rules

AI-generated external claims should be able to include:

- source URL,
- source title,
- retrieval date,
- short evidence excerpt or summary,
- relation to the selected buyer, supplier, tender, or graph node,
- limitation note where needed.

## Guardrails

- AI findings should not overwrite procurement facts.
- AI recommendations should not be presented as verified facts.
- Reports should keep evidence and limitations visible.
- Prompt definitions should specify whether evidence is required.
- The user should be able to distinguish data-backed conclusions from exploratory hypotheses.

## Example Finding

```json
{
  "type": "hypothesis",
  "subject": "Supplier Alpha",
  "claim": "Supplier Alpha may be a partnership candidate for cybersecurity opportunities rather than a direct competitor.",
  "basis": [
    "Procurement graph shows recurring managed services wins.",
    "No visible cybersecurity-specific awards in the selected buyer history.",
    "Public website describes infrastructure support services."
  ],
  "evidence": [
    {
      "source_url": "https://example.com",
      "source_type": "supplier_website",
      "retrieved_at": "analysis_time"
    }
  ],
  "limitation": "This requires human validation before being used as a sales strategy."
}
```

## Reporting Rule

Reports should group conclusions by trust level.

Recommended report order:

1. procurement facts,
2. derived metrics,
3. sourced web findings,
4. hypotheses,
5. recommendations.
