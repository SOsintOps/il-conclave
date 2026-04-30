# Steelman-then-Attack (Red Team)

> Prima dimostra di aver capito. Poi distruggi.

## Origini

Il Red Teaming nasce dai **war game tattici dell'esercito prussiano** nel primo Ottocento, evolvendosi attraverso le simulazioni della Guerra Fredda fino alla metodologia formalizzata di oggi.

Il termine "Red Team" ha origine negli anni '60 negli Stati Uniti. Il concetto specifico di red team e blue team è emerso con la **RAND Corporation**, che conduceva simulazioni per il Pentagono durante la Guerra Fredda: il "red team" rappresentava l'Unione Sovietica, il "blue team" gli Stati Uniti.

## Formalizzazione militare

Dopo i fallimenti di intelligence che portarono agli attacchi dell'11 settembre 2001, il **Defense Science Review Board** nel 2003 raccomandò un uso molto più frequente del Red Teaming nelle forze armate statunitensi. L'obiettivo: prevenire i *"fallimenti di immaginazione"* che avevano permesso gli attacchi.

L'**University of Foreign Military and Cultural Studies** (UFMCS) a Fort Leavenworth, Kansas — creata dopo i fallimenti di intelligence in Iraq — ha sviluppato il framework moderno per il Red Teaming. Ha trasformato una pratica ad-hoc in una **metodologia sistematica per l'analisi critica**, insegnando a ufficiali militari e funzionari governativi tecniche per mettere in discussione le assunzioni, considerare prospettive alternative e introdurre pensiero contrarian nei processi di pianificazione.

## Come funziona

Il Red Team opera con un mandato chiaro: **trovare le falle che il consenso di gruppo ha nascosto.** Gli strumenti:

- **Scenario peggiore realistico** — non catastrofismo gratuito, ma il peggior esito plausibile
- **Assunzioni non verificate** — cosa stanno assumendo tutti come vero senza prove?
- **Alternative radicali** — esiste un approccio completamente diverso che nessuno ha considerato?
- **Check groupthink** — il gruppo sta evitando una verità scomoda per comodità sociale?
- **Voci ostili** — cosa direbbe chi ha interesse a vederti fallire?

## Perché funziona

Il Red Team contrasta due bias critici:

- **Groupthink (Janis, 1972):** I gruppi coesi tendono a sopprimere il dissenso per mantenere l'armonia. Il Red Team ha il *permesso esplicito* di dissentire.
- **Confirmation bias:** Una volta che una direzione è stata scelta, il gruppo cerca inconsciamente conferme. Il Red Team cerca deliberatamente confutazioni.

In un council single-model come Il Conclave, il Red Team è ancora più importante: l'unanimità di 5 consiglieri generati dallo stesso modello è una bandiera gialla, non verde.

## Steelman-then-Attack

Il Conclave v0.2 evolve il Red Team puro in un formato **Steelman-then-Attack**. La ricerca (Nature 2026) mostra che un singolo agente adversariale puro può abbassare l'accuratezza del 10-40%. Il formato in due fasi mitiga questo rischio:

1. **Fase Steelman:** L'agente articola la versione più forte possibile della raccomandazione — migliore di come l'hanno formulata gli advisor. Questo forza comprensione genuina e previene attacchi a strawman.
2. **Fase Attack:** Solo dopo aver dimostrato di aver capito, l'agente attacca. L'attacco è più preciso perché parte dalla versione più forte, non da una caricatura.

Un "I couldn't break it" dopo un steelman serio è il segnale più forte che il Conclave può produrre.

## Uso nel Conclave

**Machiavelli** (Lo Scettico) esegue lo Steelman-then-Attack nella Fase 5. Non partecipa alle fasi precedenti — entra solo dopo che il consenso si è formato. Se non trova falle significative dopo il steelman, lo dichiara onestamente.

## Fonti

- [Red Team — Wikipedia](https://en.wikipedia.org/wiki/Red_team) — Storia e contesto
- [What Is Red Teaming?](https://www.redteamthinking.com/what-is-red-teaming) — Red Team Thinking
- [Red Teaming: History, Methodology, and Best Practices](https://www.sprocketsecurity.com/blog/red-teaming-best-practices) — Sprocket Security
- [Red Teaming is a Critical Thinking Exercise](https://avidml.org/blog/red-teaming-2/) — AVID
