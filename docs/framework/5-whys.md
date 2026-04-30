# 5 Whys + Constraint Mapping

> Ignora la superficie. Chiedi "perché?" finché non trovi la radice.

## Origini

La tecnica dei **5 Whys** (5 Perché) è stata sviluppata da **Sakichi Toyoda** (1867–1930), fondatore di Toyota Industries. È diventata un componente centrale del **Toyota Production System (TPS)**, il sistema di produzione che ha rivoluzionato l'industria manifatturiera mondiale.

**Taiichi Ohno**, architetto del TPS, ha descritto i 5 Whys come *"la base dell'approccio scientifico di Toyota — ripetendo 'perché' cinque volte, la natura del problema e la sua soluzione diventano chiare."*

## Come funziona

Si parte dal problema osservato e si chiede "perché?" ripetutamente, usando ogni risposta come base per la domanda successiva:

1. **Perché il sito è lento?** → Il server impiega 8 secondi a rispondere
2. **Perché il server è lento?** → La query al database è troppo pesante
3. **Perché la query è pesante?** → Fa un full table scan su 50M di righe
4. **Perché fa un full scan?** → Manca un indice sulla colonna di filtro
5. **Perché manca l'indice?** → Non c'è un processo di review degli schemi in produzione

La risposta al quinto "perché" dovrebbe rivelare la causa radice — in questo caso, un problema di processo, non di codice.

## Constraint Mapping (estensione nel Conclave)

Il Conclave estende i 5 Whys con una mappatura dei vincoli:

- **Vincoli espliciti:** tempo, budget, competenze disponibili, mercato, regolatorio
- **Vincoli reali vs assunti:** quali sono inamovibili (leggi, fisica) e quali sono presupposti non verificati ("il CEO non accetterebbe mai")
- **Riformulazione:** basata sulla causa radice trovata, riformulare la domanda originale

## Perché funziona

I 5 Whys forzano **profondità verticale**. Dove il Pre-Mortem di Savonarola forza pessimismo e la Matrice di Marco Polo forza ampiezza comparativa, i 5 Whys di Galileo forzano un percorso diverso: scendere fino alla radice. Questi sono percorsi di ragionamento strutturalmente incompatibili.

## Limiti noti

La tecnica è stata criticata come strumento troppo basilare per analisi complesse. **Teruyuki Minoura**, ex managing director di Toyota Global Purchasing, la definì troppo semplice per analizzare cause radice alla profondità necessaria per risoluzioni definitive. Per problemi con cause multiple e interconnesse, strumenti come il diagramma di Ishikawa o l'analisi FMEA sono più appropriati.

## Uso nel Conclave

**Galileo** (Il Filosofo) applica i 5 Whys alla domanda dell'utente, poi mappa i vincoli e distingue quelli reali da quelli assunti. Il risultato è spesso una riformulazione della domanda originale: "Non stai cercando di decidere X — stai cercando di risolvere Y."

## Fonti

- [Five Whys — Wikipedia](https://en.wikipedia.org/wiki/Five_whys) — Storia e contesto
- [5 Whys Root Cause Analysis](https://www.toolshero.com/problem-solving/5-whys-analysis/) — Toolshero
- [How Toyota Utilizes the 5 Whys Method](https://www.orcalean.com/article/how-toyota-is-using-5-whys-method) — OrcaLean
- [Five Whys and Five Hows](https://asq.org/quality-resources/five-whys) — American Society for Quality
- [The power of 5 Whys](https://www.atlassian.com/incident-management/postmortem/5-whys) — Atlassian
