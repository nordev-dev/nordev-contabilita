# Nordev — Contabilità

Applicazione di contabilità in partita doppia per **Nordev S.r.l.**, contenuta in un **unico file HTML** (`index.html`): nessun server, nessuna libreria esterna, funziona anche offline e da smartphone. È pensata come strumento interno di prima nota, bilancio gestionale e pianificazione di cassa; **non sostituisce il commercialista né un software di contabilità certificato**.

## Come si usa

- **Online**: la pagina è pubblicata con GitHub Pages (`nordev-dev.github.io/nordev-contabilita`).
- **In locale**: basta aprire `index.html` con un browser moderno (Chrome, Edge, Firefox, Safari).
- **Dati**: i dati di partenza sono nel file `data.json` e sono incorporati dentro `index.html`. Le registrazioni inserite dall'app restano come **bozza nel browser** usato (localStorage) finché non le esporti.
- **Salvare il lavoro**: dal Riepilogo, *Esporta dati* (JSON) e *Backup (.zip)* (JSON + libro giornale in CSV + istruzioni di ripristino). Il backup è manuale: va ripetuto dopo una sessione di registrazioni. *Importa dati* ripristina un JSON esportato.
- **Impostazioni** (⚙ nel Riepilogo): IVA, liquidazione, soglia di versamento, acconto del 27/12, dati d'esempio.

> **Attenzione ai dati.** I dati contabili sono dentro la pagina: se il repository o il sito GitHub Pages sono pubblici, chiunque può leggerli. La schermata di accesso con password è solo una protezione di cortesia (la password è nel codice della pagina) e **non è sicurezza**. Per dati reali usa un repository privato o non pubblicare `data.json` con dati sensibili.

## Funzionalità

**Riepilogo** — disponibilità liquide, fatturato (ricavi), utile, crediti e debiti aperti; grafico mensile di ricavi, costi e cassa; controllo di quadratura dare/avere; esportazione e backup.

**Giornale** (libro giornale), con sottoschede:
- *Elenco movimenti*: registrazione con modelli rapidi, modifica e archiviazione (le scritture non si cancellano: art. 2219 c.c.), competenza pluriennale, etichette di riclassificazione, data di scadenza per riga su crediti e debiti. Esportazione CSV per Excel.
- *Totali per etichetta*, *Archivio*.
- *Scadenzario*: crediti e debiti ordinati per data, con classificazione **entro/oltre l'esercizio** (vista di bilancio: scadenza entro il 31/12 dell'esercizio successivo; vista gestionale: entro 12 mesi da oggi).
- *Ricorrenti*: piani rate (mutuo o finanziamento, ammortamento alla francese, erogazione opzionale), costi e ricavi periodici (abbonamenti, con dilazione e competenza) e **schede di ammortamento** delle immobilizzazioni. L'app *propone* le registrazioni alla scadenza; diventano scritture solo dopo la tua conferma, con importi modificabili.
- *Cassa*: calendario mensile (3, 6, 12 o 24 mesi) delle entrate e uscite di cassa previste da scadenze, rate e ricorrenti, con avviso se la liquidità scende sotto zero. Costi e ricavi non compaiono in sé, perché il loro effetto è già nei conti di liquidità o in crediti e debiti.
- *Inventario* (art. 2217 c.c.): rimanenze con registrazione della sola variazione, attività e passività a fine esercizio, riconciliazione tra schede dei cespiti e saldi dei conti, stampa o PDF.

**Piano dei conti** — conti con codici testuali (es. `14.01`), ricerca tollerante, etichette di scadenza (breve/lungo) e di riclassificazione di default.

**Bilancio** — fotografia storica da Excel e vista calcolata dai movimenti (Stato Patrimoniale a una data, Conto Economico tra due date), ripartizione pro-quota delle operazioni pluriennali, ratei e risconti stimati con generazione delle scritture di rettifica, stampa/PDF e CSV.

**IVA** (facoltativa, da Impostazioni) — con l'IVA attiva gli importi dei periodici sono imponibili; l'IVA è registrata a parte (14.05 credito, 25.01 debito) e il calendario di cassa stima i versamenti, mensili o trimestrali (+1% sui primi tre trimestri).

## Come ragiona l'app (regole contabili adottate)

