# AI Security Practice Question Bank

Practice questions for the ISC2 AI Security pilot exam, organized by the six published exam domains and their objectives.

> Unofficial. Written from ISC2's published pilot exam outline. Not affiliated with or endorsed by ISC2, and not actual exam questions.

## Status

All six domains are complete: 300 questions (222 multiple choice, 78 true/false), each with an explanation, references and a difficulty rating (99 easy, 158 medium, 43 hard). Version 0.3.0.

| Domain | Name | Questions |
|---|---|---|
| 1 | Artificial Intelligence (AI) Concepts and Security Fundamentals | 50 |
| 2 | AI Governance, Ethics, Risk, and Compliance | 50 |
| 3 | AI Data Management, Privacy, and Model Security | 50 |
| 4 | Secure AI Architecture, Engineering, and IAM | 50 |
| 5 | Secure AI Operations and Incident Response | 50 |
| 6 | AI Threats, Testing, and Lifecycle Management | 50 |

Regulations move: EU AI Act questions reflect the text as amended by the Digital Omnibus on AI (Regulation (EU) 2026/1744, in force 27 July 2026), which moved the stand-alone high-risk deadline to 2 December 2027 and softened the Article 4 AI literacy duty.

## Sources

References point mainly to free sources: NIST (AI 100-1, AI 600-1, AI 100-2e2025, SP 800-61r3, SP 800-218A, SP 1270, SP 800-188, SP 800-207, SP 800-226), the EU AI Act and GDPR on EUR-Lex, OWASP (Top 10 for LLM Applications 2025, Agentic AI Threats and Mitigations, GenAI Red Teaming Guide, Non-Human Identities Top 10, CycloneDX), MITRE ATLAS, CISA/NCSC/NSA joint guidance, the MCP authorization spec and key research papers. ISO/IEC 42001 is paid, so its references give the clause number and the ISO catalogue page.

## Files

