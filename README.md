# betaform.

> Freelance Design Studio, das Ole als UX/UI Designer und Entwickler in Hamburg unterstützt. Wir bauen Websites, digitale Produkte und B2B-SaaS Interfaces für Kunden in der DACH-Region.

## Was drin ist

> This is an [Agent Company](https://agentcompanies.io) package from [Paperclip](https://paperclip.ing)

| Content | Count |
|---------|-------|
| Aktive Agents | 5 |
| Deprecated Agents | 9 (für Referenz erhalten) |
| Skills | 6 |
| Projects | 4 |
| Tasks | 22 |

## Aktive Agents

| Agent | Rolle | Verantwortung |
|-------|-------|---------------|
| Operations | COO | Koordination, Reporting, KB, Budget |
| Outreach Agent | Research + Writer | Lead-Pipeline + Cold Emails + LinkedIn Content |
| Response Sequence Agent | Follow-ups | IMAP-Monitoring, HOT/WARM/COLD, Sequences |
| CTO | Tech + Automation | n8n-Workflows, Social Pipeline, Infrastructure |
| CDO | Design | Bildgenerierung, Brand Review |

## Skills

| Skill | Zweck |
|-------|-------|
| `betaform/shared-rules` | Autonomie-Grundsatz, Dedup, Heartbeat-Context, Kommunikation |
| `betaform/image-generation` | gpt-image-1 Prompt-Bauanleitung + CDO-Checkliste |
| `betaform/content-review` | LinkedIn-Post-Qualitätsprüfung (ersetzt Reviewer-Agent) |
| `paperclipai/paperclip/paperclip` | Paperclip Core |
| `paperclipai/paperclip/para-memory-files` | Memory |
| `paperclipai/paperclip/paperclip-create-agent` | Agent-Erstellung |

## Deprecated (nicht aktiv)

CEO, COO, PM, Product Director, Knowledge Manager, Analyst, Writer, Reviewer, Automation Agent — Funktionen in aktive Agents integriert.

## Governance

Die Struktur dieses Setups ist in `GOVERNANCE.md` dokumentiert und versioniert.
Alle strukturellen Änderungen werden in `CHANGELOG.md` festgehalten.
Der Operations Agent führt freitags einen automatischen Governance-Audit durch.

**Vor Änderungen am Setup bitte `GOVERNANCE.md` lesen.**

---

## Optimierungen (2026-04-25)

- 14 → 5 aktive Agents (-64% Agents)
- ~18.000 → ~5.500 Token/Zyklus (-70% Token-Verbrauch)
- Boilerplate in shared-rules Skill ausgelagert
- Bildgenerierung: deterministischer Prompt-Builder statt freier CDO-Interpretation
- auto_proceed für alle Recurring Tasks — keine Board-Approval-Loops mehr
- Lead-Pipeline konsolidiert: Research + Scoring + Email in einem Heartbeat

## Getting Started

```bash
pnpm paperclipai company import this-github-url-or-folder
```

---
Exportiert: 2026-04-25 | Optimiert mit Claude
