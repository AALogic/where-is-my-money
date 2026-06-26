# Core User Journey

## Starting Point

The first high-value journey starts from a public buyer.

The salesperson enters a buyer NIP because they are preparing for an account conversation and need a fast read on the buyer's procurement behavior.

They are trying to answer:

- what does this buyer buy,
- who wins,
- how often,
- at what value,
- in which categories,
- and whether the relationships have changed over time.

## Journey Steps

### 1. Enter Buyer NIP

The user starts with a known public entity.

```text
Input: buyer NIP
Intent: understand the buyer's historical procurement behavior
```

This is intentionally concrete. The NIP gives the product a cleaner starting point than fuzzy name search.

### 2. Build Buyer Profile

The product loads and normalizes procurement records for that buyer.

The profile gives the user a first account read:

- total notice activity,
- result notices,
- spend by time period where values are available,
- most frequent suppliers,
- most valuable suppliers,
- common categories,
- visible technology or product areas,
- recent activity.

One important detail: raw notices, procedures, results, and supplier wins are not the same metric. The profile keeps them separate because mixing them would create a false sense of precision.

### 3. Show Cash-Flow Relationships

The graph turns the buyer profile into a relationship map.

The first business-readable relationship is:

```text
buyer -> supplier -> tender -> product/category -> value
```

At this moment the salesperson can see whether the account is dominated by a few suppliers or spread across many vendors.

### 4. Explore Supplier Context

The user clicks into a supplier.

The product shows what that supplier delivers, where else they win, how concentrated their activity is, and whether they overlap with the user's offer.

This is where the question changes from "who won?" to "are they a competitor, a blocker, or someone worth partnering with?"

### 5. Expand To Region

The user moves from one buyer to a regional view.

The regional view answers:

- which buyers spend the most,
- which suppliers win most often,
- which categories dominate,
- where the market looks crowded,
- where similar opportunities may exist.

### 6. Expand To Segment

The user then explores the broader IT segment.

This may include CPV and keyword-based views for software, infrastructure, cybersecurity, service desk, cloud, hardware, maintenance, and related categories.

### 7. Enrich With AI Research

The user sends the current board to the AI research layer.

The AI receives selected buyer, visible suppliers, tender history, categories, values, and relationship patterns. It does not start from a blank page.

The selected prompt decides what the agent researches and what evidence it needs to return.

### 8. Generate Report

At the end of the session, the user exports a PDF report.

The report follows the path of the analysis. If the session focused on one buyer, the output is a buyer intelligence report. If the user moved into supplier or regional context, the report reflects that.

## Outcome

After a successful session, the salesperson leaves with a better next move:

- who already sells into the account,
- what the buyer has been purchasing,
- whether the relationship network is concentrated or fragmented,
- which suppliers may block, compete, or partner,
- what to ask in the first meeting,
- what sales strategy is most plausible.
