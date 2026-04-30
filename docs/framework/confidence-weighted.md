# Confidence-Weighted Synthesis

> Non contare i voti. Pesa la certezza.

## Origini

La sintesi pesata per confidenza si fonda su due tradizioni convergenti:

### Teorema della Giuria di Condorcet (1785)
**Marie Jean Antoine Nicolas de Caritat, Marchese di Condorcet**, dimostrò nel 1785 che un gruppo di votanti che usa il voto a maggioranza ha più probabilità di scegliere l'opzione corretta rispetto a un singolo votante arbitrario — a patto che ogni votante abbia individualmente più del 50% di probabilità di avere ragione.

**Nitzan e Paroush (1982)** e **Shapley e Grofman (1984)** hanno esteso il teorema dimostrando che la regola decisionale collettiva ottimale assegna **pesi maggiori ai votanti con maggiore capacità di fare la scelta corretta**.

### Confidence-Weighted Majority Voting (CWMV)
Ricerca pubblicata in *Cognitive Research: Principles and Implications* (2021) ha dimostrato che il voto a maggioranza pesato per confidenza (CWMV) è **teoricamente ottimale** quando sono disponibili valutazioni di confidenza accurate e indipendenti da parte dei singoli membri del gruppo.

I risultati chiave:
- Decisioni di gruppo simulate con CWMV hanno eguagliato l'accuratezza delle decisioni di gruppo reali
- Decisioni simulate con voto a maggioranza semplice (MV) hanno mostrato accuratezza inferiore
- I gruppi reali tendono a pesare i voti individuali in modo più egualitario di quanto il CWMV suggerisca

## Come funziona nel Conclave

Salomone (Il Giudice) applica la sintesi pesata per confidenza usando:

### Punteggi di confidenza (1-10)
Ogni consigliere assegna un punteggio con:
- **Livello numerico** — 1 ("sto tirando a indovinare") a 10 ("ci scommetterei lo stipendio")
- **Incertezza chiave** — la singola cosa che potrebbe rendere sbagliata l'analisi
- **Dato che cambierebbe idea** — informazione specifica che capovolgerebbe la raccomandazione

### Confidenza aggiornata post-dibattito
Dopo la peer review e il dibattito, ogni consigliere aggiorna il proprio punteggio. La direzione del cambiamento (↑/↓/→) è informativa quanto il numero:
- **Confidenza che sale:** Il consigliere ha visto conferme dalle altre prospettive
- **Confidenza che scende:** Le critiche erano valide, la posizione è meno solida
- **Confidenza stabile:** Le critiche non hanno cambiato la sostanza

### Pesatura nella sintesi
Salomone pesa le posizioni in base alla confidenza:
- Tre consiglieri a confidenza 8-9 che concordano pesano più di cinque a 4-5
- Un dissenziente a confidenza 9 contro quattro a 5 merita attenzione seria
- Unanimità a 9/10 in un council single-model è sospetta — la vera incertezza produce varianza

## Perché funziona nel contesto single-model

In un council multi-modello (come l'originale di Karpathy), la diversità è strutturale: GPT ha bias diversi da Gemini che ha bias diversi da Claude. In un council single-model, il confidence scoring è il meccanismo principale per distinguere accordo genuino da eco dello stesso modello.

Se tutti i consiglieri danno 9/10, non è un segnale di sicurezza — è un segnale d'allarme.

## Fonti

- [Group decisions based on confidence weighted majority voting](https://pmc.ncbi.nlm.nih.gov/articles/PMC7960862/) — PMC / Cognitive Research, 2021
- [Condorcet method — Wikipedia](https://en.wikipedia.org/wiki/Condorcet_method) — Storia e contesto
- [Weighted Majority Voting Overview](https://www.emergentmind.com/topics/weighted-majority-voting-wmv) — Emergent Mind
- [A generalization of Condorcet's Jury Theorem](https://www.researchgate.net/publication/24057519_A_generalization_of_Condorcet's_Jury_Theorem_to_weighted_voting_games_with_many_small_voters) — ResearchGate
