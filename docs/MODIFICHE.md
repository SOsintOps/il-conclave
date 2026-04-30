# Modifiche rispetto agli originali

Questo documento dettaglia tutte le differenze tra Il Conclave e le due fonti originali.

## Fonti

| Progetto | Autore | Approccio |
|----------|--------|-----------|
| [LLM Council](https://github.com/karpathy/llm-council) | Andrej Karpathy | Multi-modello (GPT, Gemini, Claude via OpenRouter) |
| [llm-council-skill](https://github.com/tenfoldmarc/llm-council-skill) | tenfoldmarc | Single-model (Claude, sub-agent con lenti diverse) |
| **Il Conclave** | Sandro Rossetti | Single-model procedurale (Claude, framework forzati + dibattito + Steelman-then-Attack) |

## Il problema di fondo

Il council di Karpathy funziona bene perché usa modelli diversi: GPT ha punti ciechi diversi da Gemini, che ha punti ciechi diversi da Claude. La diversità è strutturale.

Quando tenfoldmarc ha portato il concetto in un singolo modello, i 5 advisor condividono lo stesso "cervello." La diversità diventa superficiale: stessi pregiudizi, stesse lacune, stessa tendenza a convergere. La ricerca (DMAD, ICLR 2025) conferma che team di agenti LLM basati sullo stesso modello con prompt di sola persona tendono a duplicare sforzi e produrre inconsistenze.

Il Conclave affronta questo problema con un approccio procedurale: la divergenza viene dai framework analitici, non dalle personas.

## Modifica 1: Procedure, non personas

**Originale (tenfoldmarc):** Ogni advisor ha una descrizione del proprio "stile di pensiero" (es. "il Contrarian cerca cosa c'è di sbagliato"). Il ragionamento è libero.

**Il Conclave:** Ogni advisor riceve istruzioni procedurali con step obbligatori e output strutturato. I nomi italiani sono etichette mnemoniche, non istruzioni di personalità.

| Advisor | Framework | Output procedurale obbligatorio |
|---------|-----------|--------------------------------|
| Savonarola | Pre-Mortem | 3 modalità di fallimento, segnali ignorati, assunzione fatale, azione retrospettiva |
| Galileo | 5 Whys + Mappa Vincoli | Catena dei 5 perché, problema radice, vincoli reali vs. assunti, riformulazione |
| Marco Polo | Matrice Costo Opportunità | Costi espliciti, valore opzionale, alternative comparative, versione 10x |
| Falcone | ACH | Ipotesi concorrenti, matrice evidenziale, score di sopravvivenza, evidenza diagnostica mancante |

Perché funziona: un Pre-Mortem forza ragionamento pessimistico all'indietro. I 5 Whys forzano profondità causale. La Matrice Costo Opportunità forza pensiero comparativo. L'ACH forza pensiero per disconfirma su ipotesi multiple. Sono percorsi di ragionamento strutturalmente incompatibili, non solo "atteggiamenti diversi."

Ricerca a supporto: DMAD (ICLR 2025) dimostra che framework forzati producono +4-6% di accuratezza rispetto a differenziazione per sola persona in contesti single-model.

## Modifica 2: 4 advisor, non 5-6

**Originale (tenfoldmarc):** 5 advisor.

**Il Conclave v0.1:** 6 advisor + 2 agenti speciali.

**Il Conclave v0.2:** 4 advisor procedurali + 1 sfidante + 1 sintesi.

La ricerca mostra diminishing returns netti dopo 3-4 agenti in contesti omogenei (DMAD, ICLR 2025). Più agenti dallo stesso modello = più ridondanza retorica, non più diversità. 4 framework ortogonali coprono lo spazio decisionale senza inflazione.

## Modifica 3: Confidence scoring

**Originale:** Nessun meccanismo di pesatura. Tutte le opinioni hanno lo stesso peso nel verdetto finale.

**Il Conclave:** Ogni advisor assegna un punteggio di confidenza (1-10) con:
- Livello di confidenza numerico
- L'incertezza principale (cosa potrebbe rendere sbagliata l'analisi)
- Quale dato cambierebbe la conclusione

Salomone (chairman) usa questi punteggi per pesare le opinioni. In un council single-model, il confidence scoring è anche un indicatore di groupthink: se tutti danno 9/10, è un segnale d'allarme, non di sicurezza.

Ricerca a supporto: Confidence-Weighted Majority Voting (CWMV, ACL 2025) supera il majority voting semplice.

## Modifica 4: Round di dibattito

**Originale:** Fase 1 (advisor) → Fase 2 (peer review) → Fase 3 (sintesi). Nessuna possibilità di rispondere alle critiche.

**Il Conclave:** Aggiunge un round di dibattito. Dopo la peer review, ogni advisor:
1. **CONCEDE** — Quali critiche sono valide? Cosa ha mancato?
2. **DIFENDE** — Cosa mantiene nonostante le critiche? Perché?
3. **AGGIORNA** — La raccomandazione cambia? Come?
4. **Confidenza aggiornata** — È salita o scesa dopo aver visto le altre prospettive?

Perché funziona: cattura il "falso consenso" — il problema dove un singolo modello produce risposte che sembrano diverse ma concordano su tutto. Il dibattito forza un engagement esplicito con i disaccordi.

## Modifica 5: Steelman-then-Attack

**Originale:** Nessun meccanismo adversariale dedicato.

**Il Conclave v0.1:** Red Team puro (Lo Scettico attacca direttamente).

**Il Conclave v0.2:** Steelman-then-Attack. Machiavelli deve prima articolare la versione più forte della raccomandazione, poi tentare di distruggerla.

Perché il cambiamento: la ricerca (Nature 2026) mostra che un singolo agente adversariale puro può abbassare l'accuratezza del 10-40%. Il formato Steelman-then-Attack mantiene la funzione critica ma riduce il rischio di degradazione. Machiavelli è costretto a dimostrare di aver capito la raccomandazione prima di attaccarla.

Se Machiavelli non trova falle significative dopo il steelman, lo dichiara onestamente. Un "non ho trovato nulla" dopo un tentativo serio è più prezioso di un'obiezione forzata.

## Modifica 6: Identità italiana degli archetipi

**Originale:** Nomi generici in inglese (Contrarian, First Principles Thinker, ecc.).

**Il Conclave:** Archetipi italiani con soprannomi che riflettono la funzione:
- Savonarola — predicava la rovina di Firenze prima che arrivasse (Pre-Mortem)
- Galileo — "eppur si muove", rimetteva in discussione tutto (5 Whys)
- Marco Polo — andò dove nessuno era andato, vide opportunità nel vuoto (Opportunity Cost)
- Falcone — smantellò Cosa Nostra incrociando evidenze contro ipotesi concorrenti (ACH)
- Machiavelli — analizza il potere e le debolezze senza pietà (Steelman-then-Attack)
- Salomone — il re saggio che taglia il nodo (Sintesi pesata)

I prompt interni restano in inglese per massimizzare l'efficienza del modello. I nomi italiani sono per l'identità del progetto e la leggibilità del report.

## Modifica 7: Report con verdetto immediato

**Originale:** Report HTML con sezioni collassabili per ogni advisor e il verdetto del chairman.

**Il Conclave:** Aggiunge una hero section in cima al report che mostra immediatamente:
- Score di confidenza complessivo
- Verdetto in una riga
- Prima azione da fare
- Dashboard con confidenza prima/dopo dibattito per ogni advisor
- Codifica colore: verde (7+), giallo (4-6), rosso (1-3)
- Stato Machiavelli: Superato/Fallito

## Riepilogo delle fasi

| Fase | Originale Karpathy | Originale tenfoldmarc | Il Conclave |
|------|--------------------|-----------------------|-------------|
| 1. Contesto | — | Scan workspace | Scan workspace |
| 2. Framing | Domanda diretta | Riformulazione | Riformulazione |
| 3. Advisor | Multi-modello, liberi | Single-model, 5 advisor liberi | Single-model, 4 advisor procedurali con framework forzati + confidenza |
| 4. Peer Review | Anonima | Anonima | Anonima |
| 5. Dibattito | — | — | Concedi/Difendi/Aggiorna |
| 6. Sfida | — | — | Steelman-then-Attack |
| 7. Sintesi | Chairman | Chairman | Salomone (pesato per confidenza) |
| 8. Output | Web app | HTML + MD | HTML con hero + dashboard + MD |
