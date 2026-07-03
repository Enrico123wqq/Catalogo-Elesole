# Schema Dataset Master Elesole

Campi principali del Dataset Master.

## Identificazione

- `elesole_product_id`: ID interno prodotto Elesole.
- `internal_reference`: SKU/Internal Reference Odoo, univoco.
- `source_name`: nome sorgente, esempio Solar Energy Point.
- `source_url`: URL pagina prodotto sorgente.
- `source_sku`: codice prodotto sorgente.
- `source_mpn`: codice produttore, se presente.
- `source_ean`: codice EAN, se presente.

## Brand e nome prodotto

- `brand_raw`: marchio come trovato nella sorgente.
- `brand_normalized`: marchio normalizzato Elesole.
- `product_name_raw`: nome prodotto grezzo.
- `product_name_normalized`: nome prodotto pulito.

## Categorie

- `master_category`: categoria Elesole.
- `source_category`: categoria sorgente.
- `breadcrumbs`: percorso categoria sorgente.

## Descrizioni

- `short_description`: descrizione breve.
- `description`: descrizione completa.

## Dati commerciali

- `source_price_public`: prezzo pubblico fonte.
- `supplier_cost`: costo fornitore reale, se disponibile.
- `currency`: valuta.
- `availability`: disponibilita.
- `uom`: unita di misura.

## Attributi tecnici

- `technical_attributes`: oggetto strutturato con attributi tecnici.

Esempio:

```json
{
  "power_w": "570",
  "voltage_v": "41.5",
  "weight_kg": "32"
}
```

## Media e documenti

- `image_urls`: elenco immagini.
- `main_image_url`: immagine principale.
- `document_urls`: documenti collegati.
- `datasheet_url`: scheda tecnica.
- `manual_url`: manuale.

## Relazioni

- `related_products`: prodotti correlati.
- `accessories`: accessori.

## Stato qualita

- `quality_status`: stato del record.

Valori ammessi:

- `raw_collected`
- `enriched`
- `needs_review`
- `ready_frontend`
- `ready_odoo`
- `blocked`

## Tracciabilita

- `raw_source_data`: dati grezzi originali.
- `created_at`: data creazione record.
- `updated_at`: data ultimo aggiornamento.
