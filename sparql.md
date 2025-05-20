---
layout: page
title: SPARQL Queries
---

# SPARQL Queries Used in This Project

In this section we present the queries used to explore Wikidata and identify missing or incomplete information about Formula 1 drivers.

---

## 1. Driver Lookup by Name

This query searches for Formula 1 drivers whose names include "Hamilton", "Leclerc", "Antonelli", or "Verstappen".  
It uses `FILTER` and `REGEX` to perform case-insensitive matching, and `DISTINCT` with `LIMIT` to keep the output clean.  
It helped us locate the correct Q-IDs and confirm the presence of these drivers in Wikidata.

```sparql
SELECT DISTINCT ?driver ?driverLabel
WHERE {
  ?driver wdt:P106 wd:Q10841764 .
  ?driver rdfs:label ?driverLabel .
  FILTER(LANG(?driverLabel) = "en") .
  FILTER(
    REGEX(?driverLabel, "Hamilton", "i") ||
    REGEX(?driverLabel, "Verstappen", "i") ||
    REGEX(?driverLabel, "Leclerc", "i") ||
    REGEX(?driverLabel, "Antonelli", "i")
  )
}
LIMIT 10
```

---

## 2. Nationality or Team (UNION Query)

This query retrieves either the citizenship (`P27`) or the team (`P54`) for each selected driver.  
It uses the `UNION` keyword to combine both properties in a single result set.  
This allowed us to verify that some expected team affiliations (e.g., Hamilton–Ferrari, Antonelli–Mercedes) were missing.

```sparql
SELECT DISTINCT ?driver ?driverLabel ?infoLabel
WHERE {
  VALUES ?driver {
    wd:Q9673 wd:Q17541912 wd:Q112073790 wd:Q2239218
  }

  {
    ?driver wdt:P27 ?info .
  }
  UNION
  {
    ?driver wdt:P54 ?info .
  }

  SERVICE wikibase:label { bd:serviceParam wikibase:language "en". }
}
ORDER BY ?driverLabel
```

---

## 3. Championships Won by Drivers

This query checks which major competitions each driver has won, focusing on the Formula One World Championship (`P2522`).  
The results clearly showed that Max Verstappen is listed as champion in 2021–2023, but not in 2024 — an omission that became a key enrichment point.

```sparql
SELECT ?driver ?driverLabel ?competitionLabel
WHERE {
  VALUES ?driver {
    wd:Q9673 wd:Q17541912 wd:Q112073790 wd:Q2239218
  }

  ?driver wdt:P2522 ?competition .

  SERVICE wikibase:label { bd:serviceParam wikibase:language "en". }
}
ORDER BY ?driverLabel
```

---

## 4. Unmarried Partners

This query examines whether drivers have a recorded partner using `P451` (unmarried partner).  
It uses `OPTIONAL` to ensure drivers without a recorded relationship are still included in the results.  
Only Max Verstappen and Lewis Hamilton are linked to partners (Kelly Piquet, Nicole Scherzinger), while others like Charles Leclerc have no partner listed — despite known relationships.

```sparql
SELECT ?driver ?driverLabel ?partner ?partnerLabel
WHERE {
  VALUES ?driver {
    wd:Q9673 wd:Q17541912 wd:Q112073790 wd:Q2239218
  }

  OPTIONAL { ?driver wdt:P451 ?partner . }

  SERVICE wikibase:label { bd:serviceParam wikibase:language "en". }
}
ORDER BY ?driverLabel
```
