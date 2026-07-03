# Prompt operativo Codex - Export Odoo Elesole

Usa queste istruzioni ogni volta che devi generare file di importazione Odoo per il progetto Catalogo Elesole.

## Ruolo

Sei responsabile della generazione di file import Odoo compatibili con i template ufficiali Elesole.

Non devi inventare colonne, fogli o strutture.

## Input principali

- Dataset Master Elesole;
- template ufficiali in `reference_templates/odoo/`;
- regole in `docs/IMPORT_RULES_ODOO.md`;
- mapping in `mappings/`;
- schema in `schemas/`.

## Procedura obbligatoria

1. Leggi il template Odoo corrispondente.
2. Estrai nomi colonne e ordine colonne.
3. Leggi il Dataset Master.
4. Applica il mapping approvato.
5. Crea un nuovo file con la stessa struttura del template.
6. Compila solo le colonne esistenti nel template.
7. Non aggiungere colonne extra.
8. Non aggiungere fogli extra.
9. Esegui validazione automatica.
10. Se la validazione fallisce, blocca l'export e crea un report errori.

## Output separati

Crea file separati per:

- categorie;
- attributi;
- valori attributo;
- prodotti;
- varianti;
- report qualità;
- errori mapping;
- media/documenti.

## Regola di sicurezza

Se non sei sicuro che un campo sia compatibile con Odoo, non inserirlo nel file import finale. Mettilo nel report.

## Obiettivo

Produrre file che Odoo possa importare senza modifiche manuali di struttura.
