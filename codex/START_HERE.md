# START HERE - Codex Catalogo Elesole

Questo e il punto di partenza per Codex.

Prima di modificare codice, scraper, parser, mapping o file Odoo, leggere nell'ordine:

1. `codex/context/CATALOG_ELESOLE_CONTEXT_PACK.md`
2. `codex/context/FILE_PLACEMENT_MANIFEST.md`
3. `docs/PROJECT_MEMORY.md`
4. `docs/WORKFLOW.md`
5. `docs/IMPORT_RULES_ODOO.md`
6. `docs/DATASET_MASTER_SPEC.md`
7. `codex/prompts/ODOO_EXPORT_SYSTEM_PROMPT.md`
8. `codex/tasks/TEST_PLAN_FOR_CODEX.md`

## Missione immediata

Preparare e testare il flusso Catalogo Elesole:

1. verificare che i template Odoo siano presenti in `reference_templates/odoo/`;
2. leggere le colonne reali dei template;
3. creare uno script di validazione template;
4. verificare che un output generato da Codex abbia esattamente colonne e ordine del template;
5. creare report errori se l'output non e importabile;
6. non generare file Odoo finali senza validazione.

## Regola critica

Il file import Odoo non deve essere inventato.

Codex deve usare i file template come golden master.

Se non trova i template, deve fermarsi e chiedere di caricarli, senza creare un file Odoo a fantasia.

## Primo test consigliato

Costruire un validatore che confronta:

- template Odoo originale;
- file `product_product_elesole_test_odoo.xlsx`, se presente;
- eventuale nuovo export generato.

Il validatore deve controllare:

- nomi colonne;
- ordine colonne;
- fogli presenti;
- colonne extra;
- colonne mancanti;
- righe vuote;
- SKU duplicati;
- campi obbligatori mancanti.
