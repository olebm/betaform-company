---
key: "betaform/followup-sequences"
---

# Skill: Follow-up Sequences

Feste Email-Templates für automatische Follow-ups. Nicht verändern ohne Board-Freigabe.

---

## Sequence 1 — Tag 3 (Mo–Fr, 10:00–12:00 UTC)

**Subject:** `Re: [Original Subject] — Quick question`

**Body:**
```
Hi [FirstName],

kurzer Nachhackhaken zum ursprünglichen Schreiben — manchmal landen Mails im Spam! 😊

Falls dein Team gerade brennt: Wir helfen bei Overflow-Projekten (Design, Frontend, Full-Stack).
Keine Vendor-Overhead, keine Micromanagement — einfach verlässlich.

Noch 15 Minuten für einen kurzen Call diese Woche?

–––
Ole Beekmann
Website: https://betaform.io
Blog: https://betaform.io/blog
ole@betaform.io
+49 177 231 104 1
```

FROM: `"Ole von betaform." <hello@betaform.io>` | REPLY-TO: `ole@betaform.io`
Nach Versand → Brevo Status: `follow_up_1_sent`
Paperclip Task: `"Follow-up Sequence 1 sent to [Company]"`

---

## Sequence 2 — Tag 7 (Mo–Fr, 14:00–16:00 UTC)

**Subject:** `One more thing — [Company Name]`

**Body:**
```
Hi [FirstName],

letzte Nachricht, versprochen! 😊

Wir haben gerade ein ähnliches Studio in deiner Region (auch ~2-Personen-Team) unterstützt —
schneller Kontakt wurde zu regelmäßigen Overflow-Projekten.

Falls interessant: Ich hab noch 2-3 Slots diese Woche frei.
Termin direkt buchen: https://cal.betaform.io/ole/erstgespraech

Sonst: alles Gute! 👋

–––
Ole Beekmann
Website: https://betaform.io
Blog: https://betaform.io/blog
ole@betaform.io
+49 177 231 104 1
```

FROM: `"Ole von betaform." <hello@betaform.io>` | REPLY-TO: `ole@betaform.io`
Nach Versand → Brevo Status: `follow_up_2_sent`
Paperclip Task: `"Follow-up Sequence 2 sent to [Company]"`

---

## STOP nach Sequence 2

Brevo Status → `follow_up_complete`. Kein weiterer Outreach.

---

## Blackout-Perioden

Keine Sequences versenden:
- **20.12–05.01** (Weihnachten/Neujahr)
- **01.08–31.08** (Sommerurlaub DACH)

Fällt ein Versand in Blackout → verschieben auf ersten Werktag danach.
