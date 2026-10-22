# Notizie da tenere d'occhio o da approfondire

Sono nella tabella `notizia_da_seguire` del database (non più in questo file). Le inserisce e le chiude il **Caporedattore** su indicazione di Dolphino; il **Cronista** le legge a ogni giro (skill ricerca-notizie, punto 0) e non le modifica.

Colonne: `titolo`, `cosa` (cosa aspettarsi), `cosa_fare` (cosa fare quando la notizia esce: es. trattarla come aggiornamento di una notizia esistente, quali fonti controllare), `stato` (`attiva`/`chiusa`), `inserita_il`, `chiusa_il`, `esito`.

- Elenco attive: `select titolo, cosa, cosa_fare, inserita_il from notizia_da_seguire where stato='attiva'`
- Nuova voce (Caporedattore): `insert into notizia_da_seguire (titolo, cosa, cosa_fare) values (...)`
- Chiusura (Caporedattore, quando la notizia è uscita e la card è creata o la voce non serve più): `update notizia_da_seguire set stato='chiusa', chiusa_il=current_date, esito='...' where id=...`

Se una voce attiva non è ancora uscita il Cronista non inventa niente: la scrive tra le "Scartate" come "in attesa" e la voce resta attiva.
