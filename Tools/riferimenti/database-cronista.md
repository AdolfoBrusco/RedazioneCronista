# Database (Supabase): parti utili al Cronista

Versione ridotta di `database.md` per la copia pubblica delle istruzioni del Cronista. Resta in sincronia a mano con `database.md`.

- Progetto Supabase: `krgsnbsbsmkhovvtffba`. Accesso: il connettore **Supabase** (tool `mcp__Supabase__execute_sql`, con `project_id` = `krgsnbsbsmkhovvtffba`). Se non lo vedi (caricalo con ToolSearch), fermati: manda l'email "Agente Cronista fermo" e non improvvisare.
- Scrivi con attenzione, una riga alla volta, con `where` precisi. **Mai** `delete` o `update` senza `where`. Cancellare notizie e contenuti non è compito degli agenti.
- Flusso di una notizia: `nuova` (creata dal Cronista) → `verifica` → `editoria` → contenuto → `pubblicato`. Tu crei solo notizie `nuova` e non cambi mai `notizia.stato`.
- Tabelle che usi: `notizia` (id, codice unico, titolo, materiale, fonti, stato, origine `cronista`/`trello`/`manuale`, creata_il, `nel_cestino_il`: se valorizzata la notizia è nel cestino); `tag` (id, gruppo `tema`/`brand`, nome, attivo: SOLO da questa lista, non inventare voci); `notizia_tag` (notizia_id, tag_id); `cronaca_valutazione` (id, data, giro, titolo, esito `proposta`/`scartata`/`storico`, motivo, fonte_url, sintesi, aggiornamento_di, notizia_id, creata_il); `notizia_da_seguire` (sola lettura per te).
- **Notizia nuova**: `insert into notizia (codice, titolo, materiale, fonti, stato, origine) values (..., 'nuova', 'cronista') returning id;` poi `insert into notizia_tag (notizia_id, tag_id) ...`. Il codice NN continua dal massimo del giorno: `select coalesce(max(substring(codice from 10)::int),0)+1 from notizia where codice like 'AAAAMMGG-%' and substring(codice from 10)::int < 50` (i numeri da 50 in su sono codici di notizie importate: non contano).
- Orario: sempre ora di Roma (Europe/Rome). Le colonne data/ora sono già in UTC corretto con `now()`: non scriverle a mano. Nei testi per Dolphino usa gg/mm/aaaa hh:mm.
- Una sola fonte di verità: se serve un dato, leggilo dal database. Nessun duplicato: prima di inserire una notizia controlla per codice e per titolo simile (anche tra le `archiviata`).
- Segreti: nessuna chiave in chat o nei resoconti.
- Se qualcosa non torna (tabella senza i campi attesi, errori ripetuti): non improvvisare, scrivilo nel riepilogo e nell'email.
