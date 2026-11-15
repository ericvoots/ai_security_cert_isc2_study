# AI Security Practice Question Bank

Practice questions for the ISC2 AI Security pilot exam, organized by the six published exam domains and their objectives.

> Unofficial. Written from ISC2's published pilot exam outline. Not affiliated with or endorsed by ISC2, and not actual exam questions.

## Status

All six domains are complete: 300 questions (222 multiple choice, 78 true/false), each with an explanation and references. Version 0.2.0.

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

## Running it

**GitHub Pages:** in the repo, go to Settings → Pages, set Source to "Deploy from a branch", pick `main` and `/ (root)`, and save. The quiz will be at `https://<username>.github.io/<repo>/`.

**Locally:** browsers block a page opened from disk from reading `questions.json`, so either serve the folder:

```
python3 -m http.server
```

and open http://localhost:8000, or open `index.html` directly and choose `questions.json` with the file picker it shows.

## Quiz features

- Quiz builder: tick any mix of domains and set how many questions to draw from each, or spread a total evenly across them
- Narrow each domain to specific objectives, and filter by question type (multiple choice or true/false)
- "Copy link to this quiz" saves the setup in the URL (for example `#d=1:20,2:10`), so you can bookmark or share a quiz; the page also remembers your last setup
- Results show your score by domain and by objective, with buttons to retry missed questions or take a fresh draw with the same setup
- **Mock exam mode** under exam conditions: a countdown timer, one question at a time, no skipping, no going back, and no feedback until the end. Questions are drawn evenly across domains. The time limit defaults to the real pilot exam's pace (160 questions in 3 hours, about 68 seconds each) and can be changed. Progress is saved in the browser, so a refresh doesn't lose the exam, but the clock keeps running. Results show score, time used, breakdowns by domain and objective, and a full review with explanations and references.
- Shuffled question order and answer choices (both optional)
- Instant feedback with an explanation and linked references after each answer
- Score by objective at the end, with a review of missed questions
- Missed questions are remembered in your browser, so you can drill only those
- Keyboard: A–D or 1–4 (T/F for true/false) to answer, Enter for the next question

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
- `answer` must exactly match one of the `options`.
- `references` is a list of one or more sources. `url` is `null` for a print-only book. `section` says where to look. `page` is a string (it can be a range like `"61-66"`) or `null` for web pages. Page numbers are the printed page numbers in the source document, not the PDF viewer's page count.
- `number` restarts at 1 in each domain. A question's stable ID is `<domain>-<number>`, which the page uses to remember missed questions, so avoid renumbering existing questions.

To add a domain, fill in its `questions` array. The page picks it up automatically.
