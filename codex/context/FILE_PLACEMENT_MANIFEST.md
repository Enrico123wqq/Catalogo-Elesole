# File Placement Manifest - Catalogo Elesole

Questo file indica dove devono stare i file per essere letti correttamente da Codex.

---

## 1. File Odoo template

Cartella:

```text
reference_templates/odoo/
```

File attesi:

```text
product_product_template.xls
product_template_template.xlsx
product_category_template.xlsx
product_attribute_template.xlsx
product_attribute_value_template.xlsx
```

File presenti/da classificare:

```text
product_product_elesole_test_odoo.xlsx
nuovo_foglio_lavoro_odoo.xlsx
```

### Regola

I template ufficiali devono essere indicati esplicitamente.

Se un file non e stato approvato come template, non deve essere usato come golden master.

---

## 2. File ENF

Cartella:

```text
reference_templates/enf/
```

File attesi:

```text
Product Database Sample.xlsx
```

### Uso corretto

ENF serve per:

- analisi tecnica;
- confronto attributi;
- arricchimento prodotto;
- comprensione campi fotovoltaici.

### Uso scorretto

ENF non deve essere usato come template Odoo.

---

## 3. Dataset grezzi da Apify

Cartella:

```text
output/draft/apify_raw/
```

File consigliati:

```text
universal_capture_sample.json
universal_capture_full.json
crawl_summary.md
errors.csv
```

Se la cartella non esiste, Codex puo crearla.

---

## 4. Output Parser / Field Discovery

Cartella:

```text
output/validated/field_discovery/
```

File previsti:

```text
field_inventory.json
field_inventory.csv
report_field_discovery.md
```

---

## 5. Dataset Master

Cartella:

```text
output/validated/dataset_master/
```

File previsti:

```text
dataset_master_elesole.xlsx
dataset_master_elesole.csv
dataset_master_elesole.json
quality_report.xlsx
mapping_errors.xlsx
```

---

## 6. File import Odoo finali

Cartella:

```text
output/odoo_import/
```

File previsti:

```text
odoo_import_categories.xlsx
odoo_import_attributes.xlsx
odoo_import_attribute_values.xlsx
odoo_import_products.xlsx
odoo_import_product_variants.xlsx
```

Questi file devono essere generati solo dopo validazione.

---

## 7. Script Codex

Cartella:

```text
codex/scripts/
```

Script consigliati:

```text
inspect_excel_templates.py
validate_odoo_import.py
compare_excel_structure.py
build_field_inventory.py
build_dataset_master.py
export_odoo_from_master.py
```

---

## 8. Test Codex

Cartella:

```text
codex/tests/
```

Test consigliati:

```text
test_template_structure.py
test_odoo_export_validation.py
test_dataset_master_schema.py
test_field_discovery.py
```

---

## 9. Regola per file grandi

I dataset molto grandi e gli output pesanti non devono essere trattati come template.

Possono stare in:

```text
output/
archive/
```

ma i template ufficiali devono restare solo in:

```text
reference_templates/
```

---

## 10. Primo controllo che Codex deve eseguire

Prima di fare qualsiasi test, Codex deve verificare l'esistenza di:

```text
reference_templates/odoo/
reference_templates/enf/
docs/IMPORT_RULES_ODOO.md
docs/PROJECT_MEMORY.md
codex/START_HERE.md
```

Poi deve elencare i file Excel trovati e classificare:

- template ufficiale;
- bozza;
- caso errore;
- riferimento tecnico;
- file non classificato.
