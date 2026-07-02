# Benutzerhandbuch — DuplicateFinder

> ![App screenshot](capturas/main.png)
> *Hauptansicht von DuplicateFinder mit der Scan-Leiste und der Ergebnistabelle.*

---

## Inhaltsverzeichnis

1. [Einleitung](#1-einleitung)
2. [Systemanforderungen](#2-systemanforderungen)
3. [Hauptoberfläche](#3-hauptoberfläche)
4. [Ordner auswählen](#4-ordner-auswählen)
5. [Erkennungsmodi](#5-erkennungsmodi)
6. [Scanfortschritt](#6-scanfortschritt)
7. [Ergebnisse](#7-ergebnisse)
8. [Dateiaktionen](#8-dateiaktionen)
9. [Ergebnisse exportieren](#9-ergebnisse-exportieren)
10. [Einstellungen](#10-einstellungen)
11. [Tipps und Best Practices](#11-tipps-und-best-practices)

---

## 1. Einleitung

**DuplicateFinder** ist eine macOS-Anwendung, die doppelte Dateien auf Ihrer Festplatte findet und verwaltet. Sie durchsucht einen oder mehrere Ordner, berechnet einen SHA-256-Fingerabdruck für jede Datei und gruppiert identische Dateien – sodass Sie diese überprüfen, öffnen, löschen oder einen Bericht exportieren können.

### Hauptfunktionen

- Rekursive Durchsuchung mehrerer Ordner gleichzeitig.
- Zwei Erkennungsmodi: **Zuverlässig** (inhaltsbasiert, SHA-256) und **Schnell** (Name + Größe).
- Filter nach Größe, Dateierweiterungen und ausgeschlossenen Ordnern.
- Sortierbare Tabelle mit Suche in den Ergebnissen.
- Einzel- und Stapelaktionen: Öffnen, in Finder anzeigen, in den Papierkorb verschieben oder endgültig löschen.
- Export nach CSV und JSON mit allen Speicherorten doppelter Dateien.
- Oberfläche in 8 Sprachen lokalisiert.

---

## 2. Systemanforderungen

- **macOS** 14.0 (Sonoma) oder neuer.
- **Apple Silicon** oder **Intel**.
- Keine externen Pakete oder Abhängigkeiten erforderlich.

---

## 3. Hauptoberfläche

![Interface layout](capturas/interfaz.png)

Das Fenster ist in drei Bereiche unterteilt:

| Bereich | Beschreibung |
|---------|--------------|
| **Obere Leiste (ScanView)** | Ordnerauswahl, Auswahl des Erkennungsmodus, Start-/Abbrechen-Steuerung. |
| **Statistikleiste** | Globale Kennzahlen (Gesamtdateien, Duplikate, Gruppen, wiedergewinnbarer Speicherplatz) und Export-Button. |
| **Ergebnistabelle** | Sortierbare Liste von Duplikatgruppen mit Suchfunktion. |

---

## 4. Ordner auswählen

![Folder selection](capturas/seleccion-carpetas.png)

1. Klicken Sie auf den **„Ordner auswählen…“**-Button (Ordnersymbol).
2. Der standardmäßige macOS-Dialog öffnet sich. Wählen Sie **einen oder mehrere Ordner** aus, indem Sie ⌘ (Befehl) gedrückt halten.
3. Die Ordner **sammeln sich** in der Liste. Sie können bei weiteren Auswahlen weitere Ordner hinzufügen.
4. Um die Auswahl zu löschen, klicken Sie auf den **„Löschen“**-Button (✕-Symbol), der daneben erscheint.

> Der **„Scan starten“**-Button bleibt deaktiviert, bis mindestens ein Ordner ausgewählt ist. Sie können auch einen Ordner aus dem Finder direkt auf das Fenster ziehen.

---

## 5. Erkennungsmodi

DuplicateFinder bietet zwei Modi, die über ein segmentiertes Steuerelement in der oberen Leiste ausgewählt werden können:

| Modus | Beschreibung |
|-------|--------------|
| **Zuverlässig** | Berechnet den SHA-256-Hash des **vollständigen Inhalts** jeder Datei. Garantiert keine Fehlalarme, ist aber langsamer, da jede Datei gelesen wird. |
| **Name + Größe** | Vergleicht nur den Namen (Groß-/Kleinschreibung nicht beachtet) und die Größe in Bytes. Sehr schnell (kein Dateilesen), kann aber Fehlalarme produzieren, wenn unterschiedliche Dateien denselben Namen und dieselbe Größe haben. |

> Der Standardmodus wird in **Einstellungen → Erkennung** festgelegt.

---

## 6. Scanfortschritt

Während eines Scans zeigt die obere Leiste die aktuelle Phase an:

| Phase | Anzeige |
|-------|---------|
| **Scannen…** | Zähler der verarbeiteten Dateien im Ordner. |
| **Vergleichen…** | Fortschrittsbalken mit Anzahl der berechneten Hashes von der Gesamtzahl der Kandidaten. |
| **Berechnen…** | Fortschritt der Datenbank-Einfügung und Aggregatberechnung. |
| **Abgeschlossen** | Grünes Häkchensymbol. |
| **Abgebrochen** | Orangefarbenes Symbol. |

Sie können den Scan jederzeit durch Klicken auf den **„Abbrechen“**-Button beenden.

---

## 7. Ergebnisse

![Results table](capturas/resultados.png)

Sobald der Scan abgeschlossen ist, wird die Ergebnistabelle mit den folgenden Spalten angezeigt:

| Spalte | Beschreibung |
|--------|--------------|
| **Name** | Dateiname mit seinem Symbol. |
| **Größe** | Größe jeder Kopie. |
| **Kopien** | Anzahl der Duplikate dieser Datei. |
| **Größe × Kopien** | Gesamtspeicherplatz aller Kopien. |
| **Speicherort** | Vollständiger Pfad jeder Kopie mit Aktions-Buttons. |

Sie können die Tabelle **sortieren**, indem Sie auf einen Spaltenkopf klicken. Sie können auch nach **Dateien** nach Namen oder Pfad suchen, indem Sie das Suchfeld unten verwenden.

### Statistikleiste

Oberhalb der Ergebnisse werden vier Kennzahlen angezeigt:

- **Gesamtdateien**: alle gescannten Dateien.
- **Duplikate**: Dateien, die zu einer Duplikatgruppe gehören.
- **Gruppen**: Gruppen identischer Dateien.
- **Wiedergewinnbar**: Speicherplatz, der freigegeben wird, wenn alle Duplikatkopien (minus eine pro Gruppe) entfernt werden.

---

## 8. Dateiaktionen

Jede doppelte Datei in der Spalte „Speicherort" hat Aktions-Buttons:

| Button | Aktion |
|--------|--------|
| 👁 (Auge) | Datei mit der Standardanwendung öffnen. |
| 📁 (Ordner) | Datei im Finder anzeigen. |
| 🗑 (Papierkorb) | In den Papierkorb verschieben (oder endgültig löschen, je nach Einstellung). |

### Stapellöschung

Sie können mehrere Dateien auswählen, indem Sie das quadratische Kästchen neben jeder Datei markieren:

1. Markieren Sie die Dateien, die Sie löschen möchten.
2. Der **„Ausgewählte löschen (N)“**-Button erscheint in der Statistikleiste.
3. Klicken Sie darauf, um die Löschung zu bestätigen und abzuschließen.

> Sie können das Löschverhalten in **Einstellungen → Allgemein** ändern: Umschalter „Dateien in den Papierkorb verschieben".

---

## 9. Ergebnisse exportieren

Klicken Sie auf den **„Export“**-Button (Teilen-Symbol) in der Statistikleiste und wählen Sie:

- **CSV** — Kommagetrennte Textdatei, kompatibel mit Excel, Numbers und Tabellenkalkulationen.
- **JSON** — Strukturiertes Format, ideal für die programmgesteuerte Verarbeitung.

Beide Formate enthalten **jede Kopie jeder doppelten Datei** (nicht nur eine pro Gruppe) mit den Feldern: Name, Pfad, Größe, Anzahl der Kopien, insgesamt belegter Speicherplatz und SHA-256-Hash.

Ein `NSSavePanel`-Dialog öffnet sich, um das Ziel und den Dateinamen auszuwählen.

---

## 10. Einstellungen

Drücken Sie `⌘,` (Befehl + ,), um die Einstellungen zu öffnen, die in vier Registerkarten organisiert sind.

### Allgemein

| Option | Beschreibung |
|--------|--------------|
| **Top N Ergebnisse** | Maximale Anzahl von Zeilen in der Ergebnistabelle (10–100.000). |
| **In den Papierkorb verschieben** | Wenn aktiviert, werden Dateien in den Papierkorb verschoben anstatt endgültig gelöscht. |
| **Behaltensstrategie** | Strategie zur automatischen Auswahl der zu behaltenden Kopie (älteste, neueste oder kürzester Pfad). |
| **Erscheinungsbild** | Heller, dunkler oder systemabhängiger Modus. |

### Erkennung

| Option | Beschreibung |
|--------|--------------|
| **Standardmodus** | Erkennungsmodus, der beim Öffnen der App ausgewählt ist. |

### Filter

| Option | Beschreibung |
|--------|--------------|
| **Min / Max Größe** | Größenbereich in Bytes. Dateien außerhalb dieses Bereichs werden ignoriert. |
| **Versteckte einschließen** | Versteckte Dateien und Ordner (beginnend mit `.`) einschließen. |
| **Symlinks folgen** | Wenn aktiviert, werden symbolische Links während des Scans verfolgt. |
| **Erlaubte Erweiterungen** | Kommagetrennte Liste (z. B. `jpg, png, mp4`). Leer = alle Erweiterungen. |
| **Ausgeschlossene Ordner** | Kommagetrennte Liste von Ordnernamen, die während des Scans übersprungen werden (z. B. `node_modules, .git`). |

### Sprache

Wechseln Sie die Oberflächensprache zwischen den 8 verfügbaren Sprachen. Die App muss möglicherweise neu gestartet werden, damit die Änderung vollständig übernommen wird.

---

## 11. Tipps und Best Practices

1. **Beginnen Sie mit dem Schnellmodus**, wenn Sie viele Ordner haben. Er ist viel schneller und findet möglicherweise die meisten Duplikate.
2. **Verwenden Sie den zuverlässigen Modus für endgültige Entscheidungen** vor dem Löschen – insbesondere wenn die Dateinamen nicht übereinstimmen – um Fehlalarme zu vermeiden.
3. **Wählen Sie bestimmte Ordner aus**, nicht Ihre gesamte Festplatte. Das Scannen nur von Downloads, Dokumenten und Schreibtisch reduziert Zeit und Rauschen drastisch.
4. **Überprüfen Sie die Speicherorte** in der Spalte „Speicherort" vor dem Löschen. Ein Duplikat könnte sich in einem Systemordner befinden, in dem es bleiben sollte.
5. **Exportieren Sie eine CSV**, bevor Sie aufräumen, um eine Aufzeichnung der gelöschten Dateien zu behalten.
6. **Richten Sie Filter ein**, wenn Sie nach bestimmten Dateitypen suchen (z. B. nur `.jpg`- und `.png`-Bilder).
7. **Verwenden Sie den „Löschen“-Button**, um mit einer neuen Ordnerauswahl frisch zu starten, ohne die App zu beenden.

---

> **DuplicateFinder** — [mdc](https://github.com/migueldc-oss/DuplicateFinder)
>
> Dokumentation erstellt am 1. Juli 2026.
