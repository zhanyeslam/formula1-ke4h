---
layout: page
title: LLM Enrichment
---

# LLM-Based RDF Enrichment

This section presents the RDF triples that were generated using large language models (GPT and Gemini)  
to enrich Formula 1 driver data in Wikidata. Each triple corresponds to information that was missing  
in the original dataset and was confirmed and structured based on AI-generated responses.

---

## Enrichment 1 — Lewis Hamilton joins Ferrari (2025)

**SPARQL confirmed** that Lewis Hamilton was not listed as a Ferrari driver.  
**LLMs returned** Ferrari as his 2025 team.  
**RDF triple:**

```turtle
wd:Q9673 wdt:P54 wd:Q169898 .
```

---

## Enrichment 2 — Kimi Antonelli joins Mercedes (2025)

**SPARQL showed** Antonelli had no team.  
**LLMs confirmed** he races for Mercedes in 2025.  
**RDF triple:**

```turtle
wd:Q112073790 wdt:P54 wd:Q172721 .
```

---

## Enrichment 3 — Verstappen wins 2024 F1 Championship

**SPARQL confirmed** there was no record of a 2024 title.  
**LLMs responded** Verstappen won it with Red Bull.  
**RDF triple:**

```turtle
wd:Q2239218 wdt:P2522 wd:Q113628886 .
```

---

## Enrichment 4 — Leclerc's relationship with Alexandra Saint Mleux

**SPARQL showed** no partner listed for Charles Leclerc.  
**LLMs returned** Alexandra Saint Mleux as his current partner since 2023.  
**RDF triple:**

```turtle
wd:Q17541912 p:P451 [
  ps:P451 wd:Q134520230 ;
  pq:P580 "2023-01-01"^^xsd:date
] .
```
