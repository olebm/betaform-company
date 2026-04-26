---
key: "betaform/knowledge-base"
---

# Skill: Knowledge Base Management

Wissensdatenbank von betaform.io. Lebt in **BET-112** als Paperclip-Dokumente.
Wird wöchentlich freitags vom Operations Agent ausgeführt.

---

## Dokumentstruktur (BET-112)

| Key | Inhalt | Aktualisierung |
|---|---|---|
| `index` | Zentraler Index + Routing-Matrix | Bei jeder Änderung |
| `betaform-company-info` | Unternehmensprofil, Referenzen, USP | 14-tägig via Outreach Agent |
| `tech-setup` | Stack, Infra, n8n-Workflows, Credentials-Übersicht | CTO bei Änderungen |
| `icp` | Ideal Customer Profile (Sync mit BET-484) | Bei ICP-Änderungen |
| `agent-governance` | Aktive Agents, Budgets, Entscheidungsrahmen | Bei Struktur-Änderungen |

---

## Jeden Freitag — 3 Schritte

### Schritt 1 — [KB-UPDATE]-Kommentare verarbeiten

```
GET /api/issues/BET-112/comments
```

Für jeden Kommentar mit Präfix `[KB-UPDATE]`:
- Relevant und dauerhaft? → In passendes Dokument integrieren
- Einmalig / situativ? → Ignorieren, kurz bestätigen
- Kommentar nach Verarbeitung mit `[KB-DONE]` markieren

### Schritt 2 — Abgeschlossene Issues scannen

```
GET /api/companies/{companyId}/issues?status=done&limit=20
```

Wissenswürdig wenn ein Issue enthält:
- Neue Tools, APIs oder Integrationen eingeführt
- Strategische Entscheidungen (Modell, Budget, Prozess)
- Neue Clients, Branchen oder Projekttypen
- Agent-Änderungen (neue Rollen, Merges, Deprecations)
- Lessons Learned (was ist schiefgelaufen + warum)

Nicht dokumentieren: operative Routinearbeit, einzelne Emails, abgelehnte Leads.

### Schritt 3 — Index aktualisieren

Nach jeder Dokumentänderung:

```
# Erst lesen (baseRevisionId holen)
GET /api/issues/{bet-112-id}/documents/index

# Dann schreiben
PUT /api/issues/{bet-112-id}/documents/index
{
  "title": "KB Index",
  "format": "markdown",
  "body": "...",
  "baseRevisionId": "{latestRevisionId}"
}
```

---

## Dokument erstellen / aktualisieren

```
# Neu
PUT /api/issues/{issueId}/documents/{key}
{
  "title": "...",
  "format": "markdown",
  "body": "...",
  "baseRevisionId": null
}

# Update (immer erst GET → dann PUT mit baseRevisionId)
GET /api/issues/{issueId}/documents/{key}
PUT /api/issues/{issueId}/documents/{key}
{
  "title": "...",
  "format": "markdown",
  "body": "...",
  "baseRevisionId": "{latestRevisionId aus GET}"
}
```

---

## Dokumentformat (Pflicht-Header)

Jedes KB-Dokument beginnt mit:

```markdown
> **Letzte Aktualisierung:** YYYY-MM-DD (via [Quelle])
> **Verantwortlich:** Operations Agent
> **Nächste Aktualisierung:** [Frequenz oder Datum]
```

---

## Routing-Matrix

Welche Dokumente sind für welchen Agent relevant:

| Dokument | Operations | Outreach Agent | Response Agent | CTO | CDO |
|---|---|---|---|---|---|
| `index` | ✓ | | | | |
| `betaform-company-info` | ✓ | ✓ | | | |
| `tech-setup` | ✓ | | | ✓ | |
| `icp` | ✓ | ✓ | ✓ | | |
| `agent-governance` | ✓ | | | | |

Bei neuen Dokumenten: Routing-Matrix im `index` ergänzen.

---

## Benachrichtigung bei signifikanten Updates

Nur bei handlungsrelevantem neuem Wissen — nicht bei Routine-Updates:
- Neuer Prozess der einen Agent direkt betrifft → Kommentar im laufenden Issue des Agents
- Geänderte ICP-Kriterien → Kommentar auf BET-484 + Outreach Agent informieren
- Neue Tech-Entscheidung → Kommentar auf dem CTO-Heartbeat-Issue

Keine @-Mentions für Routine-Updates.

---

## Blockierungen

Fehlende Information für ein Update:
1. Kommentar in BET-112 mit `[KB-FRAGE]` + konkreter Frage
2. Zuständigen Agent @-mentionen (sparsam)
3. Operations-Issue auf `blocked` mit Begründung
