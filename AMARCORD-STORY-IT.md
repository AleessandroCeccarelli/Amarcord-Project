### `AMARCORD-STORY-IT.md`

```markdown
# Amarcord — La Storia

> Un software estremamente complesso non dovrebbe richiedere un'esperienza altrettanto complessa.

## L'inizio

Amarcord è nato da un'idea molto semplice.

E se l'emulazione potesse essere tecnicamente estremamente complessa dietro le quinte, ma estremamente semplice per chi la utilizza?

L'utente non dovrebbe essere costretto a conoscere emulatori, core, BIOS, configurazioni dei controller, impostazioni video, impostazioni audio o decine di opzioni tecniche.

L'idea era semplice:

**Scegli un gioco. Gioca.**

Tutto il resto dovrebbe essere responsabilità di Amarcord.

Il software dovrebbe occuparsi delle decisioni e dei dettagli tecnici che altrimenti farebbero perdere tempo all'utente.

Questo principio è diventato una delle fondamenta di Amarcord:

> **La complessità deve stare nell'architettura, non nell'esperienza dell'utente.**

Amarcord quindi non nasce con l'idea di essere semplicemente una raccolta di emulatori.

La visione a lungo termine è quella di creare un ambiente completo nel quale emulazione hardware, grafica, audio, controller, archiviazione, riconoscimento delle ROM, metadati e servizi applicativi lavorino insieme come un unico sistema coerente.

---

## L'idea dell'Apple TV

La direzione originale di Amarcord era **Apple TV**.

L'idea di portare un'esperienza di emulazione nativa su tvOS è stata una delle ragioni per cui il progetto è nato.

Apple TV rappresentava una sfida interessante.

La piattaforma è volutamente semplice dal punto di vista dell'utente, e questo si sposava perfettamente con la filosofia di Amarcord:

**sedersi, scegliere un gioco e giocare.**

All'inizio il progetto è stato quindi pensato con Apple TV in mente.

Abbiamo iniziato a studiare l'architettura, i limiti della piattaforma e le possibilità di costruire un ambiente di emulazione che potesse sentirsi realmente nativo Apple invece di essere semplicemente il porting di un emulatore esistente.

---

## Il passaggio a macOS

Durante lo sviluppo, però, è diventato evidente che macOS offriva un ambiente molto più flessibile per costruire il progetto.

Strumenti di sviluppo, possibilità di debugging, accesso al filesystem e libertà complessiva della piattaforma rendevano macOS un ambiente molto più pratico nel quale costruire Amarcord.

Il progetto ha quindi spostato il proprio obiettivo principale di sviluppo su **macOS**.

Questo non ha significato abbandonare l'idea originale di Apple TV.

È stato un cambiamento di strategia.

macOS è diventato l'ambiente nel quale Amarcord può essere costruito, testato e compreso con meno limitazioni.

---

## Apple TV fa ancora parte della visione

L'idea originale di tvOS non è mai stata abbandonata.

Uno degli obiettivi architetturali di Amarcord è evitare di costruire un sistema permanentemente legato a macOS.

L'architettura viene quindi sviluppata in modo che il core dell'emulazione e le parti indipendenti dalla piattaforma possano potenzialmente essere riutilizzati in futuro su altre piattaforme Apple.

Apple TV rimane quindi parte della direzione a lungo termine di Amarcord.

macOS è il terreno di sviluppo.

tvOS rimane una possibile destinazione.

L'architettura viene costruita tenendo presente questa distinzione.

---

## Da emulatore a framework

Con la crescita del progetto, l'idea originale di "un emulatore" è diventata qualcosa di più grande.

Un ambiente di emulazione completo richiede molto più di una CPU e di un renderer video.

Servono emulazione hardware, timing, memoria, cartucce, controller, audio, video, salvataggi e comunicazione tra tutti questi componenti.

Serve inoltre tutta l'infrastruttura che circonda l'emulatore.

Questo ha portato Amarcord verso un'architettura modulare composta da concetti come:

- Amarcord Core
- Astrazioni Console e Machine
- CPU
- Bus e memoria
- PPU
- APU
- DMA
- Gestione degli interrupt
- Cartridge e mapper
- Hardware dei controller
- Timing e sincronizzazione
- Video
- Audio
- Filesystem
- Save e Save State
- Riconoscimento delle ROM
- Importazione delle ROM
- ROM Database
- Servizi per metadati e artwork

La cosa importante non è il numero dei componenti.

È la separazione delle responsabilità.

Ogni componente deve avere uno scopo chiaro e comunicare con il resto del sistema attraverso confini ben definiti.

---

## Il primo sistema: NES

Il **Nintendo Entertainment System** è diventato il primo sistema completo su cui Amarcord si è concentrato.

Il NES è sufficientemente complesso da mettere alla prova gli aspetti più difficili dell'emulazione, ma allo stesso tempo rappresenta un primo obiettivo gestibile.

Abbiamo quindi deciso di completare correttamente il NES prima di passare ad altri sistemi.

L'obiettivo non è semplicemente far apparire un gioco NES sullo schermo.

L'obiettivo è completare l'intero percorso:

```text
ROM
 ↓
