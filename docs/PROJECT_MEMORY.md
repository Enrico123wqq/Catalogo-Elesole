# Memoria operativa progetto Elesole / Catalogo Odoo

Documento di contesto da usare come memoria stabile del progetto Catalogo Elesole.

> Nota: questo file contiene solo informazioni operative pertinenti al progetto Elesole, catalogo, Odoo, scraping, importazione dati e flussi collegati. Non include informazioni personali non necessarie al lavoro tecnico.

---

## 1. Identita del progetto

- Progetto principale: **Elesole**.
- Dominio: **elesole.com**.
- Obiettivo: costruire un catalogo prodotti fotovoltaico e relativo listino importabile su Odoo.
- Contesto aziendale: Elesole nasce come progetto di distribuzione fotovoltaica collegato a esperienza nel settore elettrico e fotovoltaico.
- Stack principale: **Odoo Online / Odoo 19 come riferimento operativo**, Website, CRM, Sales, Purchase, Inventory.
- Repository operativo: `Enrico123wqq/Catalogo-Elesole`.

---

## 2. Principio operativo principale

Il flusso corretto non parte dal file Odoo.

Il flusso corretto e:

1. Raccolta dati grezzi completa.
2. Costruzione Dataset Master Elesole.
3. Controlli qualita e arricchimento.
4. Mapping verso Odoo.
5. Creazione file import Odoo solo dopo validazione.

Regola fondamentale:

- **Dataset Master** = ricco, completo, tracciabile.
- **File Odoo** = stretto, pulito, identico ai template ufficiali.

Codex non deve inventare colonne Odoo.

---

## 3. Google Drive, GitHub, Codex, Apify e Odoo

### Google Drive

Google Drive e il cervello operativo umano del progetto.

Serve per:

- archiviare documenti;
- conservare cataloghi fornitori;
- mantenere materiale commerciale;
- raccogliere file Excel, immagini, PDF e documenti ricevuti.

### GitHub

GitHub e il cervello tecnico condiviso con Codex.

Serve per:

- template ufficiali;
- regole tecniche;
- prompt Codex;
- script;
- mapping;
- workflow;
- output controllati.

### Codex

Codex deve essere usato per:

- scrivere codice;
- costruire scraper;
- analizzare dataset;
- generare parser;
- validare file;
- creare export Odoo rispettando i template.

Codex non deve inventare strutture import Odoo.

### Apify

Apify e il motore di scraping.

Serve per:

- crawling sito fornitore;
- Universal Capture;
- scraping finale;
- raccolta dataset grezzi.

### Odoo

Odoo riceve solo file validati.

Prima si importano:

1. categorie;
2. attributi;
3. valori attributo;
4. prodotti template;
5. varianti, se necessarie.

---

## 4. Workflow Catalogo Elesole

### Fase 1 - Universal Capture

Obiettivo: raccogliere tutto senza perdere informazioni.

Da salvare per ogni prodotto:

- URL sorgente;
- source name;
- timestamp crawl;
- HTML completo;
- testo pagina;
- JSON-LD;
- breadcrumb;
- categoria sorgente;
- nome prodotto grezzo;
- brand grezzo;
- SKU sorgente;
- MPN, se presente;
- EAN, se presente;
- prezzo pubblico sorgente;
- disponibilita;
- descrizioni;
- tabelle tecniche;
- blocchi specifiche;
- attributi;
- varianti;
- opzioni;
- immagini;
- PDF;
- datasheet;
- manuali;
- prodotti correlati;
- accessori;
- blocchi pagina non classificati.

In questa fase non si decide lo schema finale.

I campi che appaiono in un test iniziale non devono essere considerati definitivi.

### Fase 2 - Parser / Field Discovery

Obiettivo: capire quali campi esistono davvero nel catalogo.

Il parser deve:

- leggere tutto il dataset grezzo;
- estrarre tutte le chiavi delle tabelle tecniche;
- contare frequenza dei campi;
- riconoscere sinonimi;
- distinguere campi generali e categoria-specifici;
- proporre normalizzazioni;
- indicare utilita per Odoo.

Output:

- `field_inventory.json`;
- `field_inventory.csv`;
- `report_field_discovery.md`.

### Fase 3 - Dataset Master Elesole

