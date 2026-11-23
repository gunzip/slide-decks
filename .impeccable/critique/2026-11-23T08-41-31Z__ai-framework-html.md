---
target: ai-framework.html
total_score: 33
max_score: 40
na_heuristics: 
p0_count: 0
p1_count: 3
p2_count: 2
target_identity: "file:/Users/danilo.spinelli/Developer/slide-decks/ai-framework.html"
target_fingerprint: "sha256:7b12fc1fb082b94e9fa068f8a888ff2271aedefe5ade24c02cd294c83e87bf33"
target_path: /Users/danilo.spinelli/Developer/slide-decks/ai-framework.html
timestamp: 2026-11-23T08-41-31Z
slug: ai-framework-html
---
# Critique — ai-framework.html (deck "Agentic Delivery Framework", 17 slide, obiettivo: approvazione pilota)

**Method: dual-agent (A: ses_df87e86baffeX16ZDi13OrWwM6 · B: ses_df87e86b9ffe77FMpPUkzicdfB)**

## Design Health Score — 33/40 (Good)

| # | Euristica | Voto | Nota chiave |
|---|-----------|------|-------------|
| 1 | Visibilità dello stato | 4 | HUD persistente (sezione, 01/17, ticks cliccabili, timer), prossima slide in presenter view |
| 2 | Match col mondo reale | 3 | Parla Platform (DoR, SLO, flag) ma acronimi mai espansi (JTBD, SAST, "DR-05") e mix agente/agent incoerente |
| 3 | Controllo e libertà | 3 | Indice O, deep-link hash, Esc, sipario B, touch — ma i tasti 1-9 raggiungono solo 9/17 slide |
| 4 | Consistenza e standard | 3 | Template rigoroso, ma data-title ≠ h2 su 7 slide e tassonomia etichette incoerente |
| 5 | Prevenzione errori | 3 | Fallback presenter, blackout chiudibile — ma nota slide 7 cita un elemento inesistente |
| 6 | Riconoscimento > richiamo | 3 | Indice sempre accessibile; ma i titoli dell'indice non coincidono con gli h2 a schermo |
| 7 | Flessibilità ed efficienza | 4 | Shortcut completi, presenter view sincronizzata, fullscreen, touch, stampa |
| 8 | Estetica e minimalismo | 4 | Un font, un accento, figure su misura, zero ornamenti; unica pecca grave: densità slide 3 |
| 9 | Riconoscimento/ripristino errori | 2 | Hash sconosciuto → ritorno silenzioso a slide 0; popup presenter bloccato → nessun messaggio |
| 10 | Aiuto e documentazione | 4 | Pannello ? esaustivo, note relatore per slide, drawer note con "N per chiudere" |
| **Totale** | | **33/40** | **Good — base solida, da raffinare dove pesa l'obiettivo** |

## Verdetto di specificità

**LLM assessment**: MEDIO — contenuto autoriale, forma intercambiabile. Il copy è cucito addosso (Jira/Confluence/MCP, DoR & Pre-fill, "buy sul make"), l'arco in 6 sezioni è coerente, ma il linguaggio visivo è il template di casa e le figure sono linee-con-nodi generiche. Soprattutto: **zero numeri e zero artefatti reali in 17 slide** — nessun estratto di PRD/DR, nessun audit log, nessuna baseline. Un proposal che chiede di approvare un pilota senza una sola evidenza empirica è, nella forma, scambiabile con qualunque deck tech.

**Scan deterministico (CLI)**: 5 findings, tutti warning. Quattro sono verosimilmente falsi positivi per un deck presentazionale: `cramped-padding` sul full-bleed `.stage` (riga 380), `tight-leading` su display type 24–44px (righe 87/90/140 — interlinea 1.14–1.18 è una scelta standard per titoli grandi, la regola è tarata sul body), `all-caps-body` ×2 su micro-label 11px con letter-spacing (`.stat`, `.f-k`, eyebrow convenzionali, non prosa). Uno è reale ma di copy: `marketing-buzzword` su "servizi mission-critical" (slide 15, riga 1005).

