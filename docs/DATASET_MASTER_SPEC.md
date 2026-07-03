# Specifica Dataset Master Elesole

Il Dataset Master Elesole e la base dati completa del catalogo.

Non coincide con il file import Odoo.

## Obiettivi

Il Dataset Master deve essere:

- completo;
- tracciabile;
- normalizzato;
- controllabile;
- riutilizzabile per piu fornitori;
- trasformabile in file import Odoo solo dopo validazione.

## Campi minimi consigliati

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

## Stati quality_status

Valori consigliati:

```text
raw_collected
enriched
needs_review
ready_frontend
ready_odoo
blocked
```

## technical_attributes

Gli attributi tecnici devono rimanere in formato strutturato.

Esempio JSON:

```json
{
  "power_w": "570",
  "voltage_v": "41.5",
  "current_a": "13.7",
  "dimensions_mm": "2278 x 1134 x 30",
  "weight_kg": "32"
}
```

Non appiattire tutti gli attributi tecnici in colonne Odoo se non sono necessari all'importazione.

## raw_source_data

Ogni prodotto deve mantenere il dato grezzo originale per controllo e tracciabilita.

`raw_source_data` puo contenere:

- HTML;
- JSON-LD;
- blocchi pagina;
- tabelle tecniche raw;
- attributi raw;
- dati non classificati.

## Regola di separazione

Il Dataset Master puo essere ricco.

Il file Odoo deve essere stretto.

Se un campo non serve a Odoo ma serve al catalogo, rimane nel Dataset Master.
