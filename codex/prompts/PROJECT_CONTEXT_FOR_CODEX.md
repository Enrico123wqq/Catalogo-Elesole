# Contesto progetto per Codex - Catalogo Elesole

Questo file deve essere letto da Codex prima di lavorare su scraping, parser, Dataset Master o export Odoo.

## Missione

Costruire un sistema stabile per raccogliere cataloghi fornitori, normalizzarli nel Dataset Master Elesole e generare file importabili su Odoo.

## Regola principale

Non generare file Odoo a fantasia.

I file Odoo devono essere identici ai template in:

```text
reference_templates/odoo/
```

per:

- nomi colonne;
- ordine colonne;
- fogli;
- formato.

## Workflow obbligatorio

1. Universal Capture: raccogliere dati grezzi completi.
2. Parser / Field Discovery: capire tutti i campi realmente presenti.
3. Dataset Master: normalizzare e arricchire.
4. Mapping: applicare regole verso Odoo.
5. Export Odoo: creare file separati, stretti, validati.
6. Quality Report: segnalare errori, dati mancanti, campi non mappati.

## File da leggere sempre

- `docs/PROJECT_MEMORY.md`
- `docs/WORKFLOW.md`
- `docs/IMPORT_RULES_ODOO.md`
- `docs/DATASET_MASTER_SPEC.md`
- `codex/prompts/ODOO_EXPORT_SYSTEM_PROMPT.md`

## Separazione corretta

Dataset Master:

- puo contenere tutto;
- include raw data;
- include technical attributes;
- include media e documenti;
- include dati non ancora importabili.

Odoo import:

- contiene solo cio che Odoo accetta;
- segue template ufficiale;
- non contiene fogli tecnici extra;
- non contiene colonne inventate;
- non forza dati incompatibili.

## Oggetti Odoo da gestire separatamente

- categorie;
- attributi;
- valori attributo;
- prodotti template;
- varianti prodotto;
- immagini/media, se gestite via import separato;
- report errori.

## Validazioni obbligatorie

Prima di produrre un file finale:

- confronta colonne con template;
- controlla ordine colonne;
- controlla SKU/Internal Reference univoci;
- controlla External ID univoci;
- controlla categorie;
- controlla attributi;
- controlla valori numerici;
- controlla righe vuote;
- genera report qualita.

Se la validazione fallisce, non produrre il file finale importabile.

## Primo fornitore target

Solar Energy Point.

Usare Apify per scraping e Codex per parser, normalizzazione, mapping ed export.

## Nota pratica

I file ENF sono utili per analisi tecnica e confronto campi prodotto.

Non usare ENF come template import Odoo.