**Evidenza browser**: preflight di mutazione riuscito, detector iniettato nella pagina (live server porta 8400, fermato e confermato a fine raccolta). Il detector runtime ha scansionato le slide 1, 4, 7, 9 e 13: **0 anti-pattern trovati**. Copertura slide 16 saltata per timeout CDP del daemon browser (dichiarato, non ritentato). Screenshot di riferimento: slide04.png e slide07.png in /private/var/folders/4_/1fqf25ys5ld_j3_h_tlln78m0000gp/T/opencode/. La divergenza CLI (5) vs runtime (0) è coerente con la taratura del runtime su viewport/app interattive; per la review pesa di più la lettura di design.

## Impressione complessiva

Il deck è l'artefatto tecnicamente più curato che si possa desiderare: runtime da relatore professionale, disciplina tipografica, figure su misura. Come presentazione informativa funziona; come **deck decisionale** perde colpi esattamente dove conta: l'oggetto della decisione (slide 16) non ha contorni, il finale è un punto interrogativo, e lo scettico non trova da nessuna parte i numeri (costi, baseline, soglie). La singola maggior opportunità: trasformare le ultime due slide da descrizione in richiesta approvabile.

## Cosa funziona

1. **Slide 9 — la figura deploy/flag** con esiti "Confermata / Regressione — flag spenta, zero redeploy" (righe 781–786): converte il rischio percepito n.1 (codice AI in produzione) in un interruttore, posizionata esattamente dove il pubblico Platform cerca la rassicurazione. Il miglior pezzo persuasivo del deck.
2. **La noteline di slide 16** (riga 1034): "l'autorizzazione alla fase pilota, non l'imposizione universale immediata" — l'ask ristretto correttamente; peccato sia in 16px in fondo alla slide invece che in statement.
3. **Il runtime da presentatore**: presenter view sincronizzata (note + prossima slide + timer), tasti, indice, stampa, deep-link. È costruito per essere presentato dal vivo, e il detector runtime conferma 0 anti-pattern sulle viste scansionate.

## Problemi prioritari

### 1. [P1] L'ask non ha contorni (slide 16)
**Cosa**: le tre fasi del pilota non hanno durata, owner, perimetro nominale, costi né soglie GO/NO-GO; i KPI (riga 1026) sono nomi senza target.
**Perché danneggia**: Platform non può approvare un perimetro indefinito; l'ask forte della noteline galleggia su un piano vago, e il decisore rimanda ("riproporrete quando avete i numeri").
**Fix**: riga "Perimetro della decisione" sotto le fasi — 1-2 servizi nominali, 6-8 settimane, owner, costo stimato, GO/NO-GO con soglie (es. lead time −30%, tasso rifiuto PR <25%).
**Comando suggerito**: /impeccable clarify

### 2. [P1] Il finale è "Domande?" (slide 17)
**Cosa**: statement 44px "Domande?" (riga 1050) — la cosa più debole del deck nell'ultima cosa che il pubblico ricorda (violazione peak-end).
**Perché danneggia**: l'ultima immagine che Platform porta a casa è un punto interrogativo, non la decisione.
**Fix**: statement finale "Chiediamo l'avvio del pilota su 1-2 servizi" con i vincoli come sub-line e "Domande?" sotto (la copertina promette "Domande alla fine", che resta compatibile).
**Comando suggerito**: /impeccable bolder

### 3. [P1] Dieci domande aperte in quarta slide (slide 3)
**Cosa**: 10 domande senza risposta su 2 colonne (righe 466–501), subito dopo la promessa di slide 2.
**Perché danneggia**: allo scettico legge "non hanno ancora risposte" — uccide la fiducia appena costruita e viola il chunking (≤4 per gruppo).
**Fix**: ridurre ai 4 domini come etichette con una risposta-seme ciascuna ("Fonti → registry condiviso", "Pianificazione → DoR"), spostando le domande intere nelle note del relatore.
**Comando suggerito**: /impeccable distill

