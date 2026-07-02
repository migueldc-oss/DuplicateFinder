# Manuale utente — DuplicateFinder

> ![Screenshot dell'app](capturas/main.png)
> *Vista principale di DuplicateFinder con la barra di scansione e la tabella dei risultati.*

---

## Indice dei contenuti

1. [Introduzione](#1-introduzione)
2. [Requisiti di sistema](#2-requisiti-di-sistema)
3. [Interfaccia principale](#3-interfaccia-principale)
4. [Selezione delle cartelle](#4-selezione-delle-cartelle)
5. [Modalità di rilevamento](#5-modalita-di-rilevamento)
6. [Avanzamento scansione](#6-avanzamento-scansione)
7. [Risultati](#7-risultati)
8. [Azioni sui file](#8-azioni-sui-file)
9. [Esportazione dei risultati](#9-esportazione-dei-risultati)
10. [Preferenze](#10-preferenze)
11. [Suggerimenti e buone pratiche](#11-suggerimenti-e-buone-pratiche)

---

## 1. Introduzione

**DuplicateFinder** è un'applicazione macOS che trova e gestisce file duplicati sul tuo disco. Scansiona una o più cartelle, calcola un'impronta SHA-256 per ogni file e raggruppa quelli identici, permettendoti di rivedere, aprire, eliminare o esportare un report.

### Funzionalità principali

- Scansione ricorsiva di più cartelle simultaneamente.
- Due modalità di rilevamento: **Affidabile** (basata sul contenuto, SHA-256) e **Veloce** (nome + dimensione).
- Filtri per dimensione, estensioni e cartelle escluse.
- Tabella ordinabile con ricerca nei risultati.
- Azioni individuali e in blocco: apri, mostra nel Finder, sposta nel Cestino o elimina definitivamente.
- Esportazione in CSV e JSON con ogni percorso di file duplicato.
- Interfaccia localizzata in 8 lingue.

---

## 2. Requisiti di sistema

- **macOS** 14.0 (Sonoma) o successivo.
- **Apple Silicon** o **Intel**.
- Nessun pacchetto esterno o dipendenza richiesta.

---

## 3. Interfaccia principale

![Layout dell'interfaccia](capturas/interfaz.png)

La finestra è divisa in tre aree:

| Area | Descrizione |
|------|-------------|
| **Barra superiore (ScanView)** | Selezione cartelle, scelta modalità di rilevamento, comandi avvia/annulla. |
| **Barra delle statistiche** | Metriche globali (file totali, duplicati, gruppi, spazio recuperabile) e pulsante esportazione. |
| **Tabella dei risultati** | Elenco ordinabile dei gruppi duplicati con ricerca. |

---

## 4. Selezione delle cartelle

![Selezione cartelle](capturas/seleccion-carpetas.png)

1. Fai clic sul pulsante **"Scegli cartella…"** (icona cartella).
2. Si apre la finestra di dialogo standard di macOS. Seleziona **una o più cartelle** tenendo premuto ⌘ (Comando).
3. Le cartelle si **accumulano** nell'elenco. Puoi aggiungere altre cartelle in selezioni successive.
4. Per cancellare la selezione, fai clic sul pulsante **"Cancella"** (icona ✕) che appare accanto.

> Il pulsante **"Avvia scansione"** rimane disabilitato fino a quando non viene selezionata almeno una cartella. Puoi anche trascinare una cartella dal Finder direttamente sulla finestra.

---

## 5. Modalità di rilevamento

DuplicateFinder offre due modalità, selezionabili tramite un controllo segmentato nella barra superiore:

| Modalità | Descrizione |
|----------|-------------|
| **Affidabile** | Calcola l'hash SHA-256 del **contenuto completo** di ogni file. Garantisce zero falsi positivi, ma è più lenta perché legge ogni file. |
| **Nome + Dimensione** | Confronta solo il nome (senza distinzione maiuscole/minuscole) e la dimensione in byte. Molto veloce (nessuna lettura file), ma può produrre falsi positivi se file diversi condividono stesso nome e dimensione. |

> La modalità predefinita è impostata in **Preferenze → Rilevamento**.

---

## 6. Avanzamento scansione

Durante una scansione, la barra superiore mostra la fase corrente:

| Fase | Indicatore |
|------|------------|
| **Scansione…** | Contatore dei file elaborati nella cartella. |
| **Confronto…** | Barra di avanzamento con numero di hash calcolati sul totale dei candidati. |
| **Calcolo…** | Avanzamento dell'inserimento nel database e del calcolo degli aggregati. |
| **Completata** | Icona segno di spunta verde. |
| **Annullata** | Icona arancione. |

Puoi annullare la scansione in qualsiasi momento facendo clic sul pulsante **"Annulla"**.

---

## 7. Risultati

![Tabella dei risultati](capturas/resultados.png)

Al termine della scansione, appare la tabella dei risultati con le seguenti colonne:

| Colonna | Descrizione |
|---------|-------------|
| **Nome** | Nome del file con la sua icona. |
| **Dimensione** | Dimensione di ogni copia. |
| **Copie** | Numero di duplicati per questo file. |
| **Dimensione × Copie** | Spazio totale occupato da tutte le copie. |
| **Posizione** | Percorso completo di ogni copia, con pulsanti azione. |

Puoi **ordinare** la tabella facendo clic su qualsiasi intestazione di colonna. Puoi anche **cercare** file per nome o percorso usando il campo di ricerca in basso.

### Barra delle statistiche

Quattro metriche sono mostrate sopra i risultati:

- **File totali**: tutti i file scansionati.
- **Duplicati**: file appartenenti a un gruppo duplicato.
- **Gruppi**: insiemi di file identici.
- **Recuperabile**: spazio liberabile se tutte le copie duplicate (meno una per gruppo) vengono rimosse.

---

## 8. Azioni sui file

Ogni file duplicato nella colonna "Posizione" ha pulsanti azione:

| Pulsante | Azione |
|----------|--------|
| 👁 (Occhio) | Apri il file con l'applicazione predefinita. |
| 📁 (Cartella) | Mostra il file nel Finder. |
| 🗑 (Cestino) | Sposta nel Cestino (o elimina definitivamente, in base alle preferenze). |

### Eliminazione in blocco

Puoi selezionare più file spuntando la casella quadrata accanto a ciascuno:

1. Seleziona i file che vuoi eliminare.
2. Il pulsante **"Elimina selezionati (N)"** appare nella barra delle statistiche.
3. Fai clic per confermare e completare l'eliminazione.

> Puoi modificare il comportamento di eliminazione in **Preferenze → Generali**: attiva/disattiva "Sposta file nel Cestino".

---

## 9. Esportazione dei risultati

Fai clic sul pulsante **"Esporta"** (icona condividi) nella barra delle statistiche e scegli:

- **CSV** — File di testo con valori separati da virgola, compatibile con Excel, Numbers e fogli di calcolo.
- **JSON** — Formato strutturato, ideale per l'elaborazione programmatica.

Entrambi i formati includono **ogni copia di ogni file duplicato** (non solo una per gruppo), con i campi: nome, percorso, dimensione, numero di copie, spazio totale occupato e hash SHA-256.

Viene visualizzata una finestra di dialogo `NSSavePanel` per scegliere la destinazione e il nome del file.

---

## 10. Preferenze

Premi `⌘,` (Comando + ,) per aprire le preferenze, organizzate in quattro schede.

### Generali

| Opzione | Descrizione |
|---------|-------------|
| **Top N risultati** | Numero massimo di righe nella tabella dei risultati (10–100.000). |
| **Sposta nel Cestino** | Se attivo, i file vengono spostati nel Cestino invece di essere eliminati definitivamente. |
| **Strategia di conservazione** | Strategia per selezionare automaticamente quale copia conservare (più vecchia, più nuova o percorso più breve). |
| **Aspetto** | Modalità chiara, scura o di sistema. |

### Rilevamento

| Opzione | Descrizione |
|---------|-------------|
| **Modalità predefinita** | Modalità di rilevamento selezionata all'apertura dell'app. |

### Filtri

| Opzione | Descrizione |
|---------|-------------|
| **Dim. min / max** | Intervallo di dimensione in byte. I file al di fuori di questo intervallo vengono ignorati. |
| **Includi nascosti** | Include file e cartelle nascosti (che iniziano con `.`). |
| **Segui link simbolici** | Se attivo, i link simbolici vengono seguiti durante la scansione. |
| **Estensioni consentite** | Elenco separato da virgole (es. `jpg, png, mp4`). Vuoto = tutte le estensioni. |
| **Cartelle escluse** | Elenco separato da virgole di nomi di cartelle saltate durante la scansione (es. `node_modules, .git`). |

### Lingua

Cambia la lingua dell'interfaccia tra le 8 disponibili. L'app potrebbe dover essere riavviata per applicare completamente la modifica.

---

## 11. Suggerimenti e buone pratiche

1. **Inizia con la modalità Veloce** se hai molte cartelle. È molto più rapida e potrebbe trovare la maggior parte dei duplicati.
2. **Usa la modalità Affidabile per decisioni finali** prima di eliminare — specialmente quando i nomi dei file non corrispondono — per evitare falsi positivi.
3. **Scegli cartelle specifiche**, non l'intero disco. Scansionare solo Download, Documenti e Scrivania riduce drasticamente tempo e rumore.
4. **Controlla le posizioni** nella colonna "Posizione" prima di eliminare. Un duplicato potrebbe trovarsi in una cartella di sistema dove dovrebbe rimanere.
5. **Esporta un CSV** prima di fare pulizia per conservare un registro dei file eliminati.
6. **Configura i filtri** quando cerchi tipi di file specifici (es. solo immagini `.jpg` e `.png`).
7. **Usa il pulsante "Cancella"** per ricominciare con una nuova selezione di cartelle senza uscire dall'app.

---

> **DuplicateFinder** — [mdc](https://github.com/migueldc-oss/DuplicateFinder)
>
> Documentazione generata il 1 luglio 2026.