- `questions.json`: the question bank
- `index.html`: the quiz page, which loads `questions.json`
- `results.template.json`: an empty progress file (see [Tracking your progress](#tracking-your-progress))
- `.gitignore`: keeps your personal `results.json` out of the repo

## Running it

**GitHub Pages:** in the repo, go to Settings → Pages, set Source to "Deploy from a branch", pick `main` and `/ (root)`, and save. The quiz will be at `https://<username>.github.io/<repo>/`.

**Locally:** browsers block a page opened from disk from reading `questions.json`, so either serve the folder:

```
python3 -m http.server
```

and open http://localhost:8000, or open `index.html` directly and choose `questions.json` with the file picker it shows.

## Quiz features

- Quiz builder: tick any mix of domains and set how many questions to draw from each, or spread a total evenly across them
- Narrow each domain to specific objectives, and filter by question type (multiple choice or true/false) and difficulty (easy, medium, hard)
- "Copy link to this quiz" saves the setup in the URL (for example `#d=1:20,2:10`), so you can bookmark or share a quiz; the page also remembers your last setup
- Results show your score by domain, difficulty and objective, with buttons to retry missed questions or take a fresh draw with the same setup
- **Mock exam mode** under exam conditions: a countdown timer, one question at a time, no skipping, no going back, and no feedback until the end. Questions are drawn evenly across domains. The time limit defaults to the real pilot exam's pace (160 questions in 3 hours, about 68 seconds each) and can be changed. Progress is saved in the browser, so a refresh doesn't lose the exam, but the clock keeps running. Results show score, time used, breakdowns by domain and objective, and a full review with explanations and references.
- Shuffled question order and answer choices (both optional)
- Instant feedback with an explanation and linked references after each answer
- Score by objective at the end, with a review of missed questions
- Missed questions are remembered in your browser, so you can drill only those
- Keyboard: A–D or 1–4 (T/F for true/false) to answer, Enter for the next question
- **Progress tab:** totals across every quiz and exam you've finished, accuracy by domain and difficulty, your weakest objectives (with a button to build a quiz on them) and a list of recent attempts

## Difficulty levels

Each question has a `difficulty` of `easy`, `medium` or `hard`. These are judgment calls:

- **Easy:** recall of one definition or fact; the wrong options are clearly different concepts.
- **Medium:** apply a concept to a scenario, or tell apart two or three related ideas.
- **Hard:** fine distinctions between close options, specific clause or article details, or several plausible answers where only one is the *best*.

Wrong options are written to be believable, and the correct answer is not given away by length: it is the longest option about a quarter of the time, as you'd expect by chance.

## Tracking your progress

The page can't write files to your computer on its own, so progress works in two layers:

1. **Automatic, in your browser.** Every finished practice quiz or mock exam is saved in the browser's local storage as one summary record. Nothing is sent anywhere. Clearing site data or switching browsers or computers loses it, which is what the file is for.
2. **Your `results.json` file.** On the **Progress** tab (or the link under any results screen), choose **Download results.json** to save everything to a file. Choose **Load results.json** to bring it back on another browser or computer. Loading *merges*: attempts already in the browser are kept, and duplicates (same `id`) are skipped, so you can load the same file twice safely.

Suggested routine: keep one file (for example `Documents/aisec/results.json`), download a fresh copy after each study session and overwrite the old one, and load it when you start on a new device. `results.template.json` is the empty starting point if you want to see the shape of the file. Don't commit your `results.json` to a public repo; the included `.gitignore` already ignores that name.

### results.json format

```json
{
  "format": "aisec-qbank-results",
  "version": 1,
  "exported": "2026-11-15T17:42:10.512Z",
  "bank_version": "0.3.0",
  "attempts": [
    {
      "id": "2026-11-15T17:20:03.118Z-k3x9",
      "date": "2026-11-15T17:41:55.904Z",
      "mode": "practice",
      "bank_version": "0.3.0",
      "questions": 25,
      "answered": 25,
      "correct": 19,
      "score_pct": 76,
      "duration_sec": 1312,
      "time_limit_sec": null,
      "timed_out": false,
      "setup": "d=2%3A10%2C3%3A15&lv=medium%2Bhard",
      "by_domain":     { "2": { "correct": 8, "total": 10 }, "3": { "correct": 11, "total": 15 } },
      "by_objective":  { "2.1": { "correct": 2, "total": 2 }, "3.4": { "correct": 1, "total": 3 } },
      "by_difficulty": { "medium": { "correct": 13, "total": 16 }, "hard": { "correct": 6, "total": 9 } },
      "by_type":       { "multiple_choice": { "correct": 14, "total": 19 }, "true_false": { "correct": 5, "total": 6 } }
    }
  ],
  "missed": ["1-12", "3-40", "6-25"]
}
```

- One record per finished quiz or exam. Records hold aggregates only (counts by domain, objective, difficulty and type), not your individual answers.
- `mode` is `practice` or `exam`. `score_pct` is `correct` out of the questions answered for practice (you can end a quiz early), and out of all questions for a mock exam, where unanswered questions count as wrong.
- `by_objective` in the example is shortened; real records list every objective that came up.
- `time_limit_sec` and `timed_out` apply to mock exams. `setup` is the quiz configuration in the same form as a "Copy link" URL (for exams, `n=<questions>&m=<minutes>`).
- `missed` is the list of question IDs (`<domain>-<number>`) you most recently got wrong, which powers "Only questions I've missed". Loading a file adds these to the browser's list.
- `bank_version` records which version of `questions.json` you were tested on, since questions can be edited between versions.

## JSON format

```json
{
  "title": "...",
  "domains": [
    {
      "domain": 1,
      "name": "Artificial Intelligence (AI) Concepts and Security Fundamentals",
      "objectives": { "1.1": "AI concepts and security fundamentals" },
      "questions": [
        {
          "number": 1,
          "objective": "1.1",
          "type": "multiple_choice",
          "difficulty": "medium",
          "question": "...",
          "options": ["...", "...", "...", "..."],
          "answer": "exact text of the correct option",
          "explanation": "...",
          "references": [
            {
              "title": "NIST AI 100-2e2025, Adversarial Machine Learning: A Taxonomy and Terminology of Attacks and Mitigations",
              "url": "https://doi.org/10.6028/NIST.AI.100-2e2025",
              "section": "2.2 Evasion Attacks and Mitigations",
              "page": "11"
            }
          ]
        }
      ]
    }
  ]
}
```

- `type` is `multiple_choice` (four options) or `true_false` (options are always `["True", "False"]`).
- `difficulty` is `easy`, `medium` or `hard`. Questions without it are treated as `medium`.
- `answer` must exactly match one of the `options`.
- `references` is a list of one or more sources. `url` is `null` for a print-only book. `section` says where to look. `page` is a string (it can be a range like `"61-66"`) or `null` for web pages. Page numbers are the printed page numbers in the source document, not the PDF viewer's page count.
- `number` restarts at 1 in each domain. A question's stable ID is `<domain>-<number>`, which the page uses to remember missed questions, so avoid renumbering existing questions.

To add a domain, fill in its `questions` array. The page picks it up automatically.
