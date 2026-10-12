# Computational Basics – Übung (WS 26)

Dieses Repo enthält die Programmierübungen und das Skriptum. Die komplette
Python-Umgebung ist im Repo definiert. Du musst nur **ein** Tool installieren
(`uv`), das Repo klonen und **einen** Befehl ausführen.

## 1. Einmalig installieren

| Tool | Windows | Mac |
|---|---|---|
| **uv** | `winget install --id=astral-sh.uv -e` | `brew install uv` (oder `curl -LsSf https://astral.sh/uv/install.sh \| sh`) |
| **git** | `winget install --id=Git.Git -e` | `git --version` öffnen – Xcode Command Line Tools werden angeboten |
| **VS Code** | `winget install --id=Microsoft.VisualStudioCode -e` | `brew install --cask visual-studio-code` |

> Falls du VS Code noch nicht in der ersten Vorlesung installiert hast, kannst du
> es auch direkt von der Website herunterladen:
> [https://code.visualstudio.com/](https://code.visualstudio.com/)

> **Wichtig:** Terminal (und VS Code) nach der Installation **schließen und neu
> öffnen**, sonst findet das System die neuen Befehle nicht.

## 2. Repository holen

Wenn eine dieser Optionen nicht funktioniert, eine der anderen ausprobieren.

1. In VS Code: **Strg/Cmd+Shift+P → "Git: Clone"**, URL einfügen:
`https://github.com/VeiderFa/computationalbasics26exercise.git`,
Ordner wählen, dann **Open**.

2. Ein Terminal öffnen, in einen Ordner wechseln und dann folgenden Befehl eingeben: `git clone https://github.com/VeiderFa/computationalbasics26exercise.git`

3. Auf GitHub rechts oben auf **Code → Download ZIP** klicken, das Download in einen passenden Ordner wecheslen und entpacken (extract here).

## 3. Umgebung erstellen (einmalig)

In VS Code den Ordner mit dem Github-Repository durch **File → Open Folder** aufmachen
Terminal in VS Code öffnen (**Strg+J** oder ganz rechts oben **Toggle Panel** anklicken) und im Terminal folgenden Befehl ausführen:

```
uv sync
```

Das lädt die passende Python-Version, erstellt eine virtuelle Umgebung `.venv/` und installiert alle
Pakete die wir brauchen für den Kurs. Du musst **nichts aktivieren**.

## 4. VS Code Extensions

Wenn VS Code fragt, die **empfohlenen Extensions** (Python und Jupyter) zu
installieren: **Installieren** klicken.

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
- **`ModuleNotFoundError` im Notebook** – falscher Kernel. Oben rechts muss
  `.venv` stehen. Fragt VS Code nach `ipykernel`, ist der falsche Kernel
  gewählt (`ipykernel` ist bereits im Repo enthalten).
- **Etwas ist kaputt** – Ordner `.venv` löschen und `uv sync` erneut
  ausführen. Das behebt fast alles.
- **Keine Internetverbindung zum Python-Download** – Python von
  [python.org](https://www.python.org/downloads/) installieren; `uv` nutzt es
  dann automatisch.

## Nie tun

- `.venv/` **nicht** ins Repo committen (steht schon in `.gitignore`).
- Notebooks, die die Lehrperson aktualisiert, nicht direkt bearbeiten –
  vorher kopieren (z. B. `Kapitel6_kopie.ipynb`), sonst gibt es beim
  `git pull` Konflikte.
