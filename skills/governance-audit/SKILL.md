---
key: "betaform/governance-audit"
---

# Skill: Governance Audit

Wird vom Operations Agent freitags ausgeführt — zusammen mit dem KB-Scan.
Zweck: sicherstellen dass die Struktur aus `GOVERNANCE.md` noch stimmt.

**Wichtig:** Abweichungen niemals selbst korrigieren. Immer Issue für Ole erstellen.

---

## Audit-Checkliste (jeden Freitag)

### 1. Aktive Agents prüfen

```
GET /api/companies/{companyId}/agents
```

Vergleiche mit der Agents-Tabelle in `GOVERNANCE.md`:
- Gibt es Agents die laut GOVERNANCE pausiert sein sollten, aber noch aktiv sind?
- Gibt es neue Agents die in GOVERNANCE nicht stehen?
- Liegt ein Agent bei ≥80% seines Monatsbudgets?

**Bei Abweichung:** Issue erstellen `⚠️ Governance: Unbekannter Agent — [Name]` | Assignee: Ole | Priority: high

### 2. Skill-Integrität prüfen

Stichprobe: einen aktiven Agent laden und prüfen ob seine Skills noch der Liste in GOVERNANCE entsprechen:

```
GET /api/agents/{agentId}
```

Erwartete Skills je Agent (aus GOVERNANCE):
- `operations`: paperclip, para-memory-files, shared-rules, knowledge-base, governance-audit
- `outreach-agent`: paperclip, para-memory-files, shared-rules, content-review, betaform-voice, betaform-design
- `response-sequence-agent`: paperclip, shared-rules, followup-sequences
- `cto`: paperclip, shared-rules, betaform-voice, betaform-design
- `cdo`: paperclip, image-generation, betaform-voice, betaform-design

**Bei Abweichung:** Kommentar auf Operations-Heartbeat-Issue, kein separates Issue nötig

### 3. Offene Issues ohne Assignee

```
GET /api/companies/{companyId}/issues?status=todo&limit=50
```

Issues ohne `assigneeAgentId` die älter als 48h sind → in Briefing an Ole erwähnen.

### 4. Budget-Gesamtcheck

Summe `spentMonthlyCents` aller aktiven Agents berechnen.
Limit laut GOVERNANCE: €8.000/Monat (€80 × 100 Cents).

Wenn Gesamtverbrauch > 80% des Limits → Warnung im Tages-Briefing.
Wenn Gesamtverbrauch > 100% → sofort Issue für Ole.

### 5. Strukturelle Drift-Signale

Scanne die letzten 20 abgeschlossenen Issues auf Muster die auf Drift hindeuten:
- Issues die außerhalb der 4 definierten Projekte erstellt wurden
- Issues bei denen ein Agent einen anderen Agent direkt beauftragt hat (sollte über Operations laufen)
- Issues mit Titles wie "Neuer Agent", "Agent anpassen", "Prompt ändern" — diese brauchen Ole-Approval

**Bei Drift-Signal:** `[Governance] Möglicher Drift — [Beschreibung]` als Kommentar auf Operations-Issue

---

## Audit-Report Format

Nach dem Audit einen Kommentar auf dem aktiven Operations-Heartbeat-Issue:

```
## Governance Audit — [Datum]

Agents: [OK / X Abweichungen]
Budget: [€X verbraucht von €80 (Y%)]
Offene Issues ohne Assignee: [Anzahl]
Drift-Signale: [keine / Beschreibung]

[Nur bei Problemen: konkrete Issues oder nächste Schritte]
```

Kein Fülltext wenn alles grün ist. Max. 6 Zeilen.

---

## CHANGELOG aktualisieren

Nach jeder strukturellen Änderung die Ole genehmigt hat:
`PUT /api/issues/{changelog-issue-id}/documents/changelog` mit neuem Eintrag.

Format:
```
## [YYYY-MM-DD] — [Titel der Änderung]
- Was: [konkrete Änderung]
- Warum: [Begründung]
- Autorisiert: Ole Beekmann
```
