# Template Odoo ufficiali

Questa cartella deve contenere i template ufficiali di importazione Odoo.

## File da inserire manualmente

Copia qui dal tuo PC i file modello Odoo, ad esempio:

```text
product_product_template.xls
product_template_template.xlsx
product_category_template.xlsx
product_attribute_template.xlsx
product_attribute_value_template.xlsx
product_product_elesole_test_odoo.xlsx
```

## Regola per Codex

Codex deve sempre usare questi file come riferimento strutturale.

Quando genera un file import Odoo deve:

1. aprire il template corrispondente;
2. copiare foglio, colonne e ordine colonne;
3. compilare solo i valori compatibili;
4. non aggiungere colonne extra;
5. non aggiungere fogli extra;
6. validare il risultato prima dell'export.

## Nota importante

Il file `product_product_elesole_test_odoo.xlsx`, se non importabile, deve essere considerato esempio di errore o bozza, non template definitivo, finche non viene approvato.
