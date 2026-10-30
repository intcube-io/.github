# .github

Org-weite Vorgaben für `intcube-io`.

## gitleaks (Pflicht-Check)

`.github/workflows/gitleaks.yml` ist der Pflicht-Workflow des Org-Rulesets
`gitleaks-required` (intcube-io/ops#1127). Er läuft bei jedem Pull Request
gegen den Default-Branch jedes nicht archivierten Repos und scannt die Commits
des PRs mit gitleaks. Ein Repo braucht dafür keine eigene Workflow-Datei. Ein
Fund macht den Check rot; die Ausgabe nennt Datei, Zeile, Commit und Regel,
nie den Wert (`--redact`).

Ein Fehlalarm wird im betroffenen Repo per `.gitleaks.toml` (Allowlist mit
Begründung) erledigt, nicht hier. Ein echter Fund: Credential widerrufen,
dann Commit entfernen, solange der PR offen ist.

## pre-commit

`templates/pre-commit-config.yaml` als `.pre-commit-config.yaml` ins Repo
kopieren:

```bash
brew install pre-commit
```

```bash
pre-commit install
```

Danach prüft gitleaks jeden Commit lokal, bevor er das Repo verlässt.
