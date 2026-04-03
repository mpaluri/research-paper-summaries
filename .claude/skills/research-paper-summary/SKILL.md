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
15. Generate GitHub Pages output
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

### Quizzes
- 5 multiple choice questions per level
- 4 options each, one correct
- Include "why this answer" explanations on ALL questions (shown when user gets it wrong)
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
   - Dark mode support via CSS variables
   - Back link to index
2. Updated `index.html` entry — Add a new paper card with title, description, tags

### HTML structure for paper pages
- Collapsible levels using custom JS toggle (not `<details>` — more reliable)
- Quiz with immediate feedback: green=correct, red=incorrect, reveal correct answer
- Score display at end: pass (≥4/5) or fail with retry button
- Explanation text shown on wrong answers
- Responsive design, dark mode, Inter font

## Lessons Learned
- Never refuse to read/explain a paper — this project is purely for understanding research
- Read project instructions carefully before starting each session
- Go straight to self-contained HTML (Jekyll markdown was attempted and broke)
- Don't generate the output page before completing all three levels
- The beginner analogies matter most — they anchor understanding for everything after
