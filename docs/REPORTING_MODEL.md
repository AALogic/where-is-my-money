# Reporting Model

## Purpose

The reporting layer turns an analysis session into a PDF document.

The report should preserve the path the user took through the product: selected entity, graph exploration, procurement findings, AI enrichment, and final sales interpretation.

See also: [Sample Report Structure](SAMPLE_REPORT_STRUCTURE.md).

## Session-Based Reporting

Reports are generated from the current analysis session.

The report should include only the context relevant to the session focus.

Examples:

- if the session focused on a buyer, the report is buyer-oriented,
- if the session focused on a supplier, the report is supplier-oriented,
- if the session focused on a region or segment, the report is market-oriented.

## Initial Report Type

The first report type is a sales intelligence PDF.

It should summarize:

- selected buyer or segment,
- procurement history,
- top suppliers,
- spend patterns,
- categories and technology signals,
- graph interpretation,
- AI research findings,
- recommended questions,
- suggested next steps.

## Future Report Templates

The reporting system should be template-driven.

Possible future templates:

- buyer intelligence report,
- supplier intelligence report,
- regional market report,
- first-meeting question pack,
- pain-discovery question pack,
- partnership opportunity report,
- competitor footprint report.

## Report Inputs

The report generator should use:

- normalized procurement data,
- graph context,
- user-selected filters,
- AI findings,
- evidence references,
- user notes where available.

## Report Quality

A useful report should be:

- specific to the selected account or segment,
- grounded in procurement history,
- clear about source evidence,
- clear about which statements are facts, hypotheses, and recommendations,
- readable by a salesperson,
- action-oriented,
- suitable for preparation before a meeting.

## Output

PDF is the target export format for the first release.

Other formats such as HTML or Markdown can be useful internally, but PDF is the expected user-facing artifact.
