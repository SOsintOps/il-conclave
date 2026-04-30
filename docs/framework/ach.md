# Analysis of Competing Hypotheses (ACH)

> Non confermare la tua ipotesi preferita. Cerca di smentirle tutte.

## Origini

L'ACH è stata sviluppata da **Richards J. Heuer, Jr.**, veterano della CIA, e pubblicata nel suo libro *Psychology of Intelligence Analysis* (Center for the Study of Intelligence, CIA, 1999). Il metodo nasce dalla necessità degli analisti di intelligence di lavorare con informazioni incomplete, ambigue e talvolta deliberatamente fuorvianti.

Heuer ha progettato l'ACH per contrastare i bias cognitivi più pericolosi nell'analisi di intelligence: la tendenza a cercare conferme per l'ipotesi preferita (confirmation bias) e l'ancoraggio alla prima spiegazione plausibile.

## Il processo in 8 fasi

L'ACH segue un protocollo strutturato:

1. **Identificare le ipotesi** — generare spiegazioni mutuamente esclusive. Più sono, meglio è. Includere ipotesi scomode o impopolari.
2. **Elencare evidenze e argomenti** — raccogliere tutto ciò che è rilevante, incluse assunzioni non verificate.
3. **Costruire la matrice** — ipotesi in colonna, evidenze in riga. Per ogni cella: Consistente (C), Inconsistente (I), o Non Applicabile (N/A).
4. **Raffinare la matrice** — rimuovere evidenze non diagnostiche (quelle consistenti con tutte le ipotesi non aiutano a distinguerle).
5. **Trarre conclusioni provvisorie** — tentare di **smentire** ipotesi, non di confermarne una. L'ipotesi con meno inconsistenze sopravvive.
6. **Analizzare la sensitività** — identificare evidenze critiche: se una singola evidenza venisse rimossa o cambiasse valutazione, la conclusione cambierebbe?
7. **Riportare conclusioni** — presentare tutte le ipotesi, spiegando perché ciascuna è stata accettata o rifiutata.
8. **Identificare milestone** — definire indicatori futuri che confermerebbero o confuterebbero la conclusione.

## La matrice evidenziale

Il cuore dell'ACH è la matrice. Esempio semplificato:

| Evidenza | H1: Competitor | H2: Bug interno | H3: Cambio mercato |
|----------|:-:|:-:|:-:|
| Calo improvviso vendite | C | C | C |
| Nessun deploy recente | N/A | I | N/A |
| Competitor ha lanciato prodotto simile | C | N/A | N/A |
| Trend di settore in calo | I | N/A | C |
| Feedback clienti: "prodotto rotto" | I | C | N/A |

**Evidenza diagnostica:** "Calo improvviso vendite" è consistente con tutte e tre — non aiuta. "Nessun deploy recente" è diagnostica: se vera, rende H2 meno probabile.

**Pesatura:** Ogni evidenza riceve un peso di credibilità e rilevanza (Low = 0.707, Medium = 1, High = 1.414). L'inconsistenza pesata determina il punteggio finale di ogni ipotesi.

## Principio chiave: disconfermare, non confermare

L'ACH inverte il ragionamento naturale. Invece di chiedersi *"quale evidenza supporta la mia ipotesi?"*, chiede *"quale evidenza è inconsistente con ciascuna ipotesi?"*. L'ipotesi che sopravvive è quella con meno inconsistenze — non quella con più conferme.

Come nota Heuer: trovare evidenze consistenti con un'ipotesi è facile e poco informativo. Trovare evidenze **inconsistenti** è ciò che discrimina.

## Caso di studio: WannaCry (2017)

Un'applicazione documentata dell'ACH è l'analisi dell'attacco ransomware WannaCry. Digital Shadows e l'analista Pasquale Stirparo hanno valutato 7 ipotesi concorrenti:

- H1: Criminale sofisticato motivato finanziariamente
- H2: Criminale non sofisticato motivato finanziariamente
- H3: Stato-nazione con operazione distruttiva
- H4: Stato-nazione per screditare NSA
- H5: Attore non attribuito che espone rete compromessa NSA
- H6: Shadow Brokers (validazione dei tool leakati)
- H7: Lazarus Group

L'analisi ACH ha identificato tre "perdenti chiari" (criminali sofisticati, stato-nazione distruttivo, Lazarus Group) e ha evidenziato H5 come più consistente con le evidenze disponibili.

L'ACH *"funziona meglio quando più analisti contribuiscono con le loro valutazioni"* — nel Conclave, gli altri consiglieri forniscono implicitamente prospettive aggiuntive che Falcone può incorporare nella matrice.

## Uso nel Conclave

**Falcone** (L'Investigatore) applica l'ACH alla domanda dell'utente. Genera ipotesi concorrenti, le valuta contro le evidenze disponibili, e identifica quale sopravvive alla disconfirma. Il suo contributo unico è forzare il Conclave a considerare spiegazioni alternative prima di convergere su una raccomandazione.

L'ACH è particolarmente prezioso in un council single-model: dove gli altri framework producono prospettive diverse sulla stessa ipotesi, l'ACH forza la generazione di **ipotesi diverse** — un livello aggiuntivo di divergenza strutturale.

## Fonti

- [Analysis of Competing Hypotheses — Part 1](https://isc.sans.edu/forums/diary/Analysis+of+Competing+Hypotheses+ACH+part+1/22460/) — SANS Internet Storm Center
- [ACH Part 2: WCry and Lazarus](https://isc.sans.edu/forums/diary/Analysis+of+Competing+Hypotheses+WCry+and+Lazarus+ACH+part+2/22470/) — SANS Internet Storm Center
- Richards J. Heuer, Jr. — *Psychology of Intelligence Analysis* — Center for the Study of Intelligence, CIA, 1999
