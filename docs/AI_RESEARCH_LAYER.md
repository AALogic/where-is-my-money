# AI Research Layer

## Purpose

The AI research layer enriches the current procurement analysis with public web context.

It does not replace the procurement data layer. It starts after the user has built a board worth asking questions about.

See also: [AI Trust Model](AI_TRUST_MODEL.md).

## Core Principle

The AI does not start from an empty prompt.

It receives the current analysis context:

- selected buyer,
- selected supplier,
- visible graph nodes,
- visible relationships,
- tender history,
- categories and technology signals,
- values and time ranges,
- selected research prompt.

That context changes the quality of the answer. The question is no longer "research this company". It becomes "given this buyer-supplier-money pattern, what public context changes the sales interpretation?"

## Prompt-Driven Design

Research tasks are defined by creator-provided prompts.

A prompt defines the research goal, allowed source types, evidence expectations, output format, trust label, and whether the finding can enter the final report.

This keeps the system extensible. New research tasks can be added without turning the product into generic chat.

## Example Research Directions

Depending on the prompt, AI research can investigate supplier websites, vendor partnerships, public job postings, product pages, case studies, technology specialization, market positioning, and public people or role signals.

## Finding Types

AI output is stored as session findings.

Useful finding types:

- fact from procurement data,
- external web finding,
- hypothesis,
- sales question,
- risk signal,
- partnership signal,
- next-step recommendation.

## Context Injection Into API Request

When the user runs a prompt, the application packages the current board context into the AI request.

Conceptually:

```text
prompt definition
+ selected graph context
+ procurement summaries
+ user question
+ required output rules
+ evidence requirements
= AI research task
```

The response returns to the same analysis session and can later be used by the report generator.

## Example Context Package

```json
{
  "session_focus": "buyer",
  "selected_buyer": {
    "name": "Public Entity A",
    "nip": "buyer_nip",
    "region": "region_code"
  },
  "visible_graph": {
    "active_layer": "cash_flow",
    "top_suppliers": [
      {
        "name": "Supplier Alpha",
        "wins": 8,
        "value_pln": 4800000,
        "top_categories": ["managed services", "support"]
      }
    ]
  },
  "prompt": {
    "id": "supplier_partnership_scan",
    "goal": "Identify which suppliers may be partnership candidates rather than direct competitors.",
    "required_output": ["findings", "hypotheses", "questions", "evidence"]
  }
}
```

## Evidence Model

The prompt decides how strict the evidence requirement is. The product still stores evidence from the beginning.

An enriched finding may include:

- source URL,
- source title,
- retrieval date,
- short evidence excerpt or summary,
- confidence or limitation note,
- relation to buyer, supplier, tender, category, or graph node.

## Product Behavior

AI research is useful only if it changes the salesperson's next move.

Good output helps answer:

- what should I ask this buyer,
- what pain or gap may exist,
- which supplier may be a partner,
- which competitor is already embedded,
- what angle should I use in the first conversation.

## Trust Boundary

AI enrichment is stored separately from procurement facts.

The product preserves whether an output is a source fact, external web finding, hypothesis, or recommendation. This prevents AI-generated interpretation from being confused with official procurement data.
