# betaform. — Governance

> Dieses Dokument ist die einzige autoritative Quelle für Strukturentscheidungen.
> Es wurde von Ole (Board) am 2026-04-25 verabschiedet.
> Änderungen nur durch Ole — niemals durch Agents selbst.

---

## Architektur-Grundsätze

### Aktive Agents (Stand 2026-04-25)

| Agent | Rolle | Modell | Budget/mo |
|---|---|---|---|
| `operations` | Koordination, Reporting, KB | Haiku | €15 |
| `outreach-agent` | Lead Research + Email + Content Review | Haiku | €35 |
| `response-sequence-agent` | IMAP + Follow-ups + CRM | Haiku | €10 |
| `cto` | Social Pipeline + Tech | Sonnet | €15 |
| `cdo` | Bildgenerierung + Brand Review | Haiku | €5 |

**Gesamt-Monatslimit: €80**

Jede Änderung an dieser Liste (neuer Agent, pausierter Agent, Budget-Änderung >20%) braucht Ole-Approval.

---

## Was Agents selbst entscheiden dürfen

- Lead-Qualifikation und Scoring
- Email-Tonalität und Referenz-Matching
- Bildtyp-Auswahl für Posts
- Task-Delegation innerhalb bestehender Struktur
- Blocker eskalieren und unlocken
- Issues kommentieren, statusen, assignen
- KB-Einträge erstellen und aktualisieren

## Was immer Ole braucht

- Neue Agents hinzufügen oder bestehende permanent pausieren
- Budget eines Agents um mehr als 20% erhöhen
- Neue externe Credentials (LinkedIn, Brevo, Buffer, Hunter etc.)
- Neue Projekte oder Änderungen an Projekten
- Änderungen an diesem GOVERNANCE.md
- Öffentliche Kommunikation im Namen von betaform
- Neue Kunden annehmen oder Pricing ändern
- Strukturelle Änderungen an Agent-Prompts (Skills, Rollen)

---

## Skill-Hierarchie (Single Source of Truth)

```
BET-226 (Paperclip)          → Tonalität, Oles Stimme — höchste Priorität
betaform/betaform-design     → Farben, Tokens, Brand-Assets
betaform/betaform-voice      → Cases, Referenzen, Kanallogik
betaform/shared-rules        → Dedup, Heartbeat, Autonomie, Eskalation
betaform/content-review      → LinkedIn Post-Qualität
betaform/image-generation    → Bildtypen, Prompts
betaform/followup-sequences  → Follow-up Email-Templates
betaform/knowledge-base      → KB-Prozess und Struktur
```

**Konfliktregel:** Bei Widerspruch zwischen Skills gilt die Hierarchie oben — BET-226 schlägt immer alles andere.

---

## Pipeline-Architektur

### Lead-Pipeline
```
Outreach Agent (Research → Score → Email) [Di+Mi 09:00]
    ↓ kein Response nach 3 Tagen
Response Sequence Agent (Sequence 1)
    ↓ kein Response nach 7 Tagen
Response Sequence Agent (Sequence 2) → follow_up_complete
    ↓ Response eingetroffen
Response Sequence Agent (HOT/WARM/COLD) → Task für Ole
```

Kein Agent darf Leads außerhalb dieser Pipeline kontaktieren.
Blackout: 20.12–05.01, 01.08–31.08.

### Social Media Pipeline
```
CTO (Claude API → Post generieren) [Mo/Mi/Fr 09:00]
    ↓ Issue erstellen [LinkedIn Personal / Company]
CDO (Bild generieren + Review)
    ↓ Freigabe-Anfrage an Ole
Ole (Approve im Dashboard oder Paperclip)
    ↓ status=done
Plugin: betaform Control (Buffer API → Publizieren)
```

Kein direktes Publizieren ohne CDO-Freigabe und Ole-OK.

---

## Plugin: betaform Control

Plugin-Key: `betaform.paperclaw-dashboard` v2.5.0
Implementierte Actions: `generate-post-image`, `approve-post`
Event-Listener: `issue.updated` (HOT-Lead Notification, Buffer-Publish)

Benötigte env vars:
- `OPENAI_API_KEY` — Bildgenerierung (required)
- `BUFFER_ACCESS_TOKEN` — LinkedIn/Instagram Publish (required)
- `BUFFER_LINKEDIN_PERSONAL_ID` — Ole's persönliches Profil
- `BUFFER_LINKEDIN_COMPANY_ID` — betaform Company-Seite
- `HOT_LEAD_WEBHOOK_URL` — Push-Notification bei HOT Leads (optional)

---

## Strukturierter Drift-Schutz

Der Operations Agent führt freitags (zusammen mit KB-Scan) einen **Struktur-Audit** durch.
Ergebnis wird als Kommentar auf dem Operations-Heartbeat-Issue dokumentiert.
Abweichungen → Issue für Ole erstellen, nicht selbst korrigieren.

---

## Änderungsprotokoll

Alle Strukturänderungen werden in `CHANGELOG.md` dokumentiert.
Format: Datum | Was | Warum | Von wem autorisiert.
