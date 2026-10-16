# Finance Hub – Session Context

> Read this at the start of any new session to continue work on the finance hub without needing a recap.

## What this project is

LIBF CeFS (Certificate in Financial Studies) Unit 1 revision hub for Pratik's child studying A-Level Finance. Static site hosted on Netlify, auto-deployed from GitHub on `git push origin main`.

- **Live site:** https://alevel-finance-hub.netlify.app/
- **GitHub repo:** https://github.com/pratikpatel74/finance-hub
- **Local path (Mac):** `~/Documents/Projects/finance-hub/`
- **No build step** — Netlify serves the repo root directly

---

## File structure

```
~/Documents/Projects/finance-hub/
├── index.html               ← Hub homepage (9 topic cards, score badges)
├── quizzes/
│   ├── topic1.html          ← LO1: Purposes of Money
│   ├── topic2.html          ← LO2: The Personal Life Cycle
│   ├── topic5.html          ← LO3 (savings): Savings Products
│   ├── topic6.html          ← LO3 (borrowing): Credit & Debt
│   ├── topic7.html          ← LO4: Providers of Financial Services
│   ├── topic8.html          ← LO8: Consumer Protection
│   ├── topic9.html          ← LO5: Bank Accounts & Cards      [NEW]
│   ├── topic10.html         ← LO6: Short-Term Financial Management [NEW]
│   └── topic11.html         ← LO7: Earnings, Tax & NI         [NEW]
└── docs/
    ├── Topic1_Summary.docx  … Topic8_Summary.docx   ← existing
    ├── Topic9_Summary.docx  ← LO5 draft summary     [NEW]
    ├── Topic10_Summary.docx ← LO6 draft summary     [NEW]
    └── Topic11_Summary.docx ← LO7 draft summary     [NEW]
```

Topics 3 and 4 intentionally absent — college hasn't covered them yet.

---

## Quiz file spec (all 9 files follow this pattern)

| Feature | Detail |
|---|---|
| Question pool | 22 questions per topic |
| Draw per session | 10 (Fisher-Yates shuffle) |
| Timer | 60s countdown; auto-advances on timeout |
| Missed tracker | localStorage `topicN_missed` (array of stable `_id` indices) |
| Retry mode | `?retry=missed` URL param |
| Score persistence | localStorage `topicN_last` → `{score, total, pct, date}` |
| Keyboard nav | 1–4 to answer; Enter/Space to advance |
| Theme | Shared `localStorage('theme')` key across hub + all quizzes |
| Theme restore | Inline `<script>` immediately after `<html>` tag (before `<head>`) |

Theme restore snippet (must be on every page):
```html
<html lang="en" data-theme="dark"><script>try{var _t=localStorage.getItem("theme");if(_t)document.documentElement.setAttribute("data-theme",_t);}catch(e){}</script>
```

### Topic accent colours

| File | TOPIC_ID | Dark accent | Light accent |
|---|---|---|---|
| topic1.html | topic1 | `#818cf8` (indigo) | `#6366f1` |
| topic2.html | topic2 | `#38bdf8` (sky) | `#0ea5e9` |
| topic5.html | topic5 | `#a78bfa` (violet) | `#7c3aed` |
| topic6.html | topic6 | `#34d399` (emerald) | `#059669` |
| topic7.html | topic7 | `#fbbf24` (amber) | `#d97706` |
| topic8.html | topic8 | `#f87171` (red) | `#dc2626` |
| topic9.html | topic9 | `#10b981` (emerald) | `#059669` |
| topic10.html | topic10 | `#f59e0b` (amber) | `#d97706` |
| topic11.html | topic11 | `#c084fc` (purple) | `#7c3aed` |

---

## Hub (index.html) stats

| Stat | Value |
|---|---|
| Topics | 9 |
| Questions | 198 (22 × 9) |
| Summaries | 9 |
| Score badge IDs | `score-t1`, `score-t2`, `score-t5`, `score-t6`, `score-t7`, `score-t8`, `score-t9`, `score-t10`, `score-t11` |
| loadScores() array | `['1','2','5','6','7','8','9','10','11']` |

---

## Key facts / exam figures used in quizzes (2024/25)

- **NLW:** £11.44/hr (21+)
- **NMW:** £8.60 (18–20), £6.40 (under 18 / apprentice*)
  - *Apprentice rate applies if under 19 OR 19+ in first year
- **Personal allowance:** £12,570
- **Basic rate income tax:** 20% (£12,571–£50,270)
- **Higher rate:** 40% (£50,271–£125,140)
- **Employee NI:** 8% (Primary Threshold £242/wk to UEL £967/wk)
- **FSCS deposit protection:** £85,000 per person per authorised firm
- **Contactless limit:** £100 per transaction
- **Section 75 CCA 1974:** joint liability for purchases £100–£30,000
- **Emergency fund:** 3–6 months' essential expenditure
- **Minimum credit card payment:** £25 or 1–2% of balance (whichever greater)
- **Tax year:** 6 April – 5 April
- **P60 issued by:** 31 May (by employer, annual)
- **Self Assessment online deadline:** 31 January following tax year end

---

## Known issues / pending work

- **LO5/6/7 summary .docx files are drafts** — based on LIBF spec only. Update once college provides source material.
- **Topic 6 Summary.docx** — user needs to manually fix two things:
  1. "Consumer Rights Act 2015" → **Consumer Credit Act 1974** (Section 75)
  2. Minimum payment percentage: **3–5% → 1–2%**
- **Topics 3 & 4** — not yet covered by college; quizzes/summaries not built yet
- **LO8 topic numbering** — topic8.html covers Consumer Protection (LO8); the hub uses the college's topic numbering, not sequential LO numbers

---

## Deploy workflow

```bash
cd ~/Documents/Projects/finance-hub
git add <files>
git commit -m "message"
git push origin main   # triggers Netlify auto-deploy (~8 seconds)
```

**Important:** `git push` must be run in Terminal on the Mac — the device shell used by Claude can't authenticate with GitHub. After pushing, verify at https://alevel-finance-hub.netlify.app/

---

## Scratchpad location (cloud session)

Quiz HTML source files are kept in the cloud scratchpad at:
`/tmp/claude-0/-home-claude/c1222770-66d1-51bc-995e-74b90a09d805/scratchpad/quizzes/`

This path changes each session — always stage from Mac and edit there, or re-check the scratchpad path with `ls /tmp/claude-0/`.
