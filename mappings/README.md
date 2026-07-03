# Mapping Catalogo Elesole

Questa cartella contiene le regole di trasformazione tra sorgente, Dataset Master e Odoo.

## File consigliati

- `sep_to_master.xlsx`: mapping da Solar Energy Point a Dataset Master.
- `master_to_odoo.xlsx`: mapping da Dataset Master a file import Odoo.
- `category_rules.xlsx`: regole categorie e sottocategorie.
- `attribute_rules.xlsx`: regole attributi e valori attributo.

## Regola

Codex deve usare questi mapping prima di generare file Odoo.

Se un campo non e mappato, non deve essere forzato nel file import finale. Deve essere segnalato nel report errori.
