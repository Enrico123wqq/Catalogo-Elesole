# Primo prompt da incollare in Codex

Copia e incolla questo prompt in Codex quando apri il repository.

---

Leggi prima questi file, senza scrivere codice subito:

- `codex/START_HERE.md`
- `codex/context/CATALOG_ELESOLE_CONTEXT_PACK.md`
- `codex/context/FILE_PLACEMENT_MANIFEST.md`
- `docs/PROJECT_MEMORY.md`
- `docs/WORKFLOW.md`
- `docs/IMPORT_RULES_ODOO.md`
- `docs/DATASET_MASTER_SPEC.md`
- `codex/prompts/ODOO_EXPORT_SYSTEM_PROMPT.md`
- `codex/tasks/TEST_PLAN_FOR_CODEX.md`

Poi fai solo la Fase 0 e la Fase 1 del piano test:

1. Verifica quali file e cartelle sono presenti.
2. Cerca i file Excel in `reference_templates/odoo/` e `reference_templates/enf/`.
3. Classifica i file trovati come template ufficiale, bozza, caso errore, riferimento tecnico o non classificato.
4. Crea lo script `codex/scripts/inspect_excel_templates.py`.
5. Lo script deve leggere fogli, colonne, numero righe e numero colonne dei file Excel.
6. Salva i report in:

```text
output/draft/context_readiness_report.md
output/draft/template_inspection_report.md
output/draft/template_columns.json
output/draft/excel_file_classification.md
```

Non generare ancora nessun file Odoo importabile.

Non fare scraping.

Non modificare i template.

Se mancano i file Excel, fermati e scrivi esattamente quali file devo copiare e in quale cartella.
