# Catalogo Elesole

Repository operativo per la costruzione del Dataset Master Elesole, la raccolta dati da fornitori/e-commerce, la normalizzazione dei cataloghi e la preparazione dei file di importazione Odoo.

## Obiettivo

Costruire un flusso stabile e controllabile per trasformare dati prodotto grezzi in file importabili su Odoo, senza lasciare a Codex il compito di inventare strutture di importazione.

## Principio fondamentale

- **Dataset Master Elesole**: contiene tutti i dati raccolti, normalizzati, arricchiti e tracciabili.
- **File import Odoo**: contiene solo i campi accettati da Odoo, nello stesso formato dei template ufficiali.
- **Template ufficiali**: sono i golden master. Codex deve copiarne struttura, colonne e ordine.
- **Report qualità**: ogni errore o dato non importabile va fuori dal file Odoo e dentro un report separato.

## Struttura repository

```text
Catalogo-Elesole/
├── docs/
├── reference_templates/
├── schemas/
├── mappings/
├── apify/
├── codex/
├── output/
└── archive/
```

## Flusso sintetico

1. Universal Capture: raccolta dati grezzi completa.
2. Parser / Field Discovery: analisi dei campi realmente presenti.
3. Dataset Master: normalizzazione e arricchimento.
4. Export Odoo: creazione file stretti, identici ai template.
5. Quality Check: validazione prima dell'importazione.

## Regola per Codex

Codex non deve mai generare file import Odoo inventando colonne. Deve sempre leggere i template in `reference_templates/odoo/` e validare l'output prima di salvarlo.
