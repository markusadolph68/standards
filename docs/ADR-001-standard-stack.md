# ADR-001: Standard Tech Stack – markusadolph68

**Status:** Accepted  
**Datum:** 2026-04-29  
**Kontext:** Analyse von 13 Repos ergab inkonsistente Package Manager, fehlendes Testing und unklare Defaults.

---

## Entscheidungen

### Python

| Dimension | Standard | Begründung |
|-----------|----------|------------|
| Package Manager | **uv** | Ersetzt pip + venv + poetry; deutlich schneller; wächst zum De-facto-Standard |
| Testing | **pytest** | Minimaler Overhead, riesiges Ökosystem, keine Alternative nötig |
| Linting | **ruff** | Ersetzt flake8 + isort + black in einem Tool, sehr schnell |
| Python-Version | **3.12** | Aktuelle stabile Version; in `pyproject.toml` pinnen |
| Abhängigkeiten | `pyproject.toml` | Kein `requirements.txt` für neue Projekte |

**Pflichtstruktur neues Python-Repo:**
```
pyproject.toml        ← uv-managed, enthält Python-Version + deps
tests/
  test_*.py
.python-version       ← echo "3.12" > .python-version
```

---

### JavaScript / TypeScript

| Dimension | Standard | Begründung |
|-----------|----------|------------|
| Sprache | **TypeScript** | Kein neues reines JS; TS gibt es ab Tag 1 |
| Package Manager | **pnpm** | Schneller als npm/yarn, spart Disk durch globalen Cache |
| Testing | **Vitest** | Jest-kompatible API, native ESM, schneller |
| Linting | **ESLint + Prettier** | Bereits im Design System etabliert → konsequent übernehmen |
| Node-Version | **LTS (aktuell 22)** | In `.nvmrc` pinnen |
| Framework-Default | **kein Vorgabe** | Projektabhängig: Next.js für Web-Apps, Express/Fastify für APIs |

**Pflichtstruktur neues JS/TS-Repo:**
```
.nvmrc                ← "22"
pnpm-lock.yaml
tsconfig.json
.eslintrc.*
.prettierrc
tests/ oder *.test.ts
```

---

### Docker / Container

| Dimension | Standard | Begründung |
|-----------|----------|------------|
| Node Base Image | `node:22-alpine` | Minimal, aktuell |
| Python Base Image | `python:3.12-slim` | Bereits in security-scan verwendet, passt |
| Compose | Ja, für lokale Dev-Umgebung | Einheitliche `docker-compose.yml` in Projektwurzel |

---

### CI/CD

| Dimension | Standard |
|-----------|----------|
| System | GitHub Actions |
| Pflicht-Workflows | `ci.yml` (lint + test bei jedem PR), `release.yml` (optional) |
| Actions-Versionen | immer gepinnte Versionen (`actions/checkout@v4`) |

---

## Was bewusst *nicht* vereinheitlicht wird

- **Programmiersprache** – Python vs. TypeScript vs. Java bleibt projektabhängig
- **Web-Framework** – Next.js vs. Express vs. FastAPI je nach Use Case
- **Datenbank** – kein Vorgabe

---

## Migration bestehender Repos

| Repo | Handlungsbedarf |
|------|----------------|
| `ebf-essensbelege-app` | pytest + ruff hinzufügen |
| `agenticcodefactory` | pytest/vitest prüfen; npm → pnpm |
| `autocreditcard` | uv + pytest |
| `security-scan` | ruff hinzufügen (hat bereits poetry/uv) |
| `ebf-design-system` | npm → pnpm, Vitest hinzufügen |
| `Shadow-Coach` | Vitest hinzufügen, pnpm prüfen |
| `TokenEater` | Sprache unklar – bei nächstem Anfassen prüfen |

---

## Referenzen

- [uv Docs](https://docs.astral.sh/uv/)
- [Vitest](https://vitest.dev/)
- [ruff](https://docs.astral.sh/ruff/)
- [pnpm](https://pnpm.io/)
