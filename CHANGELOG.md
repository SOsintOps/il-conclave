# Changelog

Tutti i cambiamenti notevoli di questo progetto saranno documentati in questo file.

Il formato è basato su [Keep a Changelog](https://keepachangelog.com/it/1.1.0/),
e questo progetto aderisce al [Versionamento Semantico](https://semver.org/lang/it/).

## [0.2.0] - 2026-04-30

### Cambiato
- **Architettura procedurale:** prompt degli advisor riscritti come procedure con step obbligatori, non istruzioni di personalità
- **4 advisor invece di 6:** ridotto roster per evitare diminishing returns (ricerca DMAD, ICLR 2025)
- **Steelman-then-Attack:** Machiavelli deve prima rafforzare la raccomandazione, poi attaccarla (sostituisce Red Team puro)
- Report HTML con hero section per verdetto immediato
- Peer review con 4 risposte anonimizzate (A-D) invece di 6 (A-F)

### Rimosso
- Pinocchio (Lo Straniero / Fresh Eyes Test) — rimosso dal roster advisor
- Brunelleschi (Il Capomastro / Monday Morning Plan) — rimosso dal roster advisor
- Cartella esempio/ — verrà ricreata con nuovi esempi
- Schede archetype per personaggi rimossi
- Schede framework per metodologie rimosse (Fresh Eyes, Monday Morning)

## [0.1.0] - 2026-04-30

### Aggiunto
- Skill SKILL.md con il flusso completo del Conclave a 8 fasi
- 5 consiglieri con framework analitici forzati (Pre-Mortem, 5 Whys, Matrice Costo Opportunità, Test dell'Ingenuo, Piano Lunedì Mattina)
- Confidence scoring (1-10) con incertezza esplicita per ogni consigliere
- Round di dibattito post-peer-review (Concedi/Difendi/Aggiorna)
- Red Team (Lo Scettico) come fase adversariale dedicata
- Sintesi del Giudice pesata per confidenza con Dashboard
- Archetipi italiani con nomi e soprannomi
- Prompt degli agenti in inglese per massima efficienza del modello
- Documentazione completa in italiano
- File MODIFICHE.md con confronto dettagliato rispetto alle fonti originali
- File VIBE-CODING.md con filosofia e aspettative del progetto
- Template per issue (bug report e feature request)
- CONTRIBUTING.md e CODE_OF_CONDUCT.md