Importer
 ↓
Recognizer
 ↓
ROM Database
 ↓
Library / Filesystem
 ↓
NES Hardware
 ↓
CPU / Bus / PPU / APU / DMA
 ↓
Controller / Audio / Video
 ↓
Amarcord Core
 ↓
Utente

Solo quando questa pipeline completa funzionerà in modo affidabile Amarcord passerà verso altri sistemi.

⸻

L’idea di ScreenScraper

Un’altra parte importante della visione originale era evitare che l’utente dovesse organizzare e identificare manualmente tutto.

Una libreria di giochi dovrebbe essere in grado di capire cosa è stato importato e presentare informazioni utili.

Da qui è nata l’integrazione con ScreenScraper.

Il ruolo di ScreenScraper in Amarcord non è emulare nulla.

Il suo compito è arricchire i giochi riconosciuti con informazioni come:

* metadati
* artwork
* titoli
* informazioni regionali
* informazioni descrittive
* altre informazioni disponibili per la libreria

La distinzione architetturale fondamentale è che Amarcord deve prima capire che cosa sia la ROM.

Recognizer e ROM Database sono quindi responsabili dell’identificazione del software.

ScreenScraper diventa successivamente il livello dedicato a metadati e artwork costruito sopra quell’identità.

Il flusso previsto è:
ROM
 ↓
Amarcord Recognizer
 ↓
Identità della ROM
 ↓
ScreenScraper
 ↓
Metadata + Artwork
 ↓
Amarcord Library

Questa separazione è importante.

L’emulatore non deve conoscere i servizi online per i metadati.

La libreria non deve conoscere l’emulazione della CPU.

Ogni componente deve fare il proprio lavoro.

⸻

Il riconoscimento delle ROM e il database

Con l’evoluzione del progetto è emersa un’altra esigenza.

Amarcord deve avere un modo affidabile per capire il software importato prima di inserirlo nella libreria.

È nata così l’idea di un database centralizzato delle ROM.

La direzione attuale prevede l’utilizzo di dati XML che descrivono software e sistemi supportati, con un servizio Amarcord comune responsabile di caricare, interpretare, normalizzare e rendere disponibili queste informazioni al resto dell’applicazione.

L’obiettivo è evitare che più componenti indipendenti cerchino di interpretare lo stesso database.

Una sola fonte.

Un solo servizio.

Più utilizzatori.

Recognizer, Importer, Library e sistema dei metadati possono quindi lavorare sulle stesse informazioni.

⸻

Il capitolo MAME

MAME ha avuto un ruolo importante durante lo sviluppo di Amarcord.

A un certo punto abbiamo preso in considerazione l’idea di portare MAME direttamente dentro Amarcord.

Un bridge tra Amarcord e MAME sembrava una possibile soluzione per ottenere rapidamente una grande quantità di funzionalità di emulazione già esistenti.

Era un’idea interessante per motivi abbastanza evidenti.

MAME rappresenta un’enorme quantità di conoscenza e di lavoro nel campo dell’emulazione.

Ma introduceva anche un problema fondamentale.

Avrebbe cambiato ciò che Amarcord era realmente.

Invece di costruire un framework di emulazione indipendente e nativo per Apple, Amarcord sarebbe diventato un’applicazione costruita attorno a un runtime di emulazione esterno.

Non era questa la visione originale.

⸻

La decisione di tornare indietro

Abbiamo quindi deciso di fare un passo indietro.

L’approccio basato sul runtime MAME e sul bridge è stato abbandonato.

Amarcord sarebbe diventato un progetto autonomo.

L’architettura di emulazione sarebbe stata implementata in Swift e Metal, studiando il comportamento dell’hardware attraverso riferimenti tecnici e progetti di emulazione esistenti quando necessario.

MAME rimane un riferimento tecnico durante lo sviluppo.

Non è il runtime di Amarcord.

Non esiste un bridge MAME.

L’obiettivo è mantenere Amarcord il più possibile pulito, nativo e indipendente.

