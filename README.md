# Standards – markusadolph68

Tech-Stack-Entscheidungen, Architecture Decision Records (ADRs)
und Entwicklungsrichtlinien.

## ADRs

| # | Titel | Status |
|---|-------|--------|
| [ADR-001](docs/ADR-001-standard-stack.md) | Standard Tech Stack | ✅ Accepted |

## Claude Code

[CLAUDE.md](CLAUDE.md) definiert die Regeln für Claude Code in allen Repos.
In neue Repos einfach kopieren:

```bash
curl -sO https://raw.githubusercontent.com/markusadolph68/standards/main/CLAUDE.md
```

## Neue ADR hinzufügen

```bash
cp docs/ADR-001-standard-stack.md docs/ADR-00X-thema.md
# bearbeiten, dann:
git add . && git commit -m "feat: add ADR-00X thema"
git push
```
