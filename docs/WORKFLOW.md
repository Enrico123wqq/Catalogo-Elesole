# Workflow operativo Catalogo Elesole

## Architettura generale

Il sistema usa tre livelli distinti:

1. **Raccolta grezza**: scraping e salvataggio completo dei dati fonte.
2. **Dataset Master Elesole**: archivio normalizzato, completo e tracciabile.
3. **Import Odoo**: file finali stretti, compatibili con i template ufficiali.

## Fase 1 - Universal Capture

Obiettivo: raccogliere tutto senza decidere ancora lo schema finale.

Da raccogliere per ogni prodotto:

- URL sorgente;
- HTML completo;
- testo pagina;
- JSON-LD;
- breadcrumb;
- categorie sorgente;
- nome prodotto;
- brand;
- codici prodotto disponibili;
- prezzo;
- disponibilità;
- descrizioni;
- tabelle tecniche;
- attributi;
- varianti;
- immagini;
- PDF;
- datasheet;
- manuali;
- prodotti correlati;
- accessori;
- blocchi pagina non classificati.

In questa fase non si elimina quasi nulla.

## Fase 2 - Parser / Field Discovery

Obiettivo: capire quali campi esistono davvero nel catalogo.

Il parser deve:

- leggere tutti i prodotti raccolti;
- individuare le chiavi tecniche ricorrenti;
- riconoscere sinonimi;
- separare campi generali e categoria-specifici;
- proporre campi normalizzati;
- indicare frequenza e utilità di ogni campo.

Output attesi:

- `field_inventory.json`;
- `field_inventory.csv`;
- `report_field_discovery.md`.

## Fase 3 - Dataset Master Elesole

Obiettivo: costruire la base dati ricca e controllabile.

Il Dataset Master contiene:

- dati sorgente;
- dati normalizzati;
- categorie Elesole;
- brand normalizzato;
- attributi tecnici;
- media e documenti;
- stato qualità;
- tracciabilità.

## Fase 4 - Export Odoo

Obiettivo: creare file importabili da Odoo.

Regola: il file Odoo non deve contenere tutto. Deve contenere solo ciò che il template Odoo ufficiale accetta.

Gli output Odoo devono essere separati:

- categorie;
- prodotti;
- varianti;
- attributi;
- valori attributo;
- immagini/media, se gestite separatamente;
- report errori.

## Fase 5 - Quality Check

Prima di importare in Odoo, controllare:

- colonne uguali al template;
- ordine colonne identico;
- SKU/Internal Reference univoci;
- External ID univoci;
- categorie già presenti o importabili;
- attributi e valori coerenti;
- prezzi numerici;
- immagini e PDF validi;
- righe senza nome prodotto;
- duplicati;
- campi obbligatori mancanti.

Se il controllo fallisce, non generare il file finale importabile.
