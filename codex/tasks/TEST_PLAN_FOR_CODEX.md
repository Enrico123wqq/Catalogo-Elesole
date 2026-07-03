# Test Plan per Codex - Catalogo Elesole

Questo piano serve per procedere in modo controllato, evitando che Codex generi file Odoo non importabili.

---

## Fase 0 - Lettura contesto

Codex deve leggere:

```text
codex/START_HERE.md
codex/context/CATALOG_ELESOLE_CONTEXT_PACK.md
codex/context/FILE_PLACEMENT_MANIFEST.md
docs/PROJECT_MEMORY.md
docs/WORKFLOW.md
docs/IMPORT_RULES_ODOO.md
docs/DATASET_MASTER_SPEC.md
codex/prompts/ODOO_EXPORT_SYSTEM_PROMPT.md
```

Output richiesto:

```text
output/draft/context_readiness_report.md
```

Il report deve dire:

- file letti;
- file mancanti;
- template Excel trovati;
- blocchi che impediscono i test.

---

## Fase 1 - Ispezione template Excel

Creare script:

```text
codex/scripts/inspect_excel_templates.py
```

Lo script deve:

- cercare file Excel in `reference_templates/odoo/`;
- aprire ogni file;
- elencare fogli;
- elencare colonne per foglio;
- contare righe e colonne;
- salvare report.

Output:

```text
output/draft/template_inspection_report.md
output/draft/template_columns.json
```

---

## Fase 2 - Classificazione file Excel

Codex deve classificare i file in:

- template ufficiale;
- bozza;
- caso errore;
- riferimento tecnico;
- non classificato.

Regola:

`product_product_elesole_test_odoo.xlsx` e un caso errore finche non viene dimostrato importabile.

Output:

```text
output/draft/excel_file_classification.md
```

---

## Fase 3 - Validatore struttura Odoo

Creare script:

```text
codex/scripts/validate_odoo_import.py
```

Lo script deve ricevere:

- template ufficiale;
- file da validare;
- nome foglio opzionale.

Controlli obbligatori:

- stessi fogli o foglio corretto;
- stesso ordine colonne;
- nessuna colonna extra;
- nessuna colonna mancante;
- righe completamente vuote;
- Internal Reference duplicati, se colonna presente;
- External ID duplicati, se colonna presente;
- campi obbligatori vuoti, se definiti.

Output:

```text
output/validated/import_quality_report.xlsx
output/validated/import_quality_report.md
```

---

## Fase 4 - Test sul file errato

Usare il validatore su:

```text
reference_templates/odoo/product_product_elesole_test_odoo.xlsx
```

Confrontandolo con il template ufficiale Odoo prodotto.

Obiettivo:

- dimostrare perche non e importabile;
- produrre report leggibile;
- non modificarlo direttamente.

Output:

```text
output/validated/product_product_elesole_test_validation_report.md
```

---

## Fase 5 - Mini Dataset Master di prova

Creare un piccolo dataset di test manuale con 3 prodotti fittizi ma realistici:

1. modulo fotovoltaico;
2. inverter;
3. batteria.

File:

```text
output/draft/sample_dataset_master.csv
output/draft/sample_dataset_master.json
```

Campi minimi:

```text
elesole_product_id
internal_reference
source_name
source_url
source_sku
brand_raw
brand_normalized
product_name_raw
product_name_normalized
master_category
source_category
source_price_public
supplier_cost
currency
availability
technical_attributes
image_urls
document_urls
quality_status
raw_source_data
```

---

## Fase 6 - Export Odoo da mini Dataset Master

Creare script:

```text
codex/scripts/export_odoo_from_master.py
```

Lo script deve:

- leggere il Dataset Master;
- leggere il template Odoo;
- applicare mapping minimo;
- produrre file Odoo con stessa struttura del template;
- validare subito l'output;
- salvare report.

Output:

```text
output/odoo_import/odoo_import_products_test.xlsx
output/validated/odoo_import_products_test_report.md
```

---

## Fase 7 - Stop prima dello scraping completo

Non procedere allo scraping completo finche:

- il validatore non funziona;
- il mini export non rispetta il template;
- il report qualita non e chiaro;
- i template ufficiali non sono stati approvati.

---

## Definizione di successo

Il test e riuscito quando:

1. Codex legge i template.
2. Codex identifica correttamente colonne e fogli.
3. Codex segnala perche il vecchio file non e importabile.
4. Codex crea un mini export con struttura identica al template.
5. Il validatore conferma che il mini export e strutturalmente compatibile.

Solo dopo si puo passare al parser e allo scraper finale.
