# Esempio: Il Conclave analizza se stesso

## Il quesito

> La struttura attuale de Il Conclave — un council di 8 archetipi single-model con framework analitici forzati, confidence scoring, dibattito strutturato, Red Team e ACH — è la risposta giusta al problema della diversità insufficiente nei council single-model? Alla luce della ricerca accademica corrente, lo skill è strutturalmente solido, sovradimensionato, o manca qualcosa di critico?

**Contesto:** Il Conclave è uno skill per Claude Code che simula un consiglio di 8 archetipi AI usando un singolo modello. La ricerca accademica (ICLR 2025, Nature 2026, ACL 2025) mostra che l'approccio multi-agente omogeneo ha limiti strutturali. Abbiamo chiesto al Conclave di analizzare se stesso.

---

## Il processo

### Fase 1 — Framing
Raccolta del contesto dalla ricerca accademica: paper DMAD (ICLR 2025), paper sugli adversarial agent (Nature 2026), Perplexity Model Council, paper sulla confidence-weighted voting (ACL 2025). Formulazione della domanda in modo neutro.

### Fase 2 — 6 Consiglieri in parallelo
Ogni consigliere ha analizzato la domanda con il proprio framework:

| Consigliere | Framework | Posizione iniziale | Confidenza |
|-------------|-----------|-------------------|------------|
| Savonarola | Pre-Mortem | Il sistema ottimizza per l'apparenza del rigore, non per i risultati | 8/10 |
| Galileo | 5 Whys | Il problema reale è la coverage dello spazio ipotetico, non la diversità di voci | 7/10 |
| Marco Polo | Opportunity Cost | Panel fisso = rigidità. Serve selezione dinamica degli archetipi | 7/10 |
| Pinocchio | Fresh Eyes | "Elaborate way to feel rigorous." Self-Consistency è più semplice e competitiva | 7/10 |
| Brunelleschi | Monday Morning | Servono dati: 5 casi reali, baseline comparison, timing | 7/10 |
| Falcone | ACH | H2 (parzialmente efficace) sopravvive alla matrice evidenziale. H1 (sufficiente) eliminata | 7/10 |

### Fase 3 — Peer Review anonima
Risposte anonimizzate (A-F, ordine randomizzato) e revisionate da 6 reviewer indipendenti.

**Risultati chiave:**
- Savonarola votato più forte da tutti 6 reviewer
- Disaccordo principale: Pinocchio ("teatro del rigore") vs Falcone/Galileo ("parzialmente efficace, fixable")
- Punto cieco collettivo: nessuno ha analizzato il Chairman come single point of failure
- Confidenze troppo raggruppate a 7/10 — segnale di anchoring

### Fase 4 — Dibattito
Ogni consigliere ha risposto alle critiche con Concedi/Difendi/Aggiorna.

| Consigliere | Prima | Dopo | Movimento |
|-------------|-------|------|-----------|
| Savonarola | 8/10 | 7/10 | ↓ Concede H2 sopravvive |
| Galileo | 7/10 | 7/10 | → Difende reframe |
| Marco Polo | 7/10 | 5/10 | ↓↓ Visione 10x prematura |
| Pinocchio | 7/10 | 8/10 | ↑ Argomento rafforzato |
| Brunelleschi | 7/10 | 6/10 | ↓ Non aveva letto il Chairman |
| Falcone | 7/10 | 5/10 | ↓↓ Concede circolarità ACH |

### Fase 5 — Lo Scettico (Red Team)
Machiavelli ha attaccato la raccomandazione emergente:

> "La raccomandazione è auto-sigillante. Sei archetipi hanno dibattuto e sono atterrati su 'tieni la struttura, aggiungi più struttura.' La cura è più della malattia. Il Conclave non ha trovato groupthink — è groupthink, architetturalmente garantito."

**Esito:** Superato — il punto sul high-confidence coordinated failure è stato riconosciuto valido da Salomone.

### Fase 6 — Verdetto di Salomone
Sintesi finale pesata per confidenza di tutte le fasi.

---

## Conclusioni

### Verdetto
**Il Conclave è parzialmente efficace (H2): aggiunge valore su single-shot ma è incompleto.**

Sovradimensionato rispetto alle evidenze disponibili (nessun benchmark), sottodimensionato rispetto ai rischi identificati (Chairman come bottleneck, high-confidence coordinated failure).

### Cosa funziona
- I framework analitici forzati producono divergenza reale (confermato da ricerca DMAD +4-6%)
- Il dibattito ha generato movimento genuino nelle confidenze (da 7-8 uniforme a range 5-8)
- Il Red Team ha trovato un rischio strutturale che il council aveva sottovalutato
- La peer review ha scoperto punti ciechi collettivi (Chairman, baseline mancante)

### Cosa non funziona
- Il sistema non ha mai chiesto "rispetto a cosa?" — manca un baseline di confronto
- Il Chairman (Salomone) è il componente non scrutinato di un sistema costruito per scrutinare
- L'etichetta "council" inflaziona le aspettative: è analisi strutturata da modello singolo, non ensemble indipendente
- Le confidenze iniziali erano troppo raggruppate (anchoring a 7/10)

### Le tre azioni raccomandate
1. **Scrutinare il prompt del Chairman** — è il single point of failure
2. **Benchmark empirico** — 5 casi reali, Conclave vs single-shot vs Self-Consistency
3. **Etichettatura onesta** — dichiarare i limiti del single-model nell'output

### Confidenza complessiva: 6.5/10

---

## Allegati

- [Report visivo completo](council-report-20260430.html)
- [Transcript completo di tutte le fasi](council-transcript-20260430.md)
