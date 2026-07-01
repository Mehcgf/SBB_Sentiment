# SBB Trustpilot Sentiment Analysis

Dieses Projekt analysiert Kundenbewertungen der SBB (Schweizerische Bundesbahnen) von Trustpilot und klassifiziert diese automatisch in positiv, negativ und neutral — mit anschließender Keyword- und Wortpaar-Analyse.

## Projektziel

Kundenfeedback manuell auswerten kostet Zeit. Ziel war es, eine automatisierte NLP-Pipeline zu bauen die Bewertungen klassifiziert, häufige Beschwerdethemen identifiziert und Wortmuster erkennt — ohne einen einzigen Review manuell lesen zu müssen.

## Datenbasis

70 echte Trustpilot-Bewertungen der SBB, gesammelt über die Chrome Extension "T-Reviews Scraper" und in einem automatisierten Merge-Script dedupliziert.

**Hinweis:** Trustpilot blockiert automatisiertes Scraping aktiv (403 auch mit Browser-Headers). Die Daten wurden daher manuell über die Extension gesammelt — ein realistisches Szenario aus der Praxis.

## Methode

- Daten-Merging: 8 einzelne CSV-Exporte → 1 deduplizierter Datensatz
- Preprocessing: Spaltenreduktion, Null-Check, Textreinigung
- Sentiment-Klassifikation: `oliverguhr/german-sentiment-bert` via HuggingFace Transformers
- Keyword-Analyse: Häufigste Einzelwörter in negativen Bewertungen
- Bigramm-Analyse: Häufigste Wortpaare — zeigt welche Themen zusammen auftreten

## Ergebnisse

| Sentiment | Anzahl | Anteil |
|---|---|---|
| Negativ | 62 | 89% |
| Positiv | 5 | 7% |
| Neutral | 3 | 4% |

**Top Beschwerdethemen:** App, Ticket, Preiserhöhungen ("jedes Jahr steigen"), Klimaanlage, fehlende Entschuldigungen

**Stärkstes Wortpaar:** "immer wieder" (5x) — zeigt strukturelle Frustration über sich wiederholende Probleme

## Tools & Libraries

- Python 3.12
- pandas, numpy
- transformers (HuggingFace)
- matplotlib
- collections, re