Obiettivo: creare la base dati completa e normalizzata.

Il Dataset Master include almeno:

- `elesole_product_id`;
- `internal_reference` / SKU Odoo univoco;
- `source_name`;
- `source_url`;
- `source_sku`;
- `brand_raw`;
- `brand_normalized`;
- `product_name_raw`;
- `product_name_normalized`;
- `master_category`;
- `source_category`;
- `breadcrumbs`;
- `description`;
- `short_description`;
- `source_price_public`;
- `supplier_cost`;
- `currency`;
- `availability`;
- `uom`;
- `technical_attributes`;
- `image_urls`;
- `main_image_url`;
- `document_urls`;
- `datasheet_url`;
- `manual_url`;
- `related_products`;
- `accessories`;
- `quality_status`;
- `raw_source_data`.

### Fase 4 - Final Scraper

Solo dopo validazione dello schema, creare lo scraper finale.

Output attesi:

- `dataset_master_raw.json`;
- `dataset_master_raw.csv`;
- `errors.csv`;
- `missing_fields_report.csv`;
- `crawl_summary.md`.

### Fase 5 - Export Odoo

L'export Odoo deve rispettare i template ufficiali.

File separati consigliati:

- categorie;
- attributi;
- valori attributo;
- prodotti;
- varianti;
- media/documenti;
- report qualita;
- errori mapping.

---

## 5. Regole Odoo consolidate

- Odoo 19 e il riferimento principale.
- Tutti i cataloghi fornitori devono essere normalizzati prima del caricamento.
- Ogni prodotto deve avere SKU/Internal Reference Elesole univoco.
- Le categorie devono essere create prima dell'importazione prodotti.
- Gli attributi devono essere creati prima dei prodotti con varianti.
- Le varianti devono essere gestite tramite attributi Odoo.
- Ogni importazione deve essere testata prima del caricamento definitivo.
- Il file import Odoo deve essere identico al template ufficiale per colonne e ordine colonne.
- I dati tecnici estesi non vanno forzati nel file Odoo se non sono compatibili.

---

## 6. Template e file modello

I template ufficiali devono stare in:

```text
reference_templates/odoo/
```

I riferimenti ENF devono stare in:

```text
reference_templates/enf/
```

Regola:

- ENF aiuta a capire campi tecnici e struttura dati prodotto.
- ENF non e il tracciato Odoo.
- Odoo template decide colonne, ordine e file import.

File caricati dall'utente da conservare nel repository locale:

- `Product Database Sample (2).xlsx` -> riferimento ENF.
- `product_product (1).xls` -> riferimento import Odoo.
- `Nuovo Foglio di lavoro di Microsoft Excel.xlsx` -> possibile riferimento Odoo da rinominare.
- `product_product_elesole_test_odoo.xlsx` -> bozza generata, non considerare template se non importabile.

---

## 7. Brand Master Elesole

E stato approvato e congelato il **File 2 - Brand Master Elesole V1**.

Uso:

- elenco marchi ufficiale iniziale;
- base per normalizzazione brand;
- riferimento fino a nuova revisione da importazioni massive o scraping completo.

---

## 8. Categorie e macro categorie iniziali

All'inizio usare macro categorie semplici, senza eccessivo dettaglio.

Esempi di classificazioni base:

- moduli fotovoltaici;
- inverter;
- batterie / accumulo;
- strutture;
- quadri e protezioni;
- cavi e connettori;
- accessori;
- sistemi off-grid;
- sistemi ibridi;
- prodotti monofacciali / bifacciali, quando rilevante.

Le categorie definitive devono essere importate prima dei prodotti.

---

## 9. Attributi e varianti

Le varianti devono essere gestite con attributi Odoo, non duplicando male i prodotti.

Esempi attributi potenziali:

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

Gli attributi tecnici estesi possono restare in `technical_attributes` nel Dataset Master.

---

## 10. Prezzi e campi economici

Il Dataset Master deve distinguere:

- prezzo pubblico sorgente / benchmark;
- costo fornitore reale;
- prezzo di vendita Elesole;
- eventuale listino riservato;
- valuta;
- IVA, se gestita separatamente.

Nel progetto e stato indicato `source_price_public` come benchmark, ad esempio dal catalogo Solar Energy Point.

