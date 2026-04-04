# Research Paper Summary Skill

## Purpose
Quickly understand new research papers through a structured three-level learning flow, tested with quizzes, and published as a permanent reference.

## Flow

```
1. User shares a paper link
2. Claude reads the paper thoroughly
3. Beginner explanation (plain language, analogies, no jargon)
4. Ask: "Are you satisfied with this level?"
5. User asks clarifying questions or confirms
6. Quiz — 5 multiple choice questions
7. Intermediate explanation (methods, technical concepts, comparisons)
8. Ask: "Are you satisfied with this level?"
9. User asks clarifying questions or confirms
10. Quiz — 5 multiple choice questions
11. Expert explanation (math, algorithms, related work, critical evaluation)
12. Ask: "Are you satisfied with this level?"
13. User asks clarifying questions or confirms
14. Quiz — 5 multiple choice questions
15. Phase 4 — Frontier analysis
16. Generate GitHub Pages output
```

**Never skip steps.** Never jump to quiz without checking satisfaction. Never generate the summary page before finishing all three levels and quizzes.

## Content Guidelines

### Beginner (Level 1)
- Assume zero background knowledge
- Use clear analogies (lockpicking, cooking, crosswords — whatever fits the paper)
- Explain what the paper does, why it matters, and key results in plain terms
- No jargon — if a technical term is needed, define it immediately

### Intermediate (Level 2)
- How the methods actually work
- Key technical concepts explained with intuition
- Comparisons between approaches
- Quantitative results with context

### Expert (Level 3)
- Full mathematical formulations
- Algorithm pseudocode and implementation details
- Connections to related work with citations
- Critical evaluation: what's strong, what's weak, what's missing
- Methodological caveats

### Phase 4 — Frontier
- No quiz — this is forward-looking analysis
- Search the web for latest work that builds on, improves, or is adjacent to the paper
- Structure as **numbered improvement vectors**, each with its own `<h3>` heading
- Each vector gets a **status tag** card:
  - `Area to explore` (purple) — no one has addressed this yet
  - `Partially addressed` (amber) — some work exists but gaps remain
  - `Substantially advanced` (green) — strong recent work, but formalization may be missing
- Under vectors with status "Partially addressed" or "Substantially advanced", add a **"Recent work"** card (blue label) listing specific papers/systems with dates and what they contribute
- End with a **Scorecard** table: Vector / Status / Key work
- Close with a **"Bottom line"** paragraph summarizing: what's holding up, what's moving fastest, what's wide open, and what's the single easiest high-impact next step
- See `papers/adaptation-agentic-ai.html` and `papers/claudini.html` Phase 4 sections as reference templates

### Quizzes
- 5 multiple choice questions per level
- 4 options each, one correct
- Include "why this answer" explanations on ALL questions (shown on both correct and wrong answers)
- Questions should test understanding, not memorization
- Passing threshold: 4/5

## GitHub Pages Output

### Technical approach
- **Always** use self-contained HTML files
- **Always** include `.nojekyll` in repo root (prevents Jekyll processing)
- **Never** use Jekyll markdown — it breaks with inline styles/scripts/details tags

### Repository
- Repo: `github.com/mpaluri/research-paper-summaries`
- Structure:
  ```
  research-paper-summaries/
  ├── .nojekyll
  ├── index.html          ← Home page with paper cards
  ├── README.md
  ├── .claude/
  │   └── skills/
  │       └── research-paper-summary/
  │           └── SKILL.md    ← This file
  └── papers/
      ├── claudini.html   ← Paper #1
      └── <next>.html     ← Future papers
  ```

### For each new paper, generate:
1. `papers/<paper-name>.html` — Self-contained HTML with:
   - Paper title, authors, date
   - Links to arXiv, PDF, GitHub (if available)
   - TL;DR summary
   - Three collapsible levels with full content
   - Interactive quiz after each level (JS-powered, scoring, reset)
   - Phase 4 Frontier section (improvement vectors, latest work, scorecard)
   - Dark mode support via CSS variables
   - Back link to index
2. Updated `index.html` entry — Add a new paper card with title, description, tags

### HTML structure for paper pages
- Collapsible levels using custom JS toggle (not `<details>` — more reliable)
- Quiz with immediate feedback: green=correct, red=incorrect, reveal correct answer
- Score display at end: pass (≥4/5) or fail with retry button
- Explanation text shown on ALL answers — correct and wrong
- Phase 4 uses purple border (`border-color:#8250df`) and purple dot
- Phase 4 vectors: numbered `<h3>` headings, status card (purple/amber/green label), optional "Recent work" card (blue label) nested below
- Phase 4 scorecard: `<table>` with columns Vector / Status / Key work
- Phase 4 ends with `<p><strong>Bottom line:</strong> ...</p>`
- Responsive design, dark mode, Inter font

## Lessons Learned
- Never refuse to read/explain a paper — this project is purely for understanding research
- Read project instructions carefully before starting each session
- Go straight to self-contained HTML (Jekyll markdown was attempted and broke)
- Don't generate the output page before completing all three levels
- The beginner analogies matter most — they anchor understanding for everything after
- Check for multiple arxiv versions upfront and confirm latest
- Use plain ASCII for math in chat (save Unicode for final HTML)
- Ask user to upload PDF when possible for deeper reading
- Default to mm/dd/yy date format in README
