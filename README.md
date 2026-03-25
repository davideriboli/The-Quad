# Quadrat I + II — Samuel Beckett (1981)

**Implementazione digitale dell'opera televisiva di Samuel Beckett, fedele alla partitura originale.**

Vista dall'alto. Quattro cerchi colorati in movimento su un quadrato nero. Il centro — la *danger zone* — sempre evitato. Centomila anni dopo, tutto rallenta e perde colore.

---

## L'opera originale

*Quadrat I + II* è un'opera televisiva scritta e diretta da Samuel Beckett, trasmessa per la prima volta l'8 ottobre 1981 dalla Süddeutscher Rundfunk (SDR) di Stoccarda. Pubblicata in forma cartacea nel 1984 da Faber & Faber nei *Collected Shorter Plays*, è descritta come «a piece for four players, light and percussion» ed è stata definita anche «a ballet for four people».

Quattro interpreti incappucciati — in tuniche bianche, gialle, blu e rosse — percorrono i lati e le diagonali di un quadrato con lato di 6 passi, seguendo percorsi prescritti con precisione matematica, senza mai toccarsi e senza mai attraversare il centro. Ogni giocatore è accompagnato da un proprio strumento a percussione (tamburo, gong, triangolo, wood block) e da una luce del proprio colore.

La struttura combinatoria genera tutte le combinazioni possibili di giocatori in 4 serie di 6 fasi ciascuna: solo, duo, trio, quartetto, trio, duo — per un totale di 24 fasi di «movimento ininterrotto» (*unbroken movement*).

**Quad II** nacque per caso durante le registrazioni. Beckett vide la produzione a colori ritrasmessa su un monitor in bianco e nero ed esclamò: *«My God, it's a hundred thousand years later!»*. Creò così una seconda parte: niente colori, tuniche identiche, niente percussioni, metà velocità, solo il suono dei passi e il ticchettio di un metronomo. Una drammatizzazione dell'entropia. Il pattern dei dannati nell'*Inferno*.

### Riferimenti bibliografici

- Beckett, S. (1984). *Collected Shorter Plays of Samuel Beckett*. London: Faber & Faber, pp. 289–294.
- Herren, G. (2007). «Quadrat I + II: Eff It with Color». In: *Samuel Beckett's Plays on Film and Television*. New York: Palgrave Macmillan. DOI: [10.1007/978-1-137-10908-8_6](https://doi.org/10.1007/978-1-137-10908-8_6)
- Herren, G. (2000). «Samuel Beckett's Quad: Pacing to Byzantium». *Journal of Dramatic Theory and Criticism*, 15(1), pp. 43–60.
- Deleuze, G. (1995). «L'Épuisé» (*The Exhausted*). In: *Quad et autres pièces pour la télévision*. Paris: Minuit.
- Bláha, J. (2012). «'Mathematical Aesthetic' as a Strategy for Performance: A Vector Analysis of Samuel Beckett's Quad». *Journal of Beckett Studies*, 21(2). DOI: [10.3366/jobs.2012.0043](https://doi.org/10.3366/jobs.2012.0043)

---

## Questa implementazione

Un singolo file HTML autocontenuto (HTML + CSS + JavaScript, nessuna dipendenza esterna eccetto Google Fonts) che riproduce la coreografia di *Quad* come visualizzazione dall'alto, con piccoli cerchi colorati in movimento.

### Cosa è implementato fedelmente dalla partitura

**I 4 corsi prescritti** — Ogni giocatore segue il percorso esatto dalla partitura Faber 1984:

| Giocatore | Corso |
|-----------|-------|
| 1 (bianco) | A→C, C→B, B→A, A→D, D→B, B→C, C→D, D→A |
| 2 (giallo) | B→A, A→D, D→B, B→C, C→D, D→A, A→C, C→B |
| 3 (blu) | C→D, D→A, A→C, C→B, B→A, A→D, D→B, B→C |
| 4 (rosso) | D→B, B→C, C→D, D→A, A→C, C→B, B→A, A→D |