Il costo reale fornitore deve essere un campo separato: `supplier_cost`.

---

## 11. Logistica e forniture

Flusso logistico desiderato:

- vendita con spedizione su quotazione;
- alla conferma ordine cliente si generano richieste a fornitore e trasportatore;
- dati trasporto importanti: colli, dimensioni, peso, categoria merce, incoterms, data ritiro;
- carrier citati: DB Schenker, Savino Del Bene, DHL;
- Incoterms preferito: EXW, ritiro presso magazzino fornitore.

Nota: non fornire cavidotti come parte standard.

---

## 12. Fonti e fornitori citati

Fornitori e riferimenti citati nel progetto:

- Solar Energy Point;
- VP Solar;
- Sacchi Elettroforniture;
- Sonepar;
- BayWa r.e.;
- Prysmian;
- Convert / Valmont;
- MRac;
- Jinko;
- JA Solar;
- Ingeteam;
- Huawei;
- ZCS;
- Santerno.

Solar Energy Point e il primo caso operativo per scraping e benchmark catalogo.

---

## 13. Modello commerciale Elesole

Focus principale:

- programma a provvigione Elesole per professionisti che indirizzano acquisti verso Elesole.

Claim interno:

> Valorizzare i professionisti che aiutano i fornitori a vendere migliaia di prodotti senza ricevere alcun compenso.

Meccanismo semplice:

1. Il professionista indirizza l'acquisto verso Elesole.
2. Il cliente ordina.
3. Il professionista riceve il compenso tracciato.

Esempio simulazione:

- 3 percento del valore preventivo come base test.
- Banner test: guadagna fino a 100 euro ogni 3000 euro di ordini generati.

Alternativa opzionale:

- listino riservato all'ingrosso per rivendita con margine, solo per ordini voluminosi.

---

## 14. Funnel partner Elesole

Flusso consolidato:

1. Adv / Email / Webinar.
2. Landing con form.
3. Automazione email con tour e video.
4. Prenotazione Call 1.
5. Call 1: spiegazione e accesso demo.
6. Demo autonoma.
7. Call 2: demo guidata e proposta ordine pilota.
8. Ordine pilota guidato.
9. Attivazione account con contratto.
10. Onboarding e supporto.

Ordine pilota = primo ordine reale guidato a basso rischio.

---

## 15. Form partner

Campi principali del form partner:

- dati contatto;
- tipo attivita: consulenza, installazione, progettazione, EPC, rivendita, altro;
- ruolo: titolare, responsabile, dipendente, libero professionista;
- volumi progetti mensili;
- valore economico medio impianti;
- potenza media impianti;
- modalita lavoro: vende, non vende, solo pratiche, consulenza, progettazione;
- fattori importanti: prezzo, tempi, supporto, garanzie, semplicita;
- valore medio preventivi;
- numero preventivi.

---

## 16. Comunicazione e stile

Preferenze operative:

- usare italiano chiaro e professionale;
- evitare nomi inglesi quando esiste alternativa italiana chiara;
- essere concreti;
- dichiarare limiti;
- non compiacere;
- dare raccomandazioni nette;
- distinguere fattibilita reale, strumenti, automazioni, AI, controllo umano, investimento, rischi e raccomandazione.

---

## 17. Regola per valutazioni tecniche

Per valutazioni su strumenti, investimenti, flussi o metodi, fornire sempre:

- fattibilita reale;
- strumenti da usare;
- cosa automatizzare;
- cosa richiede AI;
- cosa richiede controllo umano;
- investimento / complessita;
- rischi;
- raccomandazione netta.

Le soluzioni con bassa fattibilita rispetto agli obiettivi Elesole non devono essere raccomandate come strada principale.

---

## 18. Regola per Codex

Codex deve sempre leggere:

- `docs/PROJECT_MEMORY.md`;
- `docs/WORKFLOW.md`;
- `docs/IMPORT_RULES_ODOO.md`;
- `docs/DATASET_MASTER_SPEC.md`;
- `codex/prompts/ODOO_EXPORT_SYSTEM_PROMPT.md`;
- template in `reference_templates/odoo/`.

Prima di creare file Odoo, Codex deve validare colonne e ordine colonne rispetto al template ufficiale.

Se non puo validare, deve fermarsi e generare un report errori.
