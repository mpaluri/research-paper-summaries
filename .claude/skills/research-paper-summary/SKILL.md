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
7. Quiz — 5 multiple choice questions (inline visualizer widget or plain text)
8. Intermediate explanation (methods, technical concepts, comparisons)
9. Ask: "Are you satisfied with this level?"
10. User asks clarifying questions or confirms
11. Quiz — 5 multiple choice questions (inline visualizer widget or plain text)
12. Expert explanation with "Go deeper →" buttons on each section
13. Ask: "Are you satisfied with this level?"
14. User asks clarifying questions, taps "Go deeper" on sections, or confirms
15. Quiz — 5 multiple choice questions (inline visualizer widget or plain text)
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
- Show "why this answer" explanations on ALL questions — correct AND wrong
- Questions should test understanding, not memorization
- Passing threshold: 4/5
- **Distribute correct answers evenly across A/B/C/D positions — no clustering**
- **Keep all option lengths similar — don't make the correct answer noticeably longer or shorter**

**Quiz delivery — two modes (user preference):**
1. **Inline visualizer widgets** — one question at a time, score tracked across turns
2. **Plain text in chat** — all 5 questions listed, user answers by letter, Claude gives feedback

**If using widgets, use the minimal pattern:**
- Named button IDs (a/b/c/d), addEventListener loop in script block
- No inline onclick attributes
- No sendPrompt in quiz widgets — user types next prompt manually
- Script at the very end, after all HTML, outside the content div
- Add `var done=false;` guard to prevent double-clicks
- This pattern prevents the widget from hanging after rendering

**If widgets cause rendering issues, fall back to plain text immediately.** Don't fight the tooling.

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
  ├── index.html
  ├── README.md
  ├── .claude/skills/research-paper-summary/SKILL.md
  └── papers/
      ├── claudini.html           ← Paper #1
      ├── adaptation-agentic-ai.html  ← Paper #2
      ├── video-mme.html          ← Paper #3
      ├── mmmu.html               ← Paper #4
      ├── mmmu-pro.html           ← Paper #5
      └── <next>.html
  ```

### For each new paper, generate:
1. `papers/<paper-name>.html` — Self-contained HTML with all 4 phases, quizzes, dark mode
2. Updated `index.html` — New paper card (newest first)
3. Updated `README.md` — New row (mm/dd/yy dates, newest first)
4. Updated `SKILL.md` — Session reflections

### Git workflow note
When pushing, if divergent branches cause conflicts on index.html or README.md:
```
git fetch origin
git reset --hard origin/main
# copy generated files over
git add . && git commit -m "Add <paper>" && git push
```

## Lessons Learned
- Never refuse to read/explain a paper — purely educational project
- Check for multiple arXiv versions upfront and confirm the latest
- Ask user to upload PDF when possible for deeper reading
- Self-contained HTML only (Jekyll broke)
- Don't generate output before completing all three levels + Phase 4
- Beginner analogies matter most — they anchor everything after
- Show quiz explanations on BOTH correct and wrong answers
- Level 3 should use "Go deeper →" buttons for tap-to-explore
- Plain ASCII for math in chat; Unicode/formatted in final HTML
- mm/dd/yy date format in README; newest papers first everywhere
- After output generation, auto-reflect and update skill + memory
- **Always read existing index.html and README.md before updating — don't drop existing papers**
- **Quiz widget pattern:** named IDs, addEventListener, no onclick, script after HTML, done-guard. If widgets hang, fall back to plain text immediately.
- **Plain text quizzes work well** — especially for complex L3 questions. Let user choose.
- **Quiz answer distribution:** Spread correct answers evenly across A/B/C/D. Keep option lengths similar. Don't cluster correct answers at one position.
- **For benchmark papers**, the key analytical insight (three-skill decomposition, delta decomposition, etc.) is the most valuable thing to explain clearly.
- **Sequential papers from the same team** (MMMU → MMMU-Pro) benefit from explicit cross-referencing — the second paper's motivation directly maps to the first paper's Phase 4 weaknesses.
