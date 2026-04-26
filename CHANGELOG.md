# betaform. — Changelog

Strukturelle Änderungen am Agent-Company-Setup.
Format: Datum | Bereich | Was geändert | Autorisiert von

---

## 2026-04-25 — Initiale Optimierung (gemeinsam mit Claude)

### Org-Struktur
- 14 → 5 aktive Agents (-64%)
- CEO + COO + PM + Product Director → `operations` (merged)
- Lead Research Agent + Analyst + Writer → `outreach-agent` (merged)
- Reviewer → `content-review` Skill (kein eigener Agent mehr)
- CDO: auf Bildgenerierung reduziert, Rest als Skill ausgelagert
- Knowledge Manager → deprecated, KB-Pflege in `operations` integriert
- Automation Agent → deprecated, Social Pipeline in `cto` integriert

### Token-Verbrauch
- Boilerplate (Dedup, Heartbeat-Context, Kommunikation) → `shared-rules` Skill
- Follow-up Email-Templates → `followup-sequences` Skill
- Geschätzte Reduktion: ~70% (von ~18.000 auf ~5.500 Token/Zyklus)

### Autonomie
- `auto_proceed: true` für alle Recurring Tasks
- Board-Approval-Loops aus operativen Heartbeats entfernt
- Explizite Autonomie-Regeln + Eskalationsschwellen in `shared-rules`

### Lead-Pipeline
- 3-Heartbeat-Pipeline → 1 Heartbeat (Research + Score + Email in einem Lauf)
- Hunter.io 3-Stufen-Strategie (0 Credits → Verification → Search) erhalten
- Degradation-Pfad bei API-Ausfällen definiert
- Beispiel-Emails nach Trigger-Typ als Referenz in `betaform-voice`

### Social Media
- n8n → direkte Claude API-Calls im CTO-Agent
- 1 Bildtyp → 8 Bildtypen je nach Post-Thema (image-generation Skill)
- CTO dokumentiert Bildtyp im Issue-Body für CDO
- Kanal-Rotation: Mo Personal / Mi Company / Fr Personal

### Plugin: betaform Control
- v2.4.0 → v2.5.0
- `generate-post-image` implementiert (war vorher nur deklariert, nie funktionsfähig)
- `approve-post` Action neu (Ole klickt im Dashboard → Buffer publiziert automatisch)
- Social Media Tab als neuer Einstiegspunkt
- HOT-Lead Highlight + cal-Link direkt in Pipeline-View
- Budget-Warning bei Agents ≥80%
- Event-Listener: HOT-Lead → Webhook, Post approved → Buffer API

### Design System
- `betaform/betaform-design` Skill neu (colors_and_type.css, alle Client-Logos, Icons)
- Wird als Primärquelle für alle visuellen Outputs referenziert

### Wissensdatenbank
- `betaform/knowledge-base` Skill neu — vollständiger KB-Prozess mit API-Calls, Routing-Matrix, Dokumentformat
- Knowledge Manager deprecated, Operations Agent übernimmt wöchentlichen KB-Scan

### Autorisiert von: Ole Beekmann (Board)

---

## Offene Punkte (noch nicht production-ready)

- [ ] `OPENAI_API_KEY` im Plugin konfigurieren
- [ ] `BUFFER_LINKEDIN_PERSONAL_ID` + `BUFFER_LINKEDIN_COMPANY_ID` eintragen
- [ ] `HOT_LEAD_WEBHOOK_URL` setzen (optional)
- [ ] LinkedIn Token bis 10. Juni 2026 erneuern (Ablauf: 22. Juni)
- [ ] BET-226 auf Aktualität prüfen (Primärquelle für alle Tonalitäts-Skills)
- [ ] Verwaiste Routinen bereinigen: `outreach-director-pipeline-koordination-scout-analyst-writer-cascade`, `reviewer-t-gliche-content-queue-pr-fung`, `bet-388-final-report-ceo-handoff`
