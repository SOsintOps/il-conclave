# Modifiche rispetto agli originali

Questo documento dettaglia tutte le differenze tra Il Conclave e le due fonti originali.

## Fonti

| Progetto | Autore | Approccio |
|----------|--------|-----------|
| [LLM Council](https://github.com/karpathy/llm-council) | Andrej Karpathy | Multi-modello (GPT, Gemini, Claude via OpenRouter) |
| [llm-council-skill](https://github.com/tenfoldmarc/llm-council-skill) | tenfoldmarc | Single-model (Claude, sub-agent con lenti diverse) |
| **Il Conclave** | Sandro Rossetti | Single-model potenziato (Claude, framework forzati + dibattito + Red Team) |

## Il problema di fondo

Il council di Karpathy funziona bene perché usa modelli diversi: GPT ha punti ciechi diversi da Gemini, che ha punti ciechi diversi da Claude. La diversità è strutturale.

Quando tenfoldmarc ha portato il concetto in un singolo modello, i 5 advisor condividono lo stesso "cervello." La diversità diventa superficiale: stessi pregiudizi, stesse lacune, stessa tendenza a convergere. Un paper ACL 2025 conferma che team di agenti LLM basati sullo stesso modello con prompt diversi tendono a duplicare sforzi e produrre inconsistenze, a differenza di team con vera diversità di addestramento.

Il Conclave affronta questo problema con quattro interventi specifici.

## Modifica 1: Framework analitici forzati

**Originale (tenfoldmarc):** Ogni advisor ha una descrizione del proprio "stile di pensiero" (es. "il Contrarian cerca cosa c'è di sbagliato"). Il ragionamento è libero.

**Il Conclave:** Ogni consigliere deve seguire un framework strutturato con output specifici:

| Consigliere | Framework | Output obbligatorio |
|-------------|-----------|---------------------|
| L'Avvocato del Diavolo | Pre-Mortem | 3 modalità di fallimento, segnali ignorati, assunzione fatale |
| Il Filosofo | 5 Whys + Mappa Vincoli | Catena dei perché, vincoli reali vs. assunti, riformulazione |
| L'Esploratore | Matrice Costo Opportunità | Costi espliciti, valore opzionale, versione 10x |
| Lo Straniero | Test dell'Ingenuo | Cosa confonde, gergo presupposto, reazione di pancia |
| Il Capomastro | Piano Lunedì Mattina | Prima azione concreta, prime 72 ore, test minimo |

Perché funziona: un Pre-Mortem forza ragionamento pessimistico all'indietro. I 5 Whys forzano profondità. La Matrice Costo Opportunità forza pensiero comparativo. Sono percorsi di ragionamento strutturalmente incompatibili, non solo "atteggiamenti diversi."

## Modifica 2: Confidence scoring

**Originale:** Nessun meccanismo di pesatura. Tutte le opinioni hanno lo stesso peso nel verdetto finale.

**Il Conclave:** Ogni consigliere assegna un punteggio di confidenza (1-10) con:
- Livello di confidenza numerico
- L'incertezza principale (cosa potrebbe rendere sbagliata l'analisi)
- Quale dato cambierebbe la conclusione

Il Giudice (chairman) usa questi punteggi per pesare le opinioni. Se tre consiglieri ad alta confidenza concordano e due a bassa confidenza dissentono, il peso è diverso da uno scenario 3 vs 2 senza distinzione.

In un council single-model, il confidence scoring è anche un indicatore di groupthink: se tutti danno 9/10, è un segnale d'allarme, non di sicurezza.

## Modifica 3: Round di dibattito

**Originale:** Fase 1 (advisor) → Fase 2 (peer review) → Fase 3 (sintesi). Nessuna possibilità di rispondere alle critiche.

**Il Conclave:** Aggiunge una Fase 3.5 — il dibattito. Dopo la peer review, ogni consigliere:
1. **CONCEDE** — Quali critiche sono valide? Cosa ha mancato?
2. **DIFENDE** — Cosa mantiene nonostante le critiche? Perché?
3. **AGGIORNA** — La raccomandazione cambia? Come?
4. **Confidenza aggiornata** — È salita o scesa dopo aver visto le altre prospettive?

Perché funziona: cattura il "falso consenso" — il problema dove un singolo modello produce 5 risposte che sembrano diverse ma concordano su tutto. Il dibattito forza un engagement esplicito con i disaccordi.

## Modifica 4: Red Team (Il Sabotatore)

**Originale:** Nessun meccanismo adversariale dedicato.

**Il Conclave:** Dopo il dibattito, un agente dedicato (Il Sabotatore) ha un solo compito: distruggere la raccomandazione emergente. Cerca:
- Lo scenario peggiore realistico
- L'assunzione condivisa che potrebbe essere sbagliata
- Un approccio radicalmente diverso che nessuno ha considerato
- Segni di groupthink

Se Il Sabotatore non trova falle significative, lo dichiara onestamente. Un "non ho trovato nulla" dopo un tentativo serio è più prezioso di un'obiezione forzata.

Il Red Team è più importante quando tutti concordano. L'unanimità in un council single-model è una bandiera gialla, non verde.

## Modifica 5: Identità italiana degli archetipi

**Originale:** Nomi generici in inglese (Contrarian, First Principles Thinker, ecc.).

**Il Conclave:** Archetipi italiani con nomi e soprannomi che riflettono la funzione:
- L'Avvocato del Diavolo ("Il Gufo")
- Il Filosofo ("Maestro dei Perché")
- L'Esploratore ("L'Orizzonte")
- Lo Straniero ("Occhi Nuovi")
- Il Capomastro ("Mani in Pasta")
- Il Sabotatore ("La Mina")
- Il Giudice ("La Bilancia")

I prompt interni restano in inglese per massimizzare l'efficienza del modello. I nomi italiani sono per l'identità del progetto e la leggibilità del report.

## Modifica 6: Dashboard di confidenza nel report

**Originale:** Report HTML con sezioni collassabili per ogni advisor e il verdetto del chairman.

**Il Conclave:** Aggiunge una dashboard visiva che mostra:
- Confidenza iniziale → confidenza post-dibattito per ogni consigliere (con freccia di direzione)
- Codifica colore: verde (7+), giallo (4-6), rosso (1-3)
- Stato Red Team: Superato/Fallito
- Confidenza complessiva del Conclave

## Riepilogo delle fasi

| Fase | Originale Karpathy | Originale tenfoldmarc | Il Conclave |
|------|--------------------|-----------------------|-------------|
| 1. Contesto | — | Scan workspace | Scan workspace |
| 2. Framing | Domanda diretta | Riformulazione | Riformulazione |
| 3. Advisor | Multi-modello, liberi | Single-model, liberi | Single-model, framework forzati + confidenza |
| 4. Peer Review | Anonima | Anonima | Anonima |
| 5. Dibattito | — | — | Concedi/Difendi/Aggiorna |
| 6. Red Team | — | — | Il Sabotatore |
| 7. Sintesi | Chairman | Chairman | Il Giudice (pesato per confidenza) |
| 8. Output | Web app | HTML + MD | HTML con dashboard + MD |
