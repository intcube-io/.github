# .github

Org-weite Vorgaben für `intcube-io`.

## gitleaks (Pflicht-Check)

`.github/workflows/gitleaks.yml` ist der Pflicht-Workflow des Org-Rulesets
`gitleaks-required` (intcube-io/ops#1127). Er läuft bei jedem Pull Request
gegen den Default-Branch jedes nicht archivierten Repos und scannt die Commits
des PRs mit gitleaks. Ein Repo braucht dafür keine eigene Workflow-Datei. Ein
Fund macht den Check rot; die Ausgabe nennt Datei, Zeile, Commit und Regel,
nie den Wert (`--redact`).

Konfiguration und `.gitleaksignore` liest der Check vom **Base-Branch**, nicht
aus dem PR, und `gitleaks:allow`-Kommentare zählen nicht: sonst könnte ein PR
seine eigene Ausnahme mitbringen. Ein Fehlalarm wird deshalb in einem eigenen,
vorher gemergten PR per `.gitleaks.toml` (`[extend] useDefault = true` plus
enge, begründete Allowlist) erledigt. Ein echter Fund: Credential widerrufen;
den Commit zu entfernen reicht nicht, `refs/pull/<n>/head` bleibt.

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