**La struttura combinatoria completa** — 4 serie × 6 fasi con entrate e uscite sequenziali:

```
Serie I:   1 · 1,3 · 1,3,4 · 1,3,4,2 · 3,4,2 · 4,2
Serie II:  2 · 2,1 · 2,1,4 · 2,1,4,3 · 1,4,3 · 4,3
Serie III: 3 · 3,2 · 3,2,1 · 3,2,1,4 · 2,1,4 · 1,4
Serie IV:  4 · 4,3 · 4,3,2 · 4,3,2,1 · 3,2,1 · 2,1
```

**L'aggiramento del centro (E)** — La *danger zone* viene sempre bypassata a sinistra, come nelle indicazioni di Beckett e nella produzione SDR.

**Quad II** — Versione desaturata, rallentata a metà velocità, cerchi grigi uniformi, scie più tenui.

### Elementi visivi

- **Cerchi colorati con alone luminoso** — visione dall'alto dei giocatori incappucciati.
- **Scie effimere** — le tracce dei percorsi svaniscono progressivamente, come i segni lasciati dai piedi sulle diagonali del quadrato bianco nella produzione originale.
- **Centro E** — punto bianco luminoso con glow radiale, sempre presente, mai toccato.
- **Barra informativa** — indica in tempo reale la modalità (Quadrat I / II), la serie corrente, il tipo di combinazione (Solo / Duo / Trio / Quartetto) e i colori dei giocatori attivi.
- **Legenda espandibile** — documentazione completa della partitura e della struttura.

### Controlli

| Pulsante | Funzione |
|----------|----------|
| **Quad I** | Avvia/riavvia Quad I (4 serie, colori, velocità normale) |
| **Quad II** | Avvia/riavvia Quad II (1 serie, grigi, metà velocità) |
| **Auto** | Transizione automatica: Quad I completo → Quad II → loop |
| **Pausa** | Sospende/riprende l'animazione |

---

## Deployment su GitHub Pages

Il progetto è un singolo file HTML. Per pubblicarlo:

1. Creare un repository su GitHub.
2. Rinominare `quad.html` in `index.html` e fare push sul branch `main`.
3. In **Settings → Pages**, selezionare la sorgente `main` / `/ (root)`.
4. La pagina sarà disponibile all'indirizzo `https://<utente>.github.io/<repo>/`.

Non sono necessari build tools, bundler, server o dipendenze npm.

### Struttura del repository

```
.
├── index.html    # L'intera applicazione (HTML + CSS + JS)
└── README.md     # Questo file
```

---

## Tecnologie

- **HTML5 Canvas** — doppio canvas sovrapposto (scie persistenti + rendering frame-by-frame).
- **Vanilla JavaScript** — macchina a stati per il sequencer della partitura, interpolazione lungo waypoint, nessun framework.
- **CSS** — layout flexbox, animazioni fade-in, design responsive con `clamp()` e unità viewport.
- **Google Fonts** — EB Garamond (testo) + JetBrains Mono (dati e interfaccia).

---

## Note

Questa è un'interpretazione digitale, non una riproduzione dell'opera televisiva. La produzione originale di Beckett per la SDR, diretta dall'autore stesso con gli allievi della Stuttgart Preparatory Ballet School (Helfried Foron, Jürg Hummel, Claudia Knupfer, Susanne Rehe), rimane un'opera irriducibile alla sua partitura — come Beckett stesso suggerì a proposito della relazione tra la pagina scritta e la realtà televisiva.

La sincronizzazione passo-passo tra giocatori simultanei (nella produzione originale, i movimenti sono perfettamente sincroni con ogni giocatore al punto corrispondente del proprio corso) è qui semplificata: tutti i giocatori attivi percorrono il proprio corso completo nello stesso intervallo temporale, ma non necessariamente con la granularità passo-per-passo della coreografia dal vivo.

---

## Licenza

Il codice di questa implementazione è rilasciato sotto licenza MIT.

L'opera *Quadrat I + II* è di Samuel Beckett. I diritti sull'opera originale appartengono al Beckett Estate.