Questa decisione ha reso lo sviluppo più difficile.

Ma ha anche reso il progetto più significativo.

Invece di collegare semplicemente componenti già esistenti, stiamo costruendo noi l’architettura.

⸻

Il prezzo dell’indipendenza

Costruire un emulatore da zero non è un compito piccolo.

Un componente può compilare perfettamente ed essere comunque sbagliato.

Una CPU può eseguire correttamente le istruzioni ma fallire perché il bus non si comporta correttamente.

Una PPU può disegnare pixel ma essere comunque errata a causa del timing.

Un DMA può sembrare funzionante mentre sottrae un numero sbagliato di cicli alla CPU.

Gli interrupt possono essere corretti individualmente ma instradati in modo errato attraverso la machine.

Un mapper può funzionare isolatamente e fallire quando viene collegato a una vera cartuccia.

Una delle lezioni più importanti dello sviluppo di Amarcord è quindi diventata:

La compilazione non è una validazione.

L’architettura deve funzionare come sistema.

Per questo il progetto viene sviluppato progressivamente, aumentando l’importanza dell’integrazione man mano che i singoli componenti hardware vengono completati.

⸻

La parte difficile: l’integrazione

Una delle difficoltà più grandi non è scrivere i singoli componenti.

È farli comportare correttamente insieme.

Il NES è composto da elementi strettamente collegati.

CPU, PPU, APU, DMA, interrupt, hardware delle cartucce, controller e timing influenzano tutti gli altri.

Lo stesso principio vale per Amarcord.

L’emulatore dovrà comunicare correttamente con:

* Amarcord Core
* Video
* Audio
* Controller
* Filesystem
* sistemi di salvataggio
* Importer
* Recognizer
* ROM Database
* servizi per i metadati

Per questo il progetto sta deliberatamente evitando la tentazione di continuare ad aggiungere funzionalità isolate.

L’obiettivo è costruire un sistema.

⸻

Human + AI

Amarcord è anche un esperimento su un modo diverso di sviluppare software.

Il progetto viene sviluppato attraverso una collaborazione tra una persona e l’AI.

L’AI contribuisce all’esplorazione tecnica, alle discussioni architetturali, all’implementazione, all’analisi e alla revisione.

La direzione finale di Amarcord, però, rimane una decisione umana.

Il progetto non vuole fingere di essere sviluppato da un tradizionale team di software engineering.

È un esperimento su ciò che può essere costruito quando un appassionato di tecnologia, la curiosità e lo sviluppo assistito dall’AI lavorano insieme.

L’importante non è nascondere questo processo.

L’importante è costruire qualcosa di reale.

⸻

Dove siamo oggi

Amarcord è ancora un progetto in sviluppo.

Il NES rimane il principale obiettivo.

La priorità attuale è completare l’hardware NES e collegarlo correttamente al resto dell’architettura Amarcord.

Il progetto dovrà arrivare al punto in cui un gioco reale possa attraversare l’intera pipeline:
ROM
 ↓
Import
 ↓
Recognition
 ↓
Library
 ↓
NES
 ↓
Controller
 ↓
Audio
 ↓
Video
 ↓
Save / State
 ↓
Gioco funzionante

Solo dopo aver validato questo percorso completo gli altri emulatori diventeranno la priorità successiva.

⸻

Cosa viene dopo

La visione a lungo termine rimane più grande del solo NES.

Tra i possibili sistemi futuri ci sono:

* Super Nintendo
* Master System
* Mega Drive
* PlayStation

Ma la filosofia rimane la stessa.

Costruire attentamente l’architettura.

Mantenere semplice l’esperienza dell’utente.

Non aggiungere complessità dove non serve.

E lasciare che Amarcord si occupi delle parti complicate.

L’utente non dovrebbe mai preoccuparsi di quanto sia difficile il software.

Dovrebbe semplicemente poter:

Scegliere un gioco.

Giocare.

⸻

Una storia in evoluzione

Questo documento non è volutamente una specifica definitiva.

Amarcord è ancora in costruzione.

L’architettura evolverà.

Le idee cambieranno.

Alcune decisioni si dimostreranno sbagliate.

Nuovi problemi emergeranno.

Questo file verrà aggiornato periodicamente per documentare questi cambiamenti e conservare la storia dell’evoluzione di Amarcord.

L’obiettivo non è fingere che il percorso sia stato perfettamente pianificato fin dall’inizio.

L’obiettivo è raccontare il percorso reale.

⸻

Amarcord — Proprietary Software
Copyright © 2026 Alessandro Ceccarelli. All rights reserved.



