# gestione-progetti-multi-sessione

Una **skill per [Claude Code](https://claude.com/claude-code)** che impone una struttura di documentazione standard ai progetti che durano più sessioni di lavoro.

> 🇬🇧 English version: [multi-session-project-docs](https://github.com/Liquidflow-configurator/multi-session-project-docs) — stesso contenuto, in inglese.

📺 **[Guarda la presentazione in video](https://youtu.be/eWo0PfzuJoU)** (8 minuti, in italiano) — panoramica dei quattro file, delle regole e del metodo per riordinare un progetto già caotico.

## Il problema

Un progetto che dura settimane o mesi vive su decine di chat diverse. Ogni chat nuova riparte da zero: l'assistente non ricorda le decisioni prese, il contesto va perso e la documentazione cresce disordinata — un `NOTES.md` qui, un `TODO.txt` là, un README che nessuno aggiorna.

## La soluzione: 4 file, 4 ruoli distinti

| File | Ruolo |
|---|---|
| `CLAUDE.md` | **Comportamento** — come l'assistente deve lavorare su questo progetto: tono, livello di dettaglio, cosa fare e cosa evitare |
| `AGENTS.md` | **Regole stabili** — vincoli tecnici e trappole note che non si possono dedurre leggendo il codice |
| `summary_for_new_chat.md` | **Diario** — log datato, solo in aggiunta: cosa è stato fatto, decisioni e perché, stato attuale, prossimi passi |
| `README.md` | **Presentazione** — cos'è il progetto e come si usa, per chi lo legge dall'esterno |

La regola che tiene in piedi tutto è il criterio **operativo contro descrittivo**: in `CLAUDE.md` e `AGENTS.md` sopravvive solo ciò che è una regola, un comando o un vincolo **non deducibile leggendo il codice**. Tutto ciò che descrive e basta l'architettura va nel README, o si taglia. È anche il motivo per cui i file generati automaticamente tendono a fare più danno che altro: sono quasi solo descrittivi.

### Da dove viene il criterio

Non è un'impressione personale. L'hanno misurato Gloaguen, Mündler, Müller, Raychev e Vechev (ETH Zurigo / LogicStar.ai) in *["Evaluating AGENTS.md: Are Repository-Level Context Files Helpful for Coding Agents?"](https://arxiv.org/abs/2602.11988)* (febbraio 2026).

Il risultato principale è **scettico**, ed è giusto dirlo: fornire file di contesto a un agente **non migliora** in generale il tasso di successo, e fa salire il costo di elaborazione di oltre il 20%. Ma il dettaglio è ciò che conta qui: **le istruzioni vengono seguite bene dagli agenti, mentre le panoramiche del repository — diffusissime e raccomandate dagli stessi fornitori dei modelli — sono inutili.** Questa skill tiene solo la metà che funziona.

## Due regole che fanno la differenza

- **Il diario non si aggiorna mai da solo.** Solo su richiesta esplicita, e sempre aggiungendo una voce datata in fondo: la cronologia passata non si riscrive.
- **L'assistente si ferma e chiede.** Chiede dove mettere i file invece di deciderlo da sé, e non cancella mai la documentazione preesistente senza conferma.

Questa skill non è un automatismo: è un insieme di istruzioni che l'assistente segue mentre lavora.

## Installazione

```bash
git clone https://github.com/Liquidflow-configurator/gestione-progetti-multi-sessione.git ~/.claude/skills/gestione-progetti-multi-sessione
```

Riavvia Claude Code. La skill si attiva da sola quando riconosce un progetto multi-sessione o una documentazione disordinata, oppure la richiami a mano con `/gestione-progetti-multi-sessione`.

Installa questa **oppure** la versione inglese, non entrambe: farebbero la stessa cosa due volte.

## Licenza

MIT — vedi [LICENSE](LICENSE).
