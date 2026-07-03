# Regole import Odoo - Catalogo Elesole

Questo documento è la regola ufficiale per generare file importabili su Odoo.

## Principio principale

Codex non deve inventare la struttura dei file Odoo.

Ogni file import deve essere generato partendo dai template presenti in:

```text
reference_templates/odoo/
```

I template sono golden master.

## Regole assolute

1. I nomi colonna devono essere identici al template ufficiale.
2. L'ordine delle colonne deve essere identico.
3. Non aggiungere colonne extra.
4. Non rimuovere colonne presenti nel template.
5. Non aggiungere fogli di lavoro tecnici nel file import finale.
6. Non inserire note, controlli o mapping nel file Odoo finale.
7. Se un dato manca, lasciare la cella vuota oppure inserirlo nel report errori se obbligatorio.
8. Se un dato non è compatibile con Odoo, non forzarlo.
9. I file di controllo qualità devono essere separati.
10. Prima dell'export finale deve essere eseguita una validazione automatica.

## Separazione dei file

I file finali devono essere separati per oggetto Odoo.

Output consigliati:

```text
output/odoo_import/odoo_import_categories.xlsx
output/odoo_import/odoo_import_attributes.xlsx
output/odoo_import/odoo_import_attribute_values.xlsx
output/odoo_import/odoo_import_products.xlsx
output/odoo_import/odoo_import_product_variants.xlsx
```

File non importabili ma necessari:

```text
output/validated/dataset_master_elesole.xlsx
output/validated/technical_attributes_long_format.xlsx
output/validated/media_documents.xlsx
output/validated/import_quality_report.xlsx
output/validated/mapping_errors.xlsx
```

## Dataset Master vs Odoo Import

### Dataset Master Elesole

Puo contenere molti campi:

- dati sorgente;
- HTML o raw data;
- descrizioni estese;
- attributi tecnici;
- immagini;
- PDF;
- categorie sorgente;
- categorie normalizzate;
- brand;
- costi;
- prezzi;
- stato qualita;
- note interne.

### File import Odoo

Deve contenere solo i campi accettati dal template.

Non tutto cio che sta nel Dataset Master va in Odoo.

## Validazioni obbligatorie

Prima di salvare un file import Odoo, Codex deve controllare:

- esistenza del template;
- nomi colonne identici;
- ordine colonne identico;
- nessuna colonna extra;
- nessuna colonna mancante;
- SKU/Internal Reference univoco;
- External ID univoco;
- categorie valorizzate secondo regole Elesole;
- attributi coerenti;
- prezzi numerici;
- campi obbligatori non vuoti;
- valori booleani compatibili;
- encoding caratteri compatibile con Excel/Odoo;
- assenza di righe completamente vuote.

## Categorie

Le categorie devono essere importate prima dei prodotti.

La struttura categoria deve essere gestita con un file dedicato.

Non creare categorie nuove dentro il file prodotti se non sono state approvate.

## Attributi e varianti

Gli attributi devono essere creati prima dei prodotti con varianti.

Ordine corretto:

1. categorie;
2. attributi;
3. valori attributo;
4. prodotti template;
5. varianti prodotto, se necessarie.

## SKU / Internal Reference

Ogni prodotto deve avere un Internal Reference univoco Elesole.

Il codice sorgente del fornitore non deve essere usato automaticamente come SKU Elesole definitivo senza regola approvata.

## External ID

Ogni record importabile deve avere un External ID stabile quando possibile.

Formato consigliato:

```text
elesole.product.<slug_o_codice>
elesole.category.<slug_categoria>
elesole.attribute.<slug_attributo>
elesole.attribute_value.<slug_valore>
```

## Gestione errori

Se una riga non e importabile, deve essere esclusa dal file finale e registrata in:

```text
output/validated/import_quality_report.xlsx
```

Il report deve indicare:

- riga;
- prodotto;
- SKU;
- errore;
- campo coinvolto;
- gravita;
- azione consigliata.
