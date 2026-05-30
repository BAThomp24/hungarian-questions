# Magyar Interjú — Hungarian interview practice

A single-page app that drills the Hungarian citizenship-interview Q&A from `Big List.html`.
Press **Play**, hear a random question spoken in Hungarian, answer out loud, then reveal the
English, your Hungarian answer (also spoken), or the English answer.

## Run it

Just **double-click `index.html`** — it works straight from disk, no server or install.

> Use **Microsoft Edge** for the best result: it ships high-quality Hungarian neural voices
> (Tamás, Noémi) that load automatically when you're online. Chrome only has Hungarian audio
> if you've installed a Windows Hungarian language pack
> (Settings → Time & language → Language → add Hungarian).

## Features

- **Play / Next** — random question, no-repeat shuffle (covers every card before repeating).
- **Topic filter** — drill a single area (ancestry, family, work, documents, …).
- **Question range** — study a slice by number, e.g. `#30`–`#50` (the number shown on each
  card is its position in the table). Combines with the topic filter; **All** resets it.
- **Reveal buttons** — English question, your Hungarian answer (spoken), English answer.
- **Interview mode** — hides the question text so you only hear it; answer aloud, then reveal.
- **Speech speed** slider and a **voice** picker.
- Keyboard: **Space/Enter** = next, **R** = replay the question.

## Privacy / how the data is handled

The published site shows **placeholders** (`[CITY]`, `[FATHER]`, `[DATE]`, …) instead of
personal details, so nothing private is on the public web. General-knowledge answers about
Hungary (the anthem, Petőfi, neighbouring countries, etc.) are kept intact.

The real, unredacted answers live only on the local machine and are **never committed**:
`Big List.html`, `data.real.json`, `extract.js`, and `redactions.js` are all git-ignored.

## Updating the questions (local only)

Edit / re-export `Big List.html`, then regenerate:

```
node extract.js
```

This writes `data.real.json` (private, full answers) and the redacted `data.json` + `data.js`
(what the site uses). It prints a warning if any personal token slips through the redaction.
Then commit and push `data.js` / `data.json` to update the live site.

## Files

| File | Purpose |
|------|---------|
| `index.html`, `style.css`, `app.js` | the app |
| `extract.js` | one-time parser: `Big List.html` → `data.json` + `data.js` |
| `data.js` / `data.json` | generated question data |
| `Big List.html` | original Google Sheets export (source of truth) |

## Later: studio-quality audio (optional)

The browser voice is good, but if you want consistent, fully-offline pro audio, we can add a
script that pre-renders every question/answer to MP3 with a cloud TTS (Azure/Google/ElevenLabs)
and have the app prefer those clips. The data shape already leaves room for it.
