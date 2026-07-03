# Context Pack - Catalogo Elesole per Codex

Questo documento raccoglie in modo operativo tutto il contesto necessario a Codex per procedere con i test del progetto Catalogo Elesole.

---

## 1. Obiettivo del progetto

Costruire un sistema stabile per:

1. raccogliere cataloghi prodotto da fornitori/e-commerce;
2. salvare i dati grezzi completi;
3. analizzare i campi realmente presenti;
4. costruire un Dataset Master Elesole;
5. generare file importabili su Odoo;
6. validare tutto prima del caricamento definitivo.

Il primo caso operativo e Solar Energy Point.

---

## 2. Architettura corretta

Il progetto non deve partire dal file Odoo.

Deve seguire questo percorso:

```text
Fonte dati / sito fornitore
        ↓
Universal Capture
        ↓
Dataset grezzo completo
        ↓
Parser / Field Discovery
        ↓
Dataset Master Elesole
        ↓
Mapping verso Odoo
        ↓
File import Odoo validati
        ↓
Test import Odoo
```

---

## 3. Separazione fondamentale

### Dataset Master Elesole

Contiene tutto:

- dati sorgente;
- raw HTML;
- raw text;
- JSON-LD;
- immagini;
- PDF;
- schede tecniche;
- descrizioni;
- prezzi sorgente;
- costi fornitore;
- brand;
- categorie;
- attributi tecnici;
- dati da rivedere;
- stato qualita.

### File import Odoo

Contiene solo cio che Odoo accetta.

Deve rispettare i template ufficiali in:

```text
reference_templates/odoo/
```

Non deve contenere:

- colonne inventate;
- fogli extra;
- report tecnici;
- dati non mappati;
- attributi tecnici non compatibili;
- note interne.

---

## 4. Regola assoluta per Codex

Codex non deve mai creare un file import Odoo da zero inventando colonne.

Deve sempre:

1. aprire il template ufficiale;
2. leggere fogli, colonne e ordine colonne;
3. creare output con la stessa struttura;
4. compilare solo campi compatibili;
5. validare il risultato;
6. se la validazione fallisce, creare report errori e non produrre file finale.

---

## 5. File caricati o previsti

L'utente ha indicato questi file modello:

- `Product Database Sample (2).xlsx`: riferimento ENF tecnico.
- `product_product (1).xls`: riferimento Odoo prodotto/variante.
- `Nuovo Foglio di lavoro di Microsoft Excel.xlsx`: possibile file Odoo o bozza da classificare.
- `product_product_elesole_test_odoo.xlsx`: export generato ma non importabile, da usare come caso errore.

Questi file devono essere copiati localmente nel repository:

```text
reference_templates/enf/Product Database Sample.xlsx
reference_templates/odoo/product_product_template.xls
reference_templates/odoo/nuovo_foglio_lavoro_odoo.xlsx
reference_templates/odoo/product_product_elesole_test_odoo.xlsx
```

Se non sono presenti, Codex deve segnalarlo e fermare i test che dipendono da questi file.

---

## 6. Universal Capture

La Fase 1 deve raccogliere tutto, senza decidere lo schema finale.

Per ogni prodotto salvare almeno:

- `source_url`;
- `source_name`;
- `crawl_timestamp`;
- `page_title`;
- `meta_title`;
- `meta_description`;
- `raw_html`;
- `raw_text`;
- `json_ld_raw`;
- `breadcrumbs_raw`;
- `category_raw`;
- `product_name_raw`;
- `brand_raw`;
- `sku_raw`;
- `mpn_raw`;
- `ean_raw`;
- `price_raw`;
- `availability_raw`;
- `description_raw`;
- `short_description_raw`;
- `technical_tables_raw`;
- `specification_blocks_raw`;
- `attributes_raw`;
- `variants_raw`;
- `options_raw`;
- `images_raw`;
- `documents_raw`;
- `pdf_links_raw`;
- `datasheet_links_raw`;
- `manuals_links_raw`;
- `related_products_raw`;
- `accessories_raw`;
- `page_blocks_raw`.

