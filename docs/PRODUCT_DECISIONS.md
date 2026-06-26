# Product Decisions

This document captures the main product decisions behind **Where is my money?**.

The point is not to record every implementation detail. The point is to show what was deliberately chosen, what was rejected for now, and what trade-off came with each choice.

## 1. Start With Buyer-Centric Analysis

**Decision:** the first workflow starts from a buyer NIP.

Salespeople usually prepare around an account, not an abstract market. Starting from the buyer gives the product a concrete job: show what this entity buys, who wins, how money flows to suppliers, and whether the account looks open, crowded, or locked.

Supplier-first and segment-first workflows still matter, but buyer-first gives the clearest first path through the product.

## 2. Use Network Intelligence Instead Of Tender Search Alone

**Decision:** the product focuses on relationship intelligence, not generic tender search.

Tender search answers what happened. Network intelligence asks what the pattern means.

That difference matters. A table can rank suppliers, but the graph makes repeated relationships easier to see: the same buyer, the same supplier, the same category, similar values, repeated over time.

The trade-off is that the product needs both surfaces. Tables stay for precision. The graph becomes the place where the user reads the market.

## 3. Treat Atlas Przetargow As The First Working Data Layer

**Decision:** Atlas Przetargow is the first operational data layer.

Atlas already aggregates and normalizes Polish public procurement data from BZP and TED. Starting there makes the first release practical.

The trade-off is dependency. The product cannot assume Atlas will always be the only source, so BZP and TED remain fallback and verification layers in the architecture.

## 4. Keep AI As An Enrichment Layer

**Decision:** AI enriches the current graph and session context. It does not replace the procurement data layer.

The best prompt is the one that starts from the user's current board: buyer, suppliers, tenders, categories, values, and visible relationships.

This avoids generic AI chat. The AI layer has a job: answer a focused research prompt against the current context and return findings that can be used in the session.

## 5. Preserve Trust Boundaries

**Decision:** procurement facts, calculated metrics, external findings, hypotheses, and recommendations stay separate.

This is one of the most important product decisions.

The product supports sales decisions, so it cannot blur an official procurement record with an AI interpretation. A user should always know what is a source fact, what is calculated, what came from web research, and what is only a hypothesis.

The trade-off is more structure in the product, but that structure protects trust.

## 6. Make Reports Session-Based

**Decision:** reports are generated from the analysis session.

A report should preserve what the user actually explored: selected buyer, graph state, supplier context, AI findings, evidence, and conclusions.

This is more useful than a generic report generator because the output follows the user's path through the problem.

## 7. Use Product Analytics To Drive The Roadmap

**Decision:** the product tracks user actions and friction points in a privacy-aware way.

The team needs to know where users start, which graph layers create insight, which prompts lead to saved findings, which reports are generated, and where users stop before reaching value.

This adds product operations work, but it creates a better feedback loop than relying only on opinions.

## 8. Keep The Repository Documentation-Only

**Decision:** this repository documents the product concept and does not expose production code.

The goal is to communicate product thinking, system logic, data flow, and product direction without publishing internal implementation details.

That means the repository should be evaluated as product thinking and product architecture, not as a software implementation.
