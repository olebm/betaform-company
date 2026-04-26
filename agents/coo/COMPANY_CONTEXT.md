# betaform.io — Kontextwissen

**Zuletzt aktualisiert:** 2026-04-25 (Agent-Konsolidierung abgeschlossen)

## Aktive Pipelines

- **Lead-Gen Pipeline:** Outreach Agent (Research → Scoring → Email) | Di+Mi 09:00 CEST
- **Social Media Pipeline:** CTO (Claude API direkt) → CDO (Bild + Review) → Ole (Freigabe) → CTO (Buffer API) | Mo/Mi/Fr 09:00
- **Response Pipeline:** Response Sequence Agent | täglich 11:00 UTC

## Aktive Agents (5)

| Agent | Modell | Budget/mo |
|---|---|---|
| Operations | Haiku | €15 |
| Outreach Agent | Haiku | €35 |
| Response Sequence Agent | Haiku | €10 |
| CTO | Sonnet | €15 |
| CDO | Haiku | €5 |

## Strategische Entscheidungen

- **Agent-Konsolidierung (2026-04-25):** 14 → 5 aktive Agents. CEO/COO/PM/Analyst/Writer/Reviewer/CDO-eigenständig deprecated.
- **Autonomie-Grundsatz:** Recurring Tasks laufen mit `auto_proceed: true`, kein Board-Approval für operative Entscheidungen
- **Shared Skills:** `betaform/shared-rules`, `betaform/image-generation`, `betaform/content-review`, `betaform/followup-sequences`
- **Bildgenerierung:** deterministischer Prompt-Builder in Skill — kein freier CDO-Interpret mehr

## ICP (Ideal Customer Profile)

DACH | 10–50 MA | Seed/Series A | SaaS, Marketplaces, B2B Fintech, Deep-Tech, Healthcare, Gov | Budget 5k–30k€
Vollständig: BET-484#document-icp

## Plugin: betaform Control (`@betaform/paperclaw-dashboard` v2.5.0)

Aktive Capabilities:
- `generate-post-image` → CDO ruft auf → gpt-image-1 via OpenAI API → Bild als Issue-Dokument
- `approve-post` → Ole klickt im Dashboard → Issue-Status `done` → Buffer-Publish automatisch via Plugin-Event
- HOT-Lead-Notification → `issue.updated` Event → Webhook an `HOT_LEAD_WEBHOOK_URL` (Telegram/WhatsApp)

Benötigte env vars im Plugin: `OPENAI_API_KEY`, `BUFFER_ACCESS_TOKEN`, `BUFFER_LINKEDIN_PERSONAL_ID`, `BUFFER_LINKEDIN_COMPANY_ID`, `HOT_LEAD_WEBHOOK_URL` (optional)

## Bekannte Einschränkungen

- LinkedIn Access Token läuft 22. Juni 2026 ab → Reminder: 10. Juni (Task: linkedin-token-renewal-reminder)
- Hunter.io Free Plan: 50 Searches/Monat (Reset am 20.), max. 11/Woche

## Nächste Termine

- **22.06.2026:** LinkedIn Token Renewal
- **01.05.2026:** Mai-Budget-Reset