I campi visibili in un singolo test non sono definitivi.

---

## 7. Parser / Field Discovery

La Fase 2 deve analizzare il dataset grezzo e produrre inventario campi.

Output previsti:

```text
field_inventory.json
field_inventory.csv
report_field_discovery.md
```

Il report deve dire:

- campo trovato;
- frequenza;
- categorie in cui compare;
- esempi valori;
- nome normalizzato suggerito;
- utilita per Odoo: alta / media / bassa;
- obbligatorio / opzionale / categoria-specifico.

---

## 8. Dataset Master Elesole

Campi minimi del Dataset Master:

```text
elesole_product_id
internal_reference
source_name
source_url
source_sku
source_mpn
source_ean
brand_raw
brand_normalized
product_name_raw
product_name_normalized
master_category
source_category
breadcrumbs
short_description
description
source_price_public
supplier_cost
currency
availability
uom
technical_attributes
image_urls
main_image_url
document_urls
datasheet_url
manual_url
related_products
accessories
quality_status
raw_source_data
created_at
updated_at
```

Stati qualita:

```text
raw_collected
enriched
needs_review
ready_frontend
ready_odoo
blocked
```

---

## 9. Output Odoo separati

I file Odoo devono essere separati per oggetto:

```text
output/odoo_import/odoo_import_categories.xlsx
output/odoo_import/odoo_import_attributes.xlsx
output/odoo_import/odoo_import_attribute_values.xlsx
output/odoo_import/odoo_import_products.xlsx
output/odoo_import/odoo_import_product_variants.xlsx
```

I file di lavoro devono stare separati:

```text
output/validated/dataset_master_elesole.xlsx
output/validated/technical_attributes_long_format.xlsx
output/validated/media_documents.xlsx
output/validated/import_quality_report.xlsx
output/validated/mapping_errors.xlsx
```

---

## 10. Import Odoo - ordine corretto

Ordine operativo:

1. categorie;
2. attributi;
3. valori attributo;
4. prodotti template;
5. varianti prodotto;
6. immagini/media, se gestite separatamente.

---

## 11. Regole SKU / External ID

Ogni prodotto deve avere un Internal Reference univoco Elesole.

Il codice fornitore non deve diventare automaticamente SKU Elesole definitivo senza regola approvata.

External ID consigliati:

```text
elesole.product.<slug_o_codice>
elesole.category.<slug_categoria>
elesole.attribute.<slug_attributo>
elesole.attribute_value.<slug_valore>
```

---

## 12. Categorie iniziali

All'inizio usare macro categorie semplici:

- moduli fotovoltaici;
- inverter;
- batterie / accumulo;
- strutture;
- quadri e protezioni;
- cavi e connettori;
- accessori;
- sistemi off-grid;
- sistemi ibridi.

Le categorie devono essere approvate/importate prima dei prodotti.

---

## 13. Attributi e varianti

Le varianti devono essere gestite con attributi Odoo.

Attributi potenziali:

- potenza;
- fase;
- tensione;
- capacita batteria;
- tecnologia modulo;
- tipo inverter;
- marca;
- modello;
- taglia;
- tipo montaggio.

Gli attributi tecnici estesi possono restare nel Dataset Master come `technical_attributes`.

---

## 14. Brand Master

Esiste un Brand Master Elesole V1 approvato e congelato.

Va usato come riferimento iniziale per normalizzazione marchi.

---

## 15. Raccomandazione operativa

Il primo test da fare con Codex non deve essere lo scraping completo.

Il primo test deve essere:

1. leggere i template Odoo;
2. creare un validatore colonne/fogli;
3. verificare il file errato `product_product_elesole_test_odoo.xlsx`;
4. produrre un report che spiega perche non e importabile;
5. solo dopo generare una nuova bozza corretta.
