---
layout: page
title: LLM Enrichment
---

# LLM-Based RDF Enrichment

This section documents how LLMs (GPT and Gemini) were used to enrich missing knowledge in Wikidata about Formula 1 drivers. Each case below includes:

- The fact checked via SPARQL
- Zero-/Few-shot/CoT prompting
- LLM responses (GPT + Gemini)
- RDF output from both models
- Error analysis
- Final corrected RDF triple

---

## 🏁 Case 1 — Lewis Hamilton joins Scuderia Ferrari (2025)

### ✅ Step 1: SPARQL Check

We queried `wd:Q9673 wdt:P54 ?team` and found **no mention of Ferrari** in the results.

---

### 🤖 Step 2: Zero-shot Prompt

**Prompt:**  
`What Formula 1 team is Lewis Hamilton racing for in the 2025 season?`

---

### 🧠 Step 3: LLM Responses

**Gemini:**  
"**Lewis Hamilton is racing for Ferrari in the 2025 season.** He moved from Mercedes. His contract runs until 2026."

**GPT-4:**  
"**Lewis Hamilton is racing for Scuderia Ferrari.** He replaced Carlos Sainz, now partners with Charles Leclerc."

> ✨ GPT included more detailed narrative and teammate context.

---

### 🧾 Step 4: RDF by LLMs

**Gemini’s RDF (simplified):**

```turtle
wd:Q1731 wdt:P54 wd:Q169898 .
```

- ❌ Wrong Q-ID for Hamilton (should be Q9673)

**GPT’s RDF (structured):**

```turtle
wd:Q9673 p:P54 [
  ps:P54 wd:Q10227 ;
  pq:P580 "2025-01-01"^^xsd:dateTime ;
  pq:P641 wd:Q1142852
] .
```

- ❌ Wrong team Q-ID (`Q10227` ≠ Ferrari), `P641` is okay.

---

### ✅ Step 5: Corrected RDF Triple

```turtle
@prefix wd: <http://www.wikidata.org/entity/> .
@prefix wdt: <http://www.wikidata.org/prop/direct/> .

wd:Q9673 wdt:P54 wd:Q169898 .
```

🧠 This RDF triple was generated after validating LLM facts and fixing both the driver and team IDs.
