# Il Conclave

**Un consiglio di 4 procedure analitiche forzate che analizza, dibatte e demolisce le tue decisioni prima che sia troppo tardi.**

Il Conclave prende una domanda, un'idea o una decisione e la passa attraverso 4 advisor indipendenti — ciascuno con un framework analitico strutturato — una peer review anonima, un round di dibattito, un attacco Steelman-then-Attack e una sintesi finale pesata per confidenza. Il tutto usando un singolo modello LLM.

Questo progetto nasce dallo studio della metodologia [LLM Council di Andrej Karpathy](https://github.com/karpathy/llm-council) e della sua [adattazione come skill per Claude](https://github.com/tenfoldmarc/llm-council-skill) di tenfoldmarc. Il Conclave estende entrambi con modifiche pensate per compensare il limite principale dell'approccio single-model: la mancanza di vera diversità tra gli advisor.

**Principio chiave:** la divergenza viene dalle procedure, non dalle personas. Ogni advisor segue un framework analitico con output strutturato obbligatorio. I nomi italiani sono etichette mnemoniche, non istruzioni di personalità.

---

## I Sei Archetipi

| Soprannome | Framework | Ruolo |
|------------|-----------|-------|
| *Savonarola* | [Pre-Mortem](docs/framework/pre-mortem.md) | Assume che la decisione sia già fallita e spiega perché |
| *Galileo* | [5 Whys + Vincoli](docs/framework/5-whys.md) | Scava fino alla radice del problema reale |
| *Marco Polo* | [Matrice Costo Opportunità](docs/framework/opportunity-cost.md) | Cerca l'upside che tutti gli altri ignorano |
| *Falcone* | [ACH](docs/framework/ach.md) | Genera ipotesi concorrenti e le valuta contro le evidenze |
| *Machiavelli* | [Steelman-then-Attack](docs/framework/red-team.md) | Rafforza la raccomandazione, poi tenta di distruggerla |
| *Salomone* | [Sintesi pesata](docs/framework/confidence-weighted.md) | Sintetizza il verdetto finale pesando la confidenza |

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
┌───────────────────────────────────────────────────────────┐
│              4 Advisor Procedurali in Parallelo            │
│  Pre-Mortem │ 5 Whys │ Costo Opportunità │ ACH            │
│  + Confidenza 1-10 per ciascuno                           │
└──────────────────────────┬────────────────────────────────┘
                   │
                   ▼
┌──────────────────────────────────────────────────┐
│           Peer Review Anonima                     │
│  Risposte anonimizzate A-D, ordine randomizzato  │
└──────────────────┬───────────────────────────────┘
                   │
                   ▼
┌──────────────────────────────────────────────────┐
│           Round di Dibattito                      │
│  Ogni advisor: CONCEDI / DIFENDI / AGGIORNA      │
│  + Confidenza aggiornata                         │
└──────────────────┬───────────────────────────────┘
                   │
                   ▼
┌──────────────────────────────────────────────────┐
│           Machiavelli (Steelman-then-Attack)      │
│  Rafforza la raccomandazione, poi la attacca      │
└──────────────────┬───────────────────────────────┘
                   │
                   ▼
┌──────────────────────────────────────────────────┐
│           Salomone (Sintesi Finale)               │
│  Verdetto pesato per confidenza                  │
│  + Dashboard di confidenza                       │
└──────────────────┬───────────────────────────────┘
                   │
                   ▼
        Report HTML + Transcript MD
```

## Cosa Cambia Rispetto agli Originali

Questo skill introduce cinque miglioramenti specifici per compensare l'uso di un singolo modello. Il dettaglio completo è in [`docs/MODIFICHE.md`](docs/MODIFICHE.md).

1. **Procedure, non personas** — Ogni advisor segue step procedurali con output strutturato obbligatorio, non un "atteggiamento diverso"
2. **4 framework ortogonali** — Pre-Mortem, 5 Whys, Opportunity Cost, ACH: percorsi di ragionamento strutturalmente incompatibili
3. **Confidence scoring** — Punteggio 1-10 con incertezza esplicita, usato dal Giudice per pesare le opinioni
4. **Round di dibattito** — Gli advisor rispondono alle critiche: concedono, difendono o aggiornano la posizione
5. **Steelman-then-Attack** — L'agente adversariale deve prima rafforzare la raccomandazione, poi attaccarla. Riduce il rischio di degradazione da adversarial puro (-10/40%)

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
| `council-report-[timestamp].html` | Report visivo con verdetto immediato e dashboard di confidenza |
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