### 4. [P2] Semantica dei gate non spiegata (slide 13)
**Cosa**: solo il Gate 3 è teal "Automatico deterministico" (riga 918), ma le note (riga 930) dicono che i gate 2 e 3 sono automatici; il gate di sicurezza sembra senza presidio umano.
**Perché danneggia**: la prima obiezione di Platform sarà "chi risponde di una breccia se il gate è solo automatico?"
**Fix**: legenda a due chip (Umano / Automatico), Gate 2 marcato ibrido, una riga "ogni gate automatico ha escalation umana".
**Comando suggerito**: /impeccable clarify

### 5. [P2] Affidabilità in sala: nota che cita l'invisibile + contrasto sotto soglia
**Cosa**: le note di slide 7 (riga 707) citano una "linea tratteggiata" (Change Request) che nell'SVG non esiste — la tratteggiata è nella figura della slide 8 (riga 736); e le linee dim delle figure (#8898a8, contrasto misurato 2.86:1) sono sotto i 3:1 di WCAG 1.4.11: loop di feedback (slide 8) ed esiti Confermata/Regressione (slide 9) rischiano di sparire su proiettore lavato.
**Perché danneggia**: il relatore indica qualcosa di invisibile nel momento che spiega la catena; le figure chiave svaniscono dalla fondo sala.
**Fix**: aggiungere all'SVG di slide 7 la return-path tratteggiata "Change Request" (o tagliare la frase dalle note), e scurire --fig-dim a ≥3:1 (es. #6b7686) alzando le label figure a 11.5–12px.
**Comando suggerito**: /impeccable audit

## Red flags per persona

**Riley (decisore Platform scettico)**: costi mai affrontati (una domanda retorica a riga 490, mai risposta); nessuna slide sul costo del non-adozione; slide 6 ammette protocolli "non ancora stabilizzati" e una "scommessa sugli harness ufficiali" (righe 640–645) senza piano B per le skill costruite oggi; l'ask è in 16px in fondo a slide 16 — può non accorgersene.

**Alex (relatore live)**: nota slide 7 punta a un elemento inesistente (flub garantito); i tasti 1-9 raggiungono solo le slide 1-9 su 17 (regex riga 1236) — per saltare alla 16 nel Q&A serve il mouse sull'indice; l'indice mostra titoli diversi dagli h2 a schermo ("Uomo e macchina" vs "Separazione delle responsabilità"); location.hash a ogni go() (riga 1170) riempie la cronologia — un Back accidentale salta slide durante il talk.

**Sam (accessibilità)**: contrasto figure dim 2.86:1 sotto WCAG 1.4.11; label figure a 10.5–11.5px al limite da fondo sala; blackout con aria-hidden statico (riga 1109) — il sipario non è annunciato. Note positive: reduced-motion gestito, focus-visible, aria-label sugli SVG.

## Osservazioni minori

- Grammatica: "pronta per poter esser presa in carico" → "essere" (riga 477).
- Mix agent/agente incoerente: "dagli agent" (riga 477), "gli agent operano" (riga 624) vs "l'agente" altrove.
- Etichette "DR-03/05/06" (righe 861, 1000, 1035) mai spiegate, convivono con etichette libere ("Governance · Mappa dei Gate") — sembrano scenografia.
- Copy: "servizi mission-critical" (slide 15, riga 1005) è l'unico finding reale del detector — buzzword in un contesto interno che non ne ha bisogno.
- CSS morto del template di casa: .quote/.tstack/.snippet/.cmd mai usati nel markup.
- HUD statico "/ 02" e placeholder presenter "01 / 21" corretti dal JS al boot — ok, ma visibili per un frame.

## Domande da porsi

1. Se sostituiste il testo con quello di qualunque proposta AI di un'altra azienda, cosa resterebbe di irripetibile — e se la risposta è "nulla visivamente", perché l'identità vive solo nel copy?
2. Quale altra richiesta di investimento avete mai approvato senza durata, costi e criteri di uscita? Perché questo deck dovrebbe essere l'eccezione?
3. Volete davvero che l'ultima cosa che Platform ricordi sia un punto interrogativo?
