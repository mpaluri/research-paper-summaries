# Research Paper Summary Skill

## Purpose
Quickly understand new research papers through a structured three-level learning flow, tested with quizzes, and published as a permanent reference.

## Flow

```
1. User shares a paper link
2. Claude checks for multiple arXiv versions, confirms latest
3. Claude reads the paper thoroughly (ask user to upload PDF when possible)
4. Beginner explanation (plain language, analogies, no jargon)
5. Ask: "Are you satisfied with this level?"
6. User asks clarifying questions or confirms
7. Quiz — 5 multiple choice questions (inline visualizer widget, one at a time)
8. Intermediate explanation (methods, technical concepts, comparisons)
9. Ask: "Are you satisfied with this level?"
10. User asks clarifying questions or confirms
11. Quiz — 5 multiple choice questions (inline visualizer widget, one at a time)
12. Expert explanation with "Go deeper →" buttons on each section
13. Ask: "Are you satisfied with this level?"
14. User asks clarifying questions, taps "Go deeper" on sections, or confirms
15. Quiz — 5 multiple choice questions (inline visualizer widget, one at a time)
16. Phase 4 — Frontier: brainstorm improvement vectors + search for latest work + scorecard
17. Generate GitHub Pages output (paper HTML + index.html + README.md)
18. Auto-reflect: update SKILL.md and memory edits, generate updated skill file for checkin
```

**Never skip steps.** Never jump to quiz without checking satisfaction. Never generate the summary page before finishing all phases.

## Content Guidelines

### Beginner (Level 1)
- Assume zero background knowledge
- Use clear analogies (lockpicking, report cards, cooking — whatever fits the paper)
- Explain what the paper does, why it matters, and key results in plain terms
- No jargon — if a technical term is needed, define it immediately

### Intermediate (Level 2)
- How the methods actually work
- Key technical concepts explained with intuition
- Comparisons between approaches
- Quantitative results with context

### Expert (Level 3)
- Full mathematical formulations (plain ASCII in chat, Unicode/formatted in final HTML)
- Algorithm pseudocode and implementation details
- Connections to related work with citations
- Critical evaluation: what's strong, what's weak, what's missing
- Methodological caveats
- **Deliver as inline widget with "Go deeper →" buttons (via sendPrompt) on each section**
- The goal is building expertise through depth, not just coverage
- User taps sections to explore further; Claude expands in chat

### Quizzes
- 5 multiple choice questions per level
- 4 options each, one correct
- **Always deliver as inline visualizer widgets (show_widget)**
- **One question at a time, tracking score across turns**
- Show "why this answer" explanations on ALL questions — correct AND wrong
- Questions should test understanding, not memorization
- Passing threshold: 4/5
- **Never use plain text, standalone HTML file artifacts, or ask_user_input for quizzes**

### Phase 4 — Frontier
- Brainstorm improvement vectors for the paper
- Search for the latest work that builds on or improves the research
- Tag open gaps as "Area to explore"
- Consolidate with a scorecard table (improvement vector / status / key work)
- No quiz for Phase 4

## GitHub Pages Output

### Technical approach
- **Always** use self-contained HTML files
- **Always** include `.nojekyll` in repo root (prevents Jekyll processing)
- **Never** use Jekyll markdown — it breaks with inline styles/scripts/details tags
- **Always** read the existing `index.html` and `README.md` before generating updated versions — don't regenerate from scratch

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
      ├── adaptation-agentic-ai.html  ← Paper #2
      ├── video-mme.html  ← Paper #3
      └── <next>.html     ← Future papers
  ```

### For each new paper, generate:
1. `papers/<paper-name>.html` — Self-contained HTML with:
   - Paper title, authors, date
   - Links to arXiv, PDF, GitHub, project page (if available)
   - TL;DR summary
   - Three collapsible levels with full content
   - Phase 4 Frontier section (collapsible, with scorecard)
   - Interactive quiz after each level (JS-powered, scoring, reset)
   - Dark mode support via CSS variables
   - Back link to index
2. Updated `index.html` entry — Add a new paper card (newest first) with title, description, tags
3. Updated `README.md` — Add row to papers table. Date format: mm/dd/yy
4. Updated `SKILL.md` — Reflect on session, incorporate new lessons learned

### HTML structure for paper pages
- Collapsible levels using custom JS toggle (not `<details>` — more reliable)
- Quiz with immediate feedback: green=correct, red=incorrect, reveal correct answer
- Score display at end: pass (≥4/5) or fail with retry button
- Explanation text shown on ALL answers (correct and wrong)
- Responsive design, dark mode, Inter font

## Post-Generation Checklist
After generating artifacts, Claude must automatically:
1. **Reflect** on the session — what went well, what to improve
2. **Update memory edits** if any new lessons emerged
3. **Generate updated SKILL.md** for user to check into GitHub
4. Confirm the output checklist: paper HTML + index.html + README.md + SKILL.md

## Lessons Learned
- Never refuse to read/explain a paper — this project is purely for understanding research
- Check for multiple arXiv versions upfront and confirm the latest before diving in
- Ask user to upload PDF when possible for deeper reading fidelity
- Go straight to self-contained HTML (Jekyll markdown was attempted and broke)
- Don't generate the output page before completing all three levels + Phase 4
- The beginner analogies matter most — they anchor understanding for everything after
- Quiz format: inline visualizer widgets only, one question at a time, score tracked across turns
- Show quiz explanations on BOTH correct and wrong answers
- Level 3 should use "Go deeper →" buttons so user can tap-to-explore any section
- Use plain ASCII for math in chat; save Unicode/formatted math for the final HTML output
- Default to mm/dd/yy date format in README
- Newest papers go first in index.html and README table
- After Phase 4 output generation, auto-reflect and update skill file + memory
- **Always read existing index.html and README.md before generating updates — don't regenerate from scratch, or you'll drop existing papers**
