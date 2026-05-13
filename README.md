# 🏰 Armil Castle

> *"Non stai uscendo dal castello: stai smettendo di abitarlo."*

Un gioco testuale con interfaccia grafica scritto interamente in Java — ma soprattutto, un **motore di gioco** progettato per essere scalabile, estendibile e indipendente dal contenuto che ci gira sopra.

Questo progetto nasce come capolavoro di fine anno al quarto anno di Informatica, ma è cresciuto ben oltre i requisiti scolastici. È il risultato di mesi di studio autonomo, di scelte architetturali deliberate, e di una storia che volevo davvero raccontare.

---

## ✨ Cosa rende questo progetto interessante

La maggior parte dei giochi testuali ha la logica di gioco cucita direttamente al contenuto — cambi il gioco, riscrivi tutto. Armil Castle è costruito diversamente.

Il **motore** non sa nulla del castello. Non conosce le stanze, i personaggi, i puzzle. Sa solo come gestire oggetti, comandi, eventi e stato. Il castello è **configurazione** — scritto in una classe separata (`CostruttoreMondo`) che il motore legge senza bisogno di essere modificato.

Vuoi costruire un gioco completamente diverso con lo stesso motore? Scrivi il tuo `CostruttoreMondo` e il resto funziona già.

---

## 🗺️ Architettura

Il progetto è organizzato in package distinti con responsabilità separate:

```
src/
├── Main.java                    ← 4 righe. Davvero.
└── motore/
    ├── core/                    ← Gioco, Stanza, Oggetto, NPC, CostruttoreMondo
    ├── comandi/                 ← interfaccia Comando + 10 implementazioni
    ├── eventi/                  ← classe astratta Evento + 6 implementazioni
    └── io/                      ← GUI, salvataggio, output
```

**Pattern utilizzati:** Command, Strategy, Composite (eventi annidati), separazione configurazione/logica.

**Strutture dati:** `HashMap` per le uscite delle stanze e i comandi, `HashSet` per gli eventi consumati e le stanze visitate, `ArrayList` per inventario e oggetti.

---

## 🎮 Il gioco

Armil Castle è un castello gotico con trenta stanze, otto personaggi non giocanti e una storia che parla di zone di comfort, rifugi mentali e della difficoltà di lasciare andare ciò che ci tiene fermi.

Ogni personaggio ha un momento di risoluzione — un oggetto che il giocatore può portargli, che lo fa svanire. Il Musicista che non ricorda da dove viene la melodia che suona. La Cuoca che aspetta qualcuno che non tornerà. Il Bambino che parla come un vecchio.

Il gioco ha due finali. Solo uno porta fuori dal castello.

La struttura narrativa è ispirata a **Save the Cat** di Blake Snyder — ogni personaggio ha un desiderio visibile e un bisogno nascosto, e il protagonista non fa eccezione.

---

## 🖥️ Interfaccia grafica

L'interfaccia è costruita con **Swing** — tema dark atmosferico, font Georgia, testo color pergamena, accenti oro antico. Non era richiesta. L'ho fatta perché il gioco la meritava.

![screenshot placeholder](screenshot.png)

---

## 🚀 Come far girare il progetto

### Requisiti

- **Java 21** o superiore (il progetto usa alcune feature di Java 25, ma è compatibile dalla 21 in su con piccole modifiche)
- Nessuna dipendenza esterna — zero librerie di terze parti

### Opzione 1 — IntelliJ IDEA (consigliata)

1. Clona la repository:
   ```bash
   git clone https://github.com/Armill0/ArmilCastle.git
   ```
2. Apri IntelliJ IDEA → `File → Open` → seleziona la cartella `ArmilCastle`
3. IntelliJ rileva automaticamente la struttura del progetto
4. Clicca **Run** sul file `Main.java`

### Opzione 2 — Da terminale

1. Clona la repository:
   ```bash
   git clone https://github.com/Armill0/ArmilCastle.git
   cd ArmilCastle
   ```

2. Compila tutti i sorgenti:
   ```bash
   javac -d out $(find src -name "*.java")
   ```
   Su Windows (PowerShell):
   ```powershell
   Get-ChildItem -Recurse -Filter "*.java" src | ForEach-Object { $_.FullName } | Out-File sources.txt
   javac -d out @sources.txt
   ```

3. Avvia il gioco:
   ```bash
   java -cp out Main
   ```

### Nota sul salvataggio

Il file di salvataggio viene creato nella directory da cui avvii il programma con il nome `salvataggio.txt`. Se vuoi ricominciare da capo, cancellalo o scegli **Nuova partita** dal menu iniziale.

---

## 📁 Struttura delle classi principali

| Classe | Responsabilità |
|---|---|
| `Gioco` | Stato globale: inventario, flag, stanze visitate, eventi consumati |
| `Stanza` | Descrizione, uscite visibili e nascoste, oggetti, eventi, NPC |
| `CostruttoreMondo` | Configurazione dell'intero mondo — stanze, oggetti, NPC, eventi |
| `MotoreIO` | Parsing dell'input e dispatch ai comandi |
| `Evento` | Classe astratta base per tutto il sistema degli eventi |
| `FinestraGioco` | GUI Swing con area narrativa, input e pannello laterale |
| `GestoreSalvataggio` | Lettura e scrittura dello stato su file di testo |

---

## 🛠️ Tecnologie e concetti

- **Java 25** — instance main methods, record classes, enhanced switch
- **Swing** — GUI con layout manager, scrollbar personalizzata, tema dark
- **Pattern Command** — ogni azione del giocatore è un oggetto
- **Pattern Strategy** — output intercambiabile tra terminale e GUI
- **Classi anonime** — eventi inline per logica specifica
- **Try-with-resources** — gestione sicura dei file
- **HashMap / HashSet** — strutture dati scelte per caratteristiche, non per abitudine

---

## 👤 Autore

**Alessandro Baire** — studente di Informatica, appassionato di narrativa interattiva e architettura software.

Questo è il secondo progetto che pubblico su GitHub. Il primo era un gioco testuale in C++. La differenza tra i due dice tutto sulla crescita che c'è stata nel mezzo.

---

*Costruito con Java, pazienza, e una quantità irragionevole di caffè "immaginario".*
