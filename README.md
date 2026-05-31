# FreshSite Copilot Product

FreshSite Copilot Product is the product-positioning and agent-capability workspace for the FreshSite Copilot portfolio project.

The original demo started from a fresh-retail siting thesis project. This repository reframes it as a broader product concept:

> A workflow-based agentic copilot for community service and retail site selection, helping users turn fuzzy expansion or planning goals into explainable field-review candidate lists.

## Why This Repo Exists

The public demo already shows a working fresh-retail scenario. This repo answers the upstream product questions:

- Who is the product really for?
- What user pain is large enough beyond the original thesis setting?
- What is the product output, and what should it not claim to decide?
- Which agent capabilities can be reused across domains?
- How can the original fresh-retail scenario become the first adapter, rather than the whole product?

## Current Documents

- [Product Positioning](docs/product-positioning.md)
- [Agent Capability Map](docs/agent-capability-map.md)

## Working Product Definition

FreshSite Copilot is not a fully autonomous site-selection agent. It is a decision copilot:

- The core decision process stays workflow-based for stability and explainability.
- The copilot layer translates user goals into structured decision tasks.
- The system returns priority field-review candidates, not final site decisions.
- The first verified scenario is fresh-retail siting, but the reusable pattern can extend to convenience stores, community canteens, pharmacies, clinics, courier pickup points, and other neighborhood service locations.

## Relationship To The Demo Repo

This repo should not replace the existing demo implementation. It is a separate product-thinking layer used to guide future iterations, portfolio storytelling, and interview framing.
