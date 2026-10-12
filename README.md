# Computational Basics – Übung (WS 26)

Dieses Repo enthält die Programmierübungen und das Skriptum. Die komplette
Python-Umgebung ist im Repo definiert. Du musst nur **ein** Tool installieren
(`uv`), das Repo klonen und **einen** Befehl ausführen.

## 1. Einmalig installieren

Folgende Tools müssen installiert werden damit der Code am Ende läuft. 

| Tool | Windows | Mac |
|---|---|---|
| **uv** | `winget install --id=astral-sh.uv -e` | `brew install uv` (oder `curl -LsSf https://astral.sh/uv/install.sh \| sh`) |
| **git** | `winget install --id=Git.Git -e` | `git --version` öffnen – Xcode Command Line Tools werden angeboten |
| **VS Code** | `winget install --id=Microsoft.VisualStudioCode -e` | `brew install --cask visual-studio-code` |

> Weitere Informationen zur Installation gibt es direkt auf den Websites:
> [https://code.visualstudio.com/](https://code.visualstudio.com/)
> [https://git-scm.com/install/](https://git-scm.com/install/)
> [https://docs.astral.sh/uv/getting-started/installation/][https://docs.astral.sh/uv/getting-started/installation/]

> **Wichtig:** Terminal (und VS Code) nach der Installation **schließen und neu
> öffnen**, sonst findet das System die neuen Befehle nicht.
> Python laden wir dann über uv nochmal runter falls ihr es jetzt noch nicht auf eurem PC habt.

## 2. Repository von Github holen

Wenn eine dieser Optionen nicht funktioniert, eine der anderen Optionen ausprobieren.

1. In VS Code: **Strg/Cmd+Shift+P → "Git: Clone"**, URL einfügen:
`https://github.com/VeiderFa/computationalbasics26exercise.git`,
Ordner für den Kurs wählen oder erstellen, dann **Open**.

2. Ein Terminal öffnen (extern oder in VS Code via **Ctrl + J**), in einen Ordner der Wahl für den Kurs wechseln und dann folgenden Befehl eingeben: `git clone https://github.com/VeiderFa/computationalbasics26exercise.git`

3. Auf GitHub rechts oben auf **Code → Download ZIP** klicken, das Download in einen passenden Ordner wechseln und entpacken (extract here).

Bei Fehlermeldungen gleich melden, wir besprechen dann mögliche Lösungsmöglichkeiten.

## 3. Umgebung erstellen (einmalig)

In VS Code den Ordner wo jetzt das Github-Repository reingeladen wurde durch **File → Open Folder** aufmachen
Terminal in VS Code öffnen (**Strg+J** oder ganz rechts oben **Toggle Panel** anklicken) und im Terminal folgenden Befehl ausführen:

```
uv sync
```

Das lädt die passende Python-Version (und installiert Python falls es noch nicht installiert wurde), erstellt eine virtuelle Umgebung `.venv/` und installiert alle Pakete die wir brauchen für den Kurs. Du musst **nichts aktivieren**.

## 4. VS Code Extensions

Wenn VS Code fragt, die **empfohlenen Extensions** (Python und Jupyter) zu
installieren: **Installieren** klicken. Ansonsten können dieselinks bei dem Symbol mit vier Rechtecken runtergeladen werden.

## 5. Testen

`check_setup.ipynb` öffnen (im Explorer link oben im Ordner **computationalbasics26exercise**) → oben rechts **Select Kernel → Python
Environments → .venv** → Zelle ausführen. Es muss `Setup OK` erscheinen.
VS Code wählt `.venv` meist automatisch.

## 6. Arbeiten

- **Alle** Notebooks und Skripte laufen mit dem **Repo-Ordner als
  Arbeitsverzeichnis**. Öffne VS Code immer im Repo-Hauptordner, nicht in
  einem Unterordner. Datendateien wie `labormarket.csv` liegen deshalb im
  Hauptordner.
- **Notebook:** öffnen, Kernel `.venv` wählen, starten.
- **Python-Skript:** VS Code Run-Knopf, oder im Terminal
  `uv run python Programme/Programm6.py`.

## Paket-Änderungen (nur Lehrperson)

`uv add <paket>`, dann `pyproject.toml`, `uv.lock` und `.python-version`
committen. Danach: `git pull` und `uv sync`.

## Häufige Probleme

- **`command not found: uv`** – Terminal/VS Code neu öffnen.
  **Windows:** Meldet `uv --version` „uv wird nicht erkannt"? VS Code komplett
  schließen und neu öffnen (VS Code übernimmt die PATH-Änderung nur beim
  Neustart des Fensters). In einem bereits offenen Terminal hilft:
  `$env:Path += ";$env:USERPROFILE\.local\bin"`.
  Fehlt der Pfad dauerhaft:
  `[Environment]::SetEnvironmentVariable("Path", "$env:USERPROFILE\.local\bin;$([Environment]::GetEnvironmentVariable('Path','User'))", "User")`
  und ein neues Terminal öffnen.
- **`ModuleNotFoundError` im Notebook** – falscher Kernel. Oben rechts muss
  `.venv` stehen. Fragt VS Code nach `ipykernel`, ist der falsche Kernel
  gewählt (`ipykernel` ist bereits im Repo enthalten).
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
3. `check_setup.ipynb` öffnen → **Select Kernel → Python Environments → .venv**
   → Zelle ausführen. Es muss `Setup OK` erscheinen.

Die Notebooks brauchen nur `numpy`, `pandas` und `matplotlib` – kleinere
Versionsunterschiede sind egal. `.venv/` steht schon in `.gitignore`, es wird
also nichts ins Repo committen. Funktioniert `uv` nachträglich doch, ersetzt
`uv sync` diese Umgebung einfach.

## Nie tun

- `.venv/` **nicht** ins Repo committen (steht schon in `.gitignore`).
- Notebooks, die die Lehrperson aktualisiert, nicht direkt bearbeiten –
  vorher kopieren (z. B. `Kapitel6_kopie.ipynb`), sonst gibt es beim
  `git pull` Konflikte.
