# Secondo prompt Codex - Validazione Odoo

Usa questo prompt solo dopo aver completato il primo prompt e dopo aver verificato che i template Excel siano presenti.

---

Ora esegui la Fase 3 e Fase 4 del piano test.

Obiettivo: costruire un validatore dei file import Odoo.

Leggi:

- `docs/IMPORT_RULES_ODOO.md`
- `codex/prompts/ODOO_EXPORT_SYSTEM_PROMPT.md`
- `codex/tasks/TEST_PLAN_FOR_CODEX.md`
- `output/draft/template_columns.json`
- `output/draft/excel_file_classification.md`

Poi crea:

```text
codex/scripts/validate_odoo_import.py
```

Lo script deve confrontare un file da validare contro un template ufficiale.

Controlli richiesti:

1. fogli presenti;
2. colonne presenti;
3. ordine colonne;
4. colonne mancanti;
5. colonne extra;
6. righe completamente vuote;
7. duplicati Internal Reference, se la colonna esiste;
8. duplicati External ID, se la colonna esiste;
9. celle obbligatorie vuote, se le colonne obbligatorie sono definite.

Poi testa il file:

```text
reference_templates/odoo/product_product_elesole_test_odoo.xlsx
```

contro il template Odoo prodotto corretto.

Output richiesti:

```text
output/validated/import_quality_report.md
output/validated/product_product_elesole_test_validation_report.md
```

Non correggere ancora il file.

Non generare ancora il nuovo export.

Il risultato deve spiegare chiaramente perche il file non e importabile o quali problemi ha.
