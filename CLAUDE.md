# CLAUDE.md

Dieses File steuert das Verhalten von Claude Code in allen Repos dieses Accounts.
Abweichungen von diesen Regeln erfordern explizite Begründung im Chat.

---

## Identität & Kontext

- Account: markusadolph68
- Schwerpunkt: Python-Tools, TypeScript-Web-Apps, DevOps/Automation
- Standard-Dokument: siehe `STANDARD_STACK.md` (im Root dieses Repos oder unter github.com/markusadolph68/standards)

---

## Pflichtregeln – Tech Stack

### Python
- Package Manager: **uv** – niemals `pip install` direkt, immer `uv add`
- Testing: **pytest** – bei jeder neuen Datei mit Logik direkt einen Test anlegen
- Linting: **ruff** – kein flake8, kein black, kein isort separat
- Python-Version: **3.12** – in `pyproject.toml` unter `[project] requires-python = ">=3.12"`
- Keine `requirements.txt` in neuen Projekten – nur `pyproject.toml`

### JavaScript / TypeScript
- Sprache: **TypeScript** – kein reines JavaScript in neuen Dateien
- Package Manager: **pnpm** – niemals `npm install` oder `yarn add` vorschlagen
- Testing: **Vitest** – kein Jest für neue Projekte
- Linting: **ESLint + Prettier** – Konfiguration aus `ebf-design-system` als Vorlage

### Docker
- Node Base Image: `node:22-alpine`
- Python Base Image: `python:3.12-slim`
- Immer ein `docker-compose.yml` für lokale Entwicklung anlegen

### CI/CD
- System: **GitHub Actions**
- Jedes neue Repo bekommt `.github/workflows/ci.yml` mit lint + test
- Actions nur mit gepinnten Versionen: `actions/checkout@v4`

---

## Verhaltensregeln für Claude

### Vor dem Coden
- Prüfe ob ein `pyproject.toml` / `pnpm-lock.yaml` existiert – wenn ja, existierenden Stack respektieren
- Frage NICHT nach dem bevorzugten Package Manager oder Testing-Framework – die Antwort steht hier
- Schlage KEINE Alternativen zu den oben definierten Tools vor, außer ich frage explizit danach

### Beim Coden
- Neue Python-Dateien: direkt zugehörige `test_*.py` in `/tests` anlegen
- Neue TS-Dateien: zugehörige `*.test.ts` anlegen wenn sinnvoll
- Imports immer mit korrektem Type-Safety (kein `any` ohne Kommentar)
- Keine `console.log` in Commits – nur strukturiertes Logging

### Abhängigkeiten
- Vor `uv add` / `pnpm add`: kurz erklären warum diese Dependency nötig ist
- Keine Abhängigkeiten hinzufügen die eine bereits vorhandene ersetzen würden, ohne Rückfrage
- Bevorzuge stdlib / kleine Libraries gegenüber großen Frameworks

### Kommunikation
- Antworte auf Deutsch, außer der Code selbst (Kommentare, Variablennamen auf Englisch)
- Kurze, präzise Antworten – kein Padding
- Bei Unklarheiten: eine konkrete Frage stellen, nicht mehrere

---

## Was Claude NICHT tun soll

- `pip install` statt `uv add` vorschlagen
- `npm` oder `yarn` statt `pnpm` verwenden
- Jest in neuen Projekten einrichten
- `requirements.txt` in neuen Repos anlegen
- Neue Sprachen/Frameworks einführen ohne explizite Freigabe
- Code ohne Fehlerbehandlung schreiben (kein nacktes `except: pass`)

---

## Ausnahmen

Wenn ein bestehendes Repo einen abweichenden Stack hat (z.B. `EBF-Linkara` mit Java),
gilt für dieses Repo der vorhandene Stack. CLAUDE.md überschreibt nicht die lokale Realität,
sondern definiert den Standard für neue Projekte und neue Dateien.
