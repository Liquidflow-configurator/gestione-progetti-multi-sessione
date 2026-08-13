---
name: gestione-progetti-multi-sessione
description: Attiva questa skill quando l'utente avvia o menziona un progetto che continuerà su più sessioni future (parole chiave come "progetto", "continuiamo la prossima volta", "riprendiamo questo lavoro", "nuovo progetto", ecc.), oppure quando l'utente segnala un progetto esistente con documentazione disorganizzata (file sparsi, note incoerenti, nessuna struttura chiara). In questi casi, applica di default una struttura standard di 4 file di documentazione: CLAUDE.md (comportamento), AGENTS.md (architettura/regole stabili), summary_for_new_chat.md (cronaca sessione per sessione) e README.md (presentazione esterna). Attiva questa skill SEMPRE anche quando l'utente usa frasi esplicite come "impostami i 4 file", "creami i 4 file di documentazione", "sistemami la documentazione del progetto", "riorganizzami i file di progetto", o nomina direttamente la skill "gestione-progetti-multi-sessione". NON usare per task singoli, una tantum, senza continuità futura.
---

# Gestione Progetti Multi-Sessione

Questa skill definisce come creare e mantenere la documentazione standard per i progetti dell'utente che si sviluppano su più sessioni di chat nel tempo.

## Quando attivarsi

Attivati in questi casi:

1. **Nuovo progetto multi-sessione**: l'utente usa parole come "progetto", "continuiamo la prossima volta", "riprendiamo questo lavoro" per introdurre qualcosa che chiaramente durerà più sessioni. Proponi di impostare i 4 file, non aspettare che te lo chieda esplicitamente.
2. **Progetto esistente disorganizzato**: l'utente segnala (o è evidente dal contesto/dai file) che un progetto già avviato ha documentazione sparsa, incoerente o con nomi di file diversi dallo standard.
3. **Richiesta esplicita**: l'utente chiede di creare/sistemare/riorganizzare i file di documentazione di un progetto.

Non attivarti per richieste singole, senza seguito previsto (es. "scrivimi uno script per convertire questo CSV" e basta).

## I 4 file standard

| File | Scopo | Contenuto tipico |
|---|---|---|
| `CLAUDE.md` | Comportamento | Regole su COME Claude deve comportarsi in questo progetto specifico: tono, livello di dettaglio, cose da fare/non fare, preferenze di workflow |
| `AGENTS.md` | Architettura e regole stabili | Struttura del progetto, componenti, regole tecniche non deducibili dal solo codice, vincoli, trappole note |
| `summary_for_new_chat.md` | Cronaca sessione per sessione | Log progressivo: cosa è stato fatto, decisioni prese, stato attuale, prossimi passi. Serve a far ripartire una nuova chat senza perdere il contesto |
| `README.md` | Presentazione esterna | Cos'è il progetto, a cosa serve, come si usa — pensato per chi (persona o altro strumento) lo legge dall'esterno, non per Claude |

### Regola importante per AGENTS.md (criterio ETH Zurich)

Ogni volta che scrivi o aggiorni **AGENTS.md** (e allo stesso modo **CLAUDE.md**), applica SEMPRE — fin dalla prima stesura, non solo in revisione — questo criterio:

- Per ogni riga/informazione, chiediti: è **OPERATIVA** (una regola, un comando, un vincolo che NON si potrebbe dedurre semplicemente leggendo il codice) → tienila.
- Oppure è **DESCRITTIVA** (una spiegazione dell'architettura, struttura cartelle, cosa fa il progetto — cose scopribili esplorando il repository) → tagliala o spostala nel README.md.
- Eccezione: una sezione "Architettura" NON è automaticamente descrittiva se contiene trappole o bug non ovvi — quel contenuto resta OPERATIVO.
- Non generare mai questi file con `/init` o strumenti automatici senza poi applicare questo filtro: i file auto-generati sono spesso controproducenti perché troppo descrittivi.

Da dove viene: Thibaud Gloaguen, Niels Mündler, Mark Müller, Veselin Raychev, Martin Vechev, *"Evaluating AGENTS.md: Are Repository-Level Context Files Helpful for Coding Agents?"* (ETH Zurich e LogicStar.ai, febbraio 2026) — [arXiv:2602.11988](https://arxiv.org/abs/2602.11988). Il paper è in gran parte **scettico** sui file di contesto: in generale non migliorano il tasso di successo e fanno salire il costo di inferenza di oltre il 20%. L'unica eccezione netta è ciò su cui questo criterio si fonda: le *istruzioni* vengono seguite bene dagli agenti, le *panoramiche del repository* no. Non citarlo come se validasse la pratica in sé.

### summary_for_new_chat.md — quando aggiornarlo

**Non aggiornarlo automaticamente.** Aggiornalo/riscrivilo solo quando l'utente te lo chiede esplicitamente (es. "aggiorna il summary", "chiudi la sessione", "prepara il riepilogo per la prossima volta"). Quando lo fai, aggiungi una nuova voce datata in fondo al file (non riscrivere da zero la cronologia precedente), con:
- Data/sessione
- Cosa è stato fatto
- Decisioni prese e perché
- Stato attuale del progetto
- Prossimi passi previsti

## Dove creare i file

**Chiedi sempre all'utente dove posizionare i 4 file** prima di crearli (es. root del progetto, sottocartella `docs/`, ecc.). Non assumere una posizione di default.

## Se il progetto ha già documentazione esistente

Se trovi file di documentazione già presenti (anche con nomi diversi, es. `NOTES.md`, `TODO.txt`, commenti sparsi, README vecchio):

1. Leggi tutto il contenuto esistente.
2. Proponi all'utente come vuoi smistare le informazioni nei 4 file standard (mostra una bozza di mappatura prima di scrivere).
3. Migra/riorganizza il contenuto nei 4 file standard, applicando comunque il criterio OPERATIVA/DESCRITTIVA per CLAUDE.md e AGENTS.md.
4. Non cancellare i file originali senza conferma esplicita dell'utente — puoi lasciarli o proporre di archiviarli (es. in una cartella `docs/archivio/`), ma chiedi prima.

## Stile di comunicazione

Segui sempre queste preferenze di comunicazione: linguaggio semplice, spiega i termini tecnici tra parentesi, procedi passo dopo passo spiegando il ragionamento (non solo il risultato finale), rispondi sempre in italiano.