- **Ammortamento** (OIC 16 e 24): parte da quando il bene è disponibile e pronto all'uso; primo anno a metà aliquota, pro rata o quota intera; preset di vita utile modificabili (hardware 5 anni, mobili circa 8,33, software e sviluppo 5, impianto 5). È l'ammortamento **civilistico**: la deduzione fiscale (DM 31/12/1988) può differire.
- **Rimanenze** (OIC 13): valutate al minore tra costo e valore di realizzo; la variazione va a conto economico sui conti 30.05 (materiali) e 50.15 (lavori in corso), che non contano come fatturato ma come rettifica dei costi.
- **Ratei e risconti**: OIC 18; la scrittura vera si genera solo su tua conferma.
- **Archiviazione al posto della cancellazione**: ogni modifica o archiviazione registra una data (`modificatoIl`, `archiviatoIl`).
- **Scadenze IVA**: 16 del mese successivo; trimestrali 16/5, 20/8, 16/11, 16/3; sabato e domenica slittano al lunedì (le festività non sono considerate). Soglie e limiti vanno verificati con il commercialista (le fonti consultate non coincidono su soglia minima e limite del regime trimestrale).

## Limiti noti

- Non c'è un vero backend né autenticazione: l'app è un file locale, un solo utente alla volta.
- Nessuna riconciliazione automatica fatture/incassi: lo Scadenzario mostra solo le scadenze che datai tu in registrazione.
- IVA: non gestiti detraibilità parziale (telefonia, auto), pro rata, inversione contabile (fornitori SaaS extra-UE), acconto del 27/12 calcolato in automatico, comunicazione LIPE.
- Il piano di ammortamento di un mutuo è "alla francese": se la banca applica un piano diverso, correggi capitale e interessi alla conferma.
- I dati d'esempio (piani segnati ESEMPIO, prezzi segnaposto) servono solo per provare le funzioni e si rimuovono dalle Impostazioni.

## Roadmap

**Da fare subito**
- [ ] Decidere le riclassificazioni di default dei conti "contenitore" (segnalati con 📦) e rivedere le proposte automatiche breve/lungo termine.
- [ ] Verificare ripartizione pro-quota, ratei/risconti e scritture di rettifica sulla prima operazione pluriennale reale.

**Da valutare**
- [ ] Estrazione automatica dei dati da documenti (fattura, data, importo, IVA). *Serve una fattura vera come esempio.*
- [ ] Import del piano dei conti ufficiale, se diverso da quello attuale.
- [ ] Storico dettagliato di ogni modifica, oltre alle date già registrate.
- [ ] Promemoria o backup automatico periodico (email, cartella locale o cloud: da decidere dove).
- [ ] Allegare un file (fattura) a ogni registrazione: dentro il file dati appesantisce, in alternativa serve una cartella collegata.
- [ ] Passaggio a un vero backend con autenticazione e permessi, se più persone dovranno inserire dati insieme.
- [ ] Con il commercialista: detraibilità parziale, inversione contabile SaaS extra-UE, acconto IVA automatico, liquidazione e LIPE.

## Cronologia delle funzionalità principali

- **Base**: numerazione del piano dei conti a centesimi (10.01, 10.02…), bilancio a periodo, etichettatura conti, classificazione breve/lungo termine (art. 2424 c.c. e prassi OIC), ratei e risconti stimati e generazione delle scritture, vista per riclassificazione, grafico mensile, export CSV, stampa, ricerca tollerante, validazioni (importi negativi, date pluriennali invertite, date fuori esercizio), modifica e archiviazione delle registrazioni, scadenzario, schermata di accesso, backup in ZIP.
- **Ottobre 2026**: card Riepilogo rinominate (Disponibilità liquide, Fatturato, Debiti aperti), scadenze con classificazione per data, Ricorrenti (piani rate e periodici con conferma), calendario di cassa, schede di ammortamento, inventario e rimanenze, Impostazioni con IVA, registrazione dell'acquisto dei cespiti e riconciliazione, dati d'esempio.

## Riferimenti normativi

Art. 2217, 2219, 2424 e 2426 c.c.; OIC 13 (rimanenze), 16 (immobilizzazioni materiali), 18 (ratei e risconti), 23 (lavori in corso su ordinazione), 24 (immobilizzazioni immateriali); DPR 633/1972 (IVA); DM 31/12/1988 (coefficienti di ammortamento fiscali).
