# Computational Basics – Übung (WS 26)

Dieses Repo enthält die Programmierübungen und das Skriptum. Die komplette
Python-Umgebung ist im Repo definiert. Du musst nur **ein** Tool installieren
(`uv`), das Repo klonen und **einen** Befehl ausführen.

**Wie lange dauert das?** Rund 20 Minuten, wenn alles glatt läuft. Arbeite die
Schritte der Reihe nach ab und mach bei jedem Schritt die kleine „Passt das?"
-Prüfe, bevor du weitermachst.

**Wenn gar nichts klappt** (kein `uv` installierbar, kein Terminal, kein
VS Code): Du kannst die Übungen komplett **im Browser** mit Google Colab
machen – nichts installieren, alles läuft in der Cloud. Siehe
[Plan B: Google Colab](#funktioniert-gar-nichts-google-colab-als-plan-b).

## 0. Begriffe, die du hier überall siehst

Kein Vorwissen nötig, das sind die wichtigsten Begriffe die auch in der Vorlesung vorkommen:

| Begriff | Bedeutung |
|---|---|
| **Terminal** | Ein Fenster, in das du Befehle tippst und mit Enter ausführst. Statt Mausklicks also Tastatureingaben. |
| **Repository (Repo)** | Der Projektordner, der bei GitHub liegt – bei uns `computationalbasics26exercise`. |
| **Klonen** | Eine Kopie des Repos von GitHub auf deinen Rechner laden (Befehl `git clone`). |
| **VS Code** | Der Editor, in dem wir Code schreiben und Notebooks öffnen. |
| **Notebook (`.ipynb`)** | Eine Datei mit Code-Zellen. Du führst Zelle für Zelle ausführst und siehst direkt das Ergebnis darunter. |
| **`.venv`** | Unsere fertige Python-Umgebung im Repo-Ordner. Enthält Python plus alle nötigen Pakete. Du musst sie **nicht** aktivieren. |
| **Kernel** | „Welches Python benutzt das Notebook gerade?" – oben rechts in VS Code eingestellt, muss `.venv` sein. |
| **Arbeitsverzeichnis** | Der Ordner, von dem aus der Code läuft. Bei uns immer der Repo-Hauptordner. |

Tastatur-Kürzel: **Strg** ist die Taste auf Windows, **⌘ (Cmd)** auf Mac. Wenn
unten „Strg/⌘+J" steht, drück also Strg+J (Windows) oder ⌘+J (Mac).

## 1. Einmalig installieren

Folgende Tools müssen installiert werden, damit der Code am Ende läuft.
Öffne zuerst ein **Terminal**:

- **Windows:** Start-Menü öffnen, `Terminal` eintippen, öffnen (Powershell ist
  auch okay).
- **Mac:** ⌘+Leertaste, `Terminal` eintippen, Enter.

Dann je Tool den Befehl für dein Betriebssystem einfügen. Einfügen im Terminal
geht mit **Rechtsklick → Einfügen** (im Mac-Terminal: ⌘+V). Mit **Enter**
wird der Befehl ausgeführt.

| Tool | Windows | Mac |
|---|---|---|
| **uv** | `winget install --id=astral-sh.uv -e` | `brew install uv` (oder `curl -LsSf https://astral.sh/uv/install.sh \| sh`) |
| **git** | `winget install --id=Git.Git -e` | `git --version` öffnen – Xcode Command Line Tools werden angeboten |
| **VS Code** | `winget install --id=Microsoft.VisualStudioCode -e` | `brew install --cask visual-studio-code` |

> Weitere Informationen zur Installation gibt es direkt auf den Websites:
> [https://code.visualstudio.com/](https://code.visualstudio.com/),
> [https://git-scm.com/install/](https://git-scm.com/install/),
> [https://docs.astral.sh/uv/getting-started/installation/](https://docs.astral.sh/uv/getting-started/installation/)

**Passt das?** Tippe als Kontrolle `uv --version` und dann `git --version` ins
Terminal und drück Enter. Wenn versionsnummern ausgedruckt werden, ist das Tool
installiert. „Befehl nicht gefunden" bzw. „command not found" heißt: siehe
[Häufige Probleme](#häufige-probleme).

> **Wichtig:** Terminal (und VS Code) nach der Installation **schließen und neu
> öffnen**, sonst findet das System die neuen Befehle nicht.
> Python laden wir dann über uv nochmal runter, falls ihr es jetzt noch nicht
> auf eurem PC habt.

## 2. VS Code Basics

1. VS Code öffnen (Windows: Start-Menü → „Visual Studio Code"; Mac: ⌘+Leertaste
   → „Visual Studio Code").
2. Beim ersten Start fragt VS Code nach einem **Design** (Dark oder Light) –
   egal, einfach eines aussuchen und auf **Next** klicken.
3. VS Code fragt „Do you trust the authors of the files in this Folder?" –
   das ist unser Kursmaterial: auf **Yes, I trust the authors** klicken.

Das Fenster hat drei wichtige Bereiche:

- **Links der Explorer** (Ordner-Ansicht). Wenn du ihn nicht siehst: das
  Ordner-Symbol ganz oben in der linken Leiste anklicken (oder Strg/⌘+Shift+E).
- **Mitte der Editor.** Jede geöffnete Datei wird ein **Tab** oben im Editor.
  Ein Tab schließt du mit dem **×**.
- **Unten das Panel** (Terminal, Probleme, …). Öffnet sich mit **Strg/⌘+J**.

## 3. Repository von GitHub holen

Wenn eine dieser Optionen nicht funktioniert, eine der anderen ausprobieren.
**Option 1 ist empfohlen.**

### Option 1: Klonen über VS Code

1. Drück **Strg/⌘+Shift+P**. Ganz oben öffnet sich eine **Kommando-Palette**
   (ein Eingabefeld mit einer Leiste).
2. Tippe `Git: Clone` und drück **Enter**.
3. Es erscheint ein weiteres Feld: die URL
   `https://github.com/VeiderFa/computationalbasics26exercise.git`
   einfügen (Strg/⌘+V) und **Enter** drücken.
4. Jetzt fragt VS Code nach einem **Ordner**, in den geklont werden soll.
   Wähle einen Ort für deine Kursordner (z. B. `Dokumente/Kurse`), ggf. vorher
   über das Feld „New Folder" einen neuen Ordner anlegen.
5. Unten rechts fragt VS Code: **Open?** → auf **Open** klicken. VS Code öffnet
   das Repo.

### Option 2: Klonen über das Terminal

1. Öffne ein Terminal – in VS Code mit **Strg/⌘+J**, dann oben im Panel den
   Reiter **Terminal** anklicken (Windows alternativ: Start-Menü → Terminal).
2. Wechsle in den Ordner, in den das Repo soll. Das machst du mit `cd`
   („change directory"), danach Enter:
   - Windows: `cd C:\Users\DeinName\Dokumente\Kurse`
   - Mac: `cd /Users/DeinName/Dokumente/Kurse`
   - Tipp: `cd ` tippen (mit Leerzeichen), dann den Ordner aus dem Finder /
     Explorer ins Terminal **ziehen** – dann wird der Pfad automatisch
     eingefügt.
3. Dann eintippen und Enter ausführen:
   `git clone https://github.com/VeiderFa/computationalbasics26exercise.git`
4. Öffne anschließend in VS Code diesen Ordner: **File → Open Folder…** und
   wähle `computationalbasics26exercise`.

### Option 3: ZIP herunterladen

1. Auf GitHub rechts oben auf **Code → Download ZIP** klicken.
2. In den Download-Ordner wechseln, Rechtsklick auf die ZIP-Datei →
   **Hier entpacken** (Mac: Doppelklick).
3. In VS Code **File → Open Folder…** → den entpackten Ordner öffnen.

> Achtung: Bei dieser Variante fehlt der `.git`-Ordner. Du kannst das Repo
> dann **nicht** per `git pull` aktualisieren – versuch deshalb immer zuerst
> Option 1 oder 2.

Bei Fehlermeldungen gleich melden, wir besprechen dann mögliche
Lösungsmöglichkeiten.

## 4. Umgebung erstellen (einmalig)

1. Falls nicht schon geschehen: das Repo in VS Code öffnen –
   **File → Open Folder…** und den Ordner `computationalbasics26exercise`
   (den mit dem README.md) auswählen. **Immer den Hauptordner öffnen, nie
   einen Unterordner.**
2. Terminal öffnen: **Strg/⌘+J** (oder das Terminal-Symbol im Panel) und den
   Reiter **Terminal** anklicken.
3. Tippe ein:
   ```
   uv sync
   ```
   und drück **Enter**. Das lädt ein paar Sekunden bis ein paar Minuten.
4. Am Ende sollte etwas wie `Installed x packages` oder `Audited x packages`
   stehen – kein `error`.

Das lädt die passende Python-Version (und installiert Python, falls es noch
nicht installiert wurde), erstellt die virtuelle Umgebung `.venv/` und
installiert alle Pakete, die wir für den Kurs brauchen. Du musst **nichts
aktivieren**.

## 5. VS Code Extensions

Extensions sind Zusatzprogramme, die VS Code neue Funktionen geben. Wir
brauchen zwei: **Python** und **Jupyter**.

- Wenn VS Code beim Öffnen des Repos rechts oben nach den **empfohlenen
  Extensions** fragt: auf **Install** klicken, fertig.
- Falls nicht: links in der Aktivitätsleiste das **Symbol mit den vier
  Rechtecken** (Extensions) anklicken, oben in die Suche `Python` tippen →
  beim Eintrag von Microsoft auf **Installieren**. Dann dasselbe für
  `Jupyter`.

**Passt das?** In der linken Leiste sollte unten „Python" und „Jupyter" unter
*Installed* stehen.

## 6. Testen

1. Im **Explorer** (links oben unter File und Edit, Ordner-Symbol) den Hauptordner
   `computationalbasics26exercise` aufklappen und **`check_setup.ipynb`**
   anklicken. Die Datei öffnet sich als Tab im Editor.
2. Oben rechts im Notebook steht jetzt **Select Kernel** (oder ein Python-
   Symbol). Anklicken und wählen:
   **Python Environments → `.venv`** bzw. `computationalbasics26exercise`** (ggf. erst auf **Python Kernel** klicken, dann auswählen).
   VS Code wählt `.venv` meist automatisch – dann steht dort schon der richtige
   Name.
3. In die erste Zelle klicken (die mit `import sys, …`) und oben im
   Zellen-Rand auf das **▶**-Dreieck klicken – oder **Shift+Enter** drücken.
4. Unter der Zelle muss folgendes erscheinen (Werte dürfen abweichen):
   ```
   Python: 3.13.x ...
   numpy ... | pandas ... | matplotlib ...
   Setup OK
   ```

**Passt das?** Sobald `Setup OK` da ist, ist deine Umgebung fertig. 

## 7. Arbeiten mit dem VS Code Setup

### Grundsätzliches

- **Öffne VS Code immer im Repo-Hauptordner** (`File → Open Folder…` →
  `computationalbasics26exercise`), nie in einem Unterordner. Alle Notebooks
  und Skripte laufen mit dem Repo-Ordner als Arbeitsverzeichnis – Datendateien
  wie `labormarket.csv` liegen deshalb auch dort.
- **Geöffnete Dateien sind Tabs** oben im Editor. Zwischen Tabs wechselst du
  mit einem Klick; schließen mit dem **×**. Verschiedene Dateien nebeneinander
  anzeigen geht, indem du den Tab aus der Mitte an die Fensterkante ziehst
  (geteilte Ansicht).
- **Neue Datei/Ordner im Explorer:** Rechtsklick im Explorer → **New
  File… / New Folder…**.

### Notebooks (`.ipynb`)

1. Im Explorer das Notebook anklicken (z. B.
   `Übungen/Kapitel2_UE.ipynb`).
2. Falls oben rechts nicht `.venv` steht: **Select Kernel → Python
   Environments → `.venv`** bzw. `computationalbasics26exercise`** (siehe [Testen](#6-testen)).
3. In eine Zelle klicken und **Shift+Enter** ausführen – Ergebnis erscheint
   direkt darunter. Mit **Shift+Enter** landest du automatisch in der nächsten
   Zelle.
4. Neue Zelle: **+ Code** (oben rechts) oder mit der Maus zwischen zwei Zellen
   am linken Rand.
5. Speichern: **Strg/⌘+S** (wichtig vor dem Schließen!).

### Python-Skripte (`.py`)

- **Über den Run-Knopf:** Datei öffnen, oben rechts im Editor das **▶**
  anklicken. Die Ausgabe erscheint unten im Terminal.
- **Über das Terminal** (Strg/⌘+J → Reiter Terminal), z. B.:
  ```
  uv run python Programme/Programm6.py
  ```

### Repo aktualisieren, wenn es neue Aufgaben oder Updates von den Lehrenden gibt

In einem Terminal im Repo-Hauptordner (`computationalbasics26exercise`**):
```
git pull
uv sync
```
Dann die betroffenen Dateien in VS Code neu öffnen. Vor dem Pull eigene
Änderungen an den Übungsnotebooks sichern – siehe [Nie tun](#nie-tun).

## Paket-Änderungen (für Lehrende)

`uv add <paket>`, dann `pyproject.toml`, `uv.lock` und `.python-version`
committen. Danach: `git pull` und `uv sync`.

## Häufige Probleme

- **`command not found: uv`** – Terminal/VS Code neu öffnen.
  **Windows:** Meldet `uv --version` „uv wird nicht erkannt"? VS Code komplett
  schließen und neu öffnen (VS Code übernimmt die PATH-Änderung nur beim
  Neustart des Fensters). 
- **`ModuleNotFoundError` im Notebook** – falscher Kernel. Oben rechts muss
  `.venv` bzw. `computationalbasics26exercise`** stehen. Fragt VS Code nach `ipykernel`, ist der falsche Kernel
  gewählt (`ipykernel` ist bereits im Repo enthalten).
- **Der Tab zeigt „(unrestricted mode)" oder der Run-Knopf fehlt** – VS Code
  vertraut dem Ordner nicht. Links unten (oder über das Schloss-Symbol) auf
  **Manage → Trust** klicken.
- **Etwas ist kaputt** – Ordner `.venv` löschen und `uv sync` erneut
  ausführen. Das behebt fast alles.
- **Keine Internetverbindung zum Python-Download** – Python von
  [python.org](https://www.python.org/downloads/) installieren; `uv` nutzt es
  dann automatisch.

## Funktioniert uv nicht? Workaround

Wenn `uv` nicht installierbar ist oder `uv sync` nicht klappt, reicht eine
ganz normale Python-Umgebung, um die Notebooks trotzdem laufen zu lassen:

1. Python von [python.org](https://www.python.org/downloads/) installieren
   (Version ≥ 3.13; bei Windows das Häkchen **"Add Python to PATH"** setzen).
2. Im Repo-Ordner ein Terminal öffnen und ausführen:
   ```powershell
   python -m venv .venv
   .venv\Scripts\python -m pip install --upgrade pip
   .venv\Scripts\python -m pip install ipykernel numpy pandas matplotlib
   ```
   (Mac/Linux stattdessen: `.venv/bin/python -m pip install ...`)
3. `check_setup.ipynb` öffnen → **Select Kernel → Python Environments → .venv** bzw. `computationalbasics26exercise`**
   → Zelle ausführen. Es muss `Setup OK` erscheinen.

Die Notebooks brauchen nur `numpy`, `pandas` und `matplotlib`, kleinere
Versionsunterschiede sind egal. `.venv/` steht schon in `.gitignore`, es wird
also nichts ins Repo committen. Funktioniert `uv` nachträglich doch, ersetzt
`uv sync` diese Umgebung einfach. Klappt auch das nicht, geht es ohne
lokale Installation weiter – siehe
[Plan B: Google Colab](#funktioniert-gar-nichts-google-colab-als-plan-b).

## Funktioniert gar nichts? Google Colab als Plan B

Wenn `uv`, `git` oder VS Code sich nicht installieren lassen (kein
Admin-Recht, kein Python, fremder Laptop …), kannst du die Übungen komplett
**im Browser** mit **Google Colab** machen. Dort läuft alles in der Cloud –
du installierst nichts und brauchst nur ein Google-Konto und eine
Internetverbindung.

### Wie Colab funktioniert

Colab ist „Jupyter im Browser": dieselben `.ipynb`-Notebooks wie bei uns,
nur laufen die Zellen nicht auf deinem Rechner, sondern auf einem Server von
Google. Übungen und Skriptum liegen also weiterhin auf Moodle und in GitHub, nur die
*Ausführung* passiert woanders.

- **Vorteil:** keine Installation, kein Terminal, funktioniert auf jedem
  Gerät.
- **Nachteil:** deine Dateien liegen auf Google-Servern, eine Sitzung kann
  unterbrochen werden, und `git pull`/`uv sync` gibt es dort nicht.

### 1. Colab öffnen

1. Geh auf [https://colab.research.google.com](https://colab.research.google.com)
   und melde dich mit deinem Google-Konto an.
2. Über **File → New notebook** öffnet sich eine leere Zelle. Für unser
   Material brauchen wir aber die Dateien aus dem Repo/Moodle (Schritt 2).

### 2. Die Notebooks aus dem Repo holen

1. **File → Open notebook…** anklicken und den Reiter **GitHub** wählen.
2. In das Suchfeld die Repo-URL einfügen:
   `https://github.com/VeiderFa/computationalbasics26exercise`
   und **Enter** drücken.
3. Colab zeigt die Notebooks des Repos – z. B. `check_setup.ipynb` und
   `Übungen/Kapitel2_UE.ipynb`. Ein Notebook anklicken, es öffnet sich in
   einem Colab-Tab.


### 3. Pakete prüfen

`numpy`, `pandas` und `matplotlib` sind in Colab schon vorinstalliert – ein
`pip install` ist meist nicht nötig. Zum Nachsehen reicht in einer Zelle:

```python
import numpy, pandas, matplotlib
print(numpy.__version__, pandas.__version__, matplotlib.__version__)
```

Fehlt doch ein Paket, installierst du es in einer Zelle mit
`!pip install <paketname>`.

### 4. Daten und Skripte hochladen

In Colab ist das Arbeitsverzeichnis `/content` – dort landen auch die
Dateien, die du hochlädst. Deshalb funktionieren die relativen Pfade in den
Übungen, sobald die Datei dort liegt:

1. Links in der Seitenleiste auf das **Ordner-Symbol** (Files) klicken.
2. Oben auf das **Upload-Symbol** (Pfeil nach oben) klicken und
   `labormarket.csv` auswählen. Die Datei liegt danach in `/content`.
3. Für die Python-Skripte zusätzlich `Programme/Programm6.py` usw.
   hochladen und in einer Zelle starten:
   ```python
   !python Programm6.py
   ```
   (Die Skripte erwarten die CSV im selben Ordner – mit dem Upload nach
   `/content` ist das erfüllt.)

### 5. Rechnen

Wie in VS Code: Zelle anklicken und **Shift+Enter** drücken, das Ergebnis
erscheint darunter. **Runtime → Restart session…** setzt alles zurück, wenn
etwas hängt.

**Passt das?** Öffne `check_setup.ipynb` und führe alle Zellen aus. Es muss
`Setup OK` erscheinen – wie in VS Code.

### 6. Ergebnisse sichern

Das ist der wichtigste Unterschied zu VS Code: **In Colab landet nichts
automatisch auf deinem Rechner.** Die Notebooks liegen in deinem
Google-Konto, und die Sitzung wird nach ein paar Stunden beendet.

1. Nach dem Bearbeiten: **File → Download → Notebook (.ipynb)**.
2. Die heruntergeladene Datei zurück in den Repo-Ordner
   `computationalbasics26exercise` legen (bei den Übungsnotebooks nach
   `Übungen/`). Dann sind deine Lösungen wieder Teil des Repos und lassen
   sich wie gewohnt mit `git pull` aktualisieren.
3. Alternativ: in Colab **File → Save in Google Drive** und die Dateien
   dort bearbeiten – fürs Abgeben trotzdem exportieren.

### Grenzen von Colab

- Kein `uv`, kein `git pull`, kein `uv sync`: Aktualisierungen der
  Lehrenden holst du manuell (Notebook neu aus GitHub öffnen) – deine
  eigenen Änderungen vorher sichern, sonst sind sie weg.
- Pakete lassen sich nur mit `!pip install` nachinstallieren; eine `.venv`
  gibt es nicht.
- Bei hoher Auslastung kann Colab Sitzungen verlangsamen oder neu starten.
- Wenn die fertigen Notebooks im Repo abgegeben werden müssen, ist Colab nur
  eine Notlösung – am Ende brauchst du die `.ipynb`-Dateien im Repo-Ordner.

## Nie tun

- `.venv/` **nicht** ins Repo committen (steht schon in `.gitignore`).
- Notebooks, die die Lehrperson aktualisiert, nicht direkt bearbeiten –
  vorher kopieren (z. B. `Kapitel6_kopie.ipynb`), sonst gibt es beim
  `git pull` Konflikte.
