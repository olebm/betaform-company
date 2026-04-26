---
key: "betaform/shared-rules"
---

# Skill: Shared Agent Rules

Dieses Skill gilt für alle betaform-Agents. Es ersetzt das identische Boilerplate in jedem AGENTS.md.

---

## Autonomie-Grundsatz

Agents entscheiden selbst — Board-Approvals nur wo explizit verlangt.

**Recurring Tasks:** Immer `auto_proceed: true`. Kein Kickoff-Kommentar, keine Bestätigung abwarten.

**Neue, einmalige Issues:** Kickoff-Protokoll anwenden (siehe unten).

**Strukturentscheidungen:** Niemals selbst ausführen. `GOVERNANCE.md` ist die einzige autoritative Quelle für Struktur. Was dort steht, gilt. Was nicht dort steht, braucht Ole-Approval bevor es umgesetzt wird.

---

## Dedup-Regel

Vor jedem neuen Issue:
1. `GET /api/companies/{companyId}/issues?q={suchbegriff}`
2. Ähnliches Issue gefunden → dort kommentieren, kein neues erstellen
3. Nichts gefunden → neues Issue erstellen

---

## Heartbeat-Context

Issue-Updates immer effizient laden:
1. **Zuerst:** `GET /api/issues/{issueId}/heartbeat-context` (kompakt, schnell)
2. **Nur bei Bedarf:** vollständiger Load wenn `fallbackFetchNeeded: true`
3. **Neue Kommentare:** `GET /api/issues/{issueId}/comments?after={last-seen-comment-id}&order=asc`

---

## Kommunikationsstil

- Niemals Task oder Kommentar wiederholen
- Kein Fülltext ("Ich werde jetzt...", "Zusammenfassend...")
- Max. 5 Bullet Points pro Kommentar
- Tool-Reasoning intern halten, nicht im Output

---

## Kickoff-Protokoll (nur neue, einmalige Issues)

Bei unklarem Scope oder fehlendem "Done wenn...":
1. Ersten Kommentar posten: Interpretation + geplante Schritte + angenommene Akzeptanzkriterien
2. Auf Bestätigung von Operations warten
3. Erst dann ausführen

---

## Eskalations-Schwellen

Selbst entscheiden (kein Approval nötig):
- Task-Delegation und Sprint-Priorisierung innerhalb bestehender Strategie
- Kleine Prozessanpassungen
- Issues kommentieren, statusen, assignen

Eskalieren an Operations:
- Blocker die >24h ohne Reaktion sind
- API-Fehler die Pipeline blockieren
- Unklare Specs nach eigenem Interpretationsversuch

Eskalieren an Ole (Board):
- Budget-Überschreitungen >20%
- Neue Clients / Pricing-Änderungen
- Externe Credentials (LinkedIn, Brevo etc.)
- Öffentliche Kommunikation im Namen von betaform
- Alles was in `GOVERNANCE.md` unter "Was immer Ole braucht" steht
