# Il Conclave

**Un consiglio di 8 archetipi AI che analizza, dibatte e demolisce le tue decisioni prima che sia troppo tardi.**

Il Conclave prende una domanda, un'idea o una decisione e la passa attraverso 6 consiglieri indipendenti, una peer review anonima, un round di dibattito, un attacco Red Team e una sintesi finale pesata per confidenza. Il tutto usando un singolo modello LLM.

Questo progetto nasce dallo studio della metodologia [LLM Council di Andrej Karpathy](https://github.com/karpathy/llm-council) e della sua [adattazione come skill per Claude](https://github.com/tenfoldmarc/llm-council-skill) di tenfoldmarc. Il Conclave estende entrambi con modifiche pensate per compensare il limite principale dell'approccio single-model: la mancanza di vera diversità tra gli advisor.

---

## Gli Otto Archetipi

| Archetipo | Ruolo | Framework | Soprannome |
|-----------|-------|-----------|------------|
| [**L'Avvocato del Diavolo**](docs/archetipi/savonarola.md) | Assume che la decisione sia già fallita e spiega perché | [Pre-Mortem](docs/framework/pre-mortem.md) | *Savonarola* |
| [**Il Filosofo**](docs/archetipi/galileo.md) | Scava fino alla radice del problema reale | [5 Whys + Vincoli](docs/framework/5-whys.md) | *Galileo* |
| [**L'Esploratore**](docs/archetipi/marco-polo.md) | Cerca l'upside che tutti gli altri ignorano | [Matrice Costo Opportunità](docs/framework/opportunity-cost.md) | *Marco Polo* |
| [**Lo Straniero**](docs/archetipi/pinocchio.md) | Vede quello che gli esperti non vedono più | [Test dell'Ingenuo](docs/framework/fresh-eyes.md) | *Pinocchio* |
| [**Il Capomastro**](docs/archetipi/brunelleschi.md) | Trasforma le idee in azioni concrete entro 72 ore | [Piano Lunedì Mattina](docs/framework/monday-morning.md) | *Brunelleschi* |
| [**L'Investigatore**](docs/archetipi/falcone.md) | Genera ipotesi concorrenti e le valuta contro le evidenze | [ACH](docs/framework/ach.md) | *Falcone* |
| [**Lo Scettico**](docs/archetipi/machiavelli.md) | Tenta di distruggere la raccomandazione emergente | [Red Team](docs/framework/red-team.md) | *Machiavelli* |
| [**Il Giudice**](docs/archetipi/salomone.md) | Sintetizza il verdetto finale pesando la confidenza | [Sintesi pesata](docs/framework/confidence-weighted.md) | *Salomone* |

## Come Funziona

```
Domanda dell'utente
       │
       ▼
┌──────────────┐
│  Scansione   │  Cerca contesto nel workspace (CLAUDE.md, memory/, ecc.)
│  Contesto    │
└──────┬───────┘
       │
       ▼
┌──────────────┐
│   Framing    │  Riformula la domanda in modo neutro e completo
│   Domanda    │
└──────┬───────┘
       │
       ▼
┌───────────────────────────────────────────────────────────────┐
│                 6 Consiglieri in Parallelo                     │
│  Avvocato │ Filosofo │ Esploratore │ Straniero │ Capomastro │ Investigatore │
│  + Confidenza 1-10 per ciascuno                               │
└──────────────────────────┬────────────────────────────────────┘
                   │
                   ▼
┌──────────────────────────────────────────────────┐
│           Peer Review Anonima                     │
│  Risposte anonimizzate A-E, ordine randomizzato  │
└──────────────────┬───────────────────────────────┘
                   │
                   ▼
┌──────────────────────────────────────────────────┐
│           Round di Dibattito                      │
│  Ogni consigliere: CONCEDI / DIFENDI / AGGIORNA  │
│  + Confidenza aggiornata                         │
└──────────────────┬───────────────────────────────┘
                   │
                   ▼
┌──────────────────────────────────────────────────┐
│           Lo Scettico (Red Team)                  │
│  Attacca la raccomandazione emergente             │
└──────────────────┬───────────────────────────────┘
                   │
                   ▼
┌──────────────────────────────────────────────────┐
│           Il Giudice (Sintesi Finale)             │
│  Verdetto pesato per confidenza                  │
│  + Dashboard di confidenza                       │
└──────────────────┬───────────────────────────────┘
                   │
                   ▼
        Report HTML + Transcript MD
```

## Cosa Cambia Rispetto agli Originali

Questo skill introduce quattro miglioramenti specifici per compensare l'uso di un singolo modello. Il dettaglio completo è in [`docs/MODIFICHE.md`](docs/MODIFICHE.md).

1. **Framework analitici forzati** — Ogni consigliere segue una metodologia strutturata specifica, non solo un "atteggiamento diverso"
2. **Confidence scoring** — Punteggio 1-10 con incertezza esplicita, usato dal Giudice per pesare le opinioni
3. **Round di dibattito** — I consiglieri rispondono alle critiche: concedono, difendono o aggiornano la posizione
4. **Red Team (Lo Scettico)** — Un agente dedicato tenta di demolire la raccomandazione prima della sintesi

## Installazione

Scarica il file `il-conclave.skill` dalla [pagina Releases](../../releases) e installalo trascinandolo in Claude.

In alternativa, copia la cartella `skill/` nella directory dei tuoi skill.

## Uso

Usa una delle frasi trigger nella chat:

- *"council this: [la tua domanda]"*
- *"conclave: [la tua domanda]"*
- *"pressure-test this: [la tua domanda]"*
- *"stress-test this: [la tua domanda]"*
- *"debate this: [la tua domanda]"*

Il Conclave funziona al meglio con domande dove sbagliare costa caro: scelte di architettura, pricing, pivot strategici, decisioni di assunzione, direzione di prodotto.

**Non usarlo per:** domande con una sola risposta corretta, task creativi, riassunti.

## Output

Ogni sessione produce due file:

| File | Descrizione |
|------|-------------|
| `council-report-[timestamp].html` | Report visivo con dashboard di confidenza, pensato per essere scannerizzato rapidamente |
| `council-transcript-[timestamp].md` | Transcript completo di tutte le fasi, utile per riferimento futuro |

## Fonti e Attribuzioni

Questo progetto si basa sul lavoro di:

- **Andrej Karpathy** — [LLM Council](https://github.com/karpathy/llm-council) — L'idea originale: sottoporre una domanda a più LLM, farli peer-revieware anonimamente, e sintetizzare con un chairman. Usa modelli diversi (GPT, Gemini, Claude, ecc.) tramite OpenRouter.

- **tenfoldmarc** — [llm-council-skill](https://github.com/tenfoldmarc/llm-council-skill) — L'adattamento come skill per Claude Code. Porta il concetto di council dentro un singolo modello usando sub-agent con "lenti di pensiero" diverse. Introduce i 5 advisor (Contrarian, First Principles, Expansionist, Outsider, Executor) e il formato report HTML + transcript MD.

Il Conclave parte dal lavoro di tenfoldmarc e aggiunge le modifiche documentate in [`docs/MODIFICHE.md`](docs/MODIFICHE.md).

## Stato del Progetto

Questo è un **progetto di studio e sperimentazione**. Leggi [`docs/VIBE-CODING.md`](docs/VIBE-CODING.md) per capire cosa significa in pratica.

In sintesi: il supporto è discontinuo, le modifiche arrivano quando arrivano, e l'obiettivo principale è imparare — non fornire un prodotto stabile. Le contribuzioni sono benvenute con questo spirito.

## Licenza

[MIT](LICENSE)
