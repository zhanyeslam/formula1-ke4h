---
layout: page
title: Methodology
---

# Methodology

This project uses a data-driven approach to explore and improve the quality of Formula 1 driver data in Wikidata. 
We use SPARQL queries to retrieve real data for selected drivers.  
By inspecting the output, we observe when specific values such as team membership, relationship data, or recent titles are not present.

When a relevant fact is missing in Wikidata, we consider it a candidate for enrichment.  
To fill the gap, we use large language models (LLMs) such as GPT-4 and Gemini to retrieve the most accurate, contextual information.  
We then convert that information into structured RDF triples using the Wikidata ontology format.

---

## How SPARQL Was Used

We used SPARQL not only as a technical requirement, but as an exploratory tool to verify what is present in Wikidata and what is not.

Each query in the project serves a real purpose:

- **Driver Lookup by Name**: Confirmed existence of target drivers using `FILTER`, `REGEX`, and `LIMIT`.
- **Nationality or Team**: Used `UNION` to extract basic properties for comparison.
- **Championship Wins**: Retrieved historical wins (`P2522`) and showed missing 2024 win.
- **Unmarried Partner**: Used `OPTIONAL` to verify whether drivers have known partners listed.

All six required SPARQL keywords (`FILTER`, `REGEX`, `UNION`, `OPTIONAL`, `DISTINCT`, `LIMIT`) were applied in meaningful, task-driven queries.

---

## Summary

This methodology allowed us to find meaningful gaps directly from the data itself — not through assumptions — and address them through targeted AI-generated enrichment.  
Every enrichment step is documented with the original SPARQL, the LLM prompt and response, and the resulting RDF triple.
