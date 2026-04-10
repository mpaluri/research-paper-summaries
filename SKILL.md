# Research Paper Summary Skill

## Purpose
Deeply understand research papers through a structured four-level learning flow, tested with quizzes at each level, and published as a permanent reference on GitHub Pages.

## Flow

```
1. User shares a paper (link, name, or topic)
2. Claude checks for multiple arXiv versions, confirms latest
3. Claude reads the paper thoroughly (ask user to upload PDF when possible)
4. Level 1 — Beginner explanation (plain language, analogies, no jargon)
   → Quiz (5 MCQ) — generated in background while user reads
5. Level 2 — Intermediate explanation (methods, architecture, training details)
   → Quiz (5 MCQ) — generated in background while user reads
6. Level 3 — Expert explanation (math, ablations, engineering decisions)
   → Quiz (5 MCQ) — generated in background while user reads
7. Level 4 — Frontier (limitations, post-paper landscape, open problems, scorecard)
   → Quiz (5 MCQ) — generated in background while user reads
8. Generate GitHub Pages output (paper HTML + index.html + README.md)
9. Cross-check all content for factual accuracy before pushing
10. Confirm with user → push to GitHub
```

**Key rules:**
- All 4 levels must be completed with all quizzes passed before pushing
- ONE paper per commit
- Generate quiz in background while user reads each section — serve instantly when asked
- When a concept deserves deep explanation (e.g., CoCa, CLS Token, Beam Search), give it a standalone deep dive and save to the ML Concepts Library

## Content Generation Rules

### Accuracy — Cross-Check Before Presenting
1. Generate content first
2. **Cross-check key claims** against primary sources (paper, Wikipedia, official blogs) via web search
3. Correct any errors found
4. Only then present to the learner
5. Never include a "cross-check notes" blurb without actually running the verification searches

### Quality
- Explain concepts with concrete examples, not just abstractions
- Use tables for comparisons, code blocks for architecture diagrams
- Training flow + inference flow for any new architecture (inputs → outputs → backprop, then inference modes)
- Never test on content not covered in the material
- Scrub all internal/proprietary references before pushing to GitHub

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

### Frontier (Level 4)
- What the paper got wrong or couldn't solve
- Post-paper landscape — what came after, who adopted the ideas
- Open research frontiers and improvement vectors
- Final scorecard (Novelty, Impact, Reproducibility, Technical Depth, Writing, Longevity)
- Quiz included (unlike earlier version that skipped L4 quiz)

## Quiz Design Rules

### Option Construction (per question)
1. Write the **correct answer** first
2. Write **2 close-but-wrong distractors** (adversarial — require real understanding to eliminate)
3. Write **1 clearly wrong option** (plausible-sounding but fundamentally off)
4. **Randomly assign** all 4 to positions A/B/C/D

### Bias Prevention
- **No position bias:** Randomize correct answer positions. Over time across levels and papers, each position should appear ~25%. Historical problem: B was correct 62.5% of the time, D was 0%. This is unacceptable.
- **No length bias:** All 4 options must be similar in length and detail. The correct answer must NOT be obviously longer or more nuanced than distractors.
- **No pattern bias:** Avoid predictable sequences.

### Hard Constraints (enforced per quiz)
- Across 5 questions, correct answers must hit **at least 3 of the 4 positions**
- No single position may be correct more than **twice** in a single quiz
- **Never test on content not covered** in the material presented at that level or earlier levels
- Questions must be answerable from the study material alone — no outside knowledge required

### Difficulty Scaling
- **Levels 1-2:** Straightforward recall and comprehension. Each option is clearly distinct.
- **Levels 3-4:** Add complexity:
  - "All of the above" / "None of the above" options
  - Roman numeral compound options (e.g., "I, II, and III only")
  - Distractors that are partially true but subtly wrong
  - Questions requiring synthesis across multiple sections

### Quiz Delivery
- **Plain text in chat** — all 5 questions listed, user answers by letter, Claude gives feedback
- Show score table after each quiz with running cumulative total
- 5 questions per quiz, 4 quizzes per paper = 20 questions per paper

## ML Concepts Library

When a concept deserves a standalone deep dive during paper study, it gets:
1. A full explanation with training flow, inference flow, and comparisons
2. Saved to the ML Concepts Library space
3. Referenced in future papers when relevant

**Current concepts:** FID, CoCa, CLS Token, Beam Search, Nucleus Sampling

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
  ├── METHODOLOGY.md
  ├── .claude/skills/research-paper-summary/SKILL.md  ← this file
  └── papers/
      ├── claudini.html
      ├── adaptation-agentic-ai.html
      ├── video-mme.html
      ├── mmmu.html
      ├── mmmu-pro.html
      ├── transfusion.html
      ├── chameleon.html
      ├── dalle3.html
      └── <next>.html
  ```

### For each new paper, generate:
1. `papers/<paper-name>.html` — Self-contained HTML with all 4 levels, quizzes, dark mode
2. Updated `index.html` — New paper card (newest first)
3. Updated `README.md` — New row (newest first)
4. Updated `SKILL.md` — Session reflections if needed

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
- Don't generate output before completing all four levels
- Beginner analogies matter most — they anchor everything after
- Show quiz explanations on BOTH correct and wrong answers in the HTML
- Plain ASCII for math in chat; Unicode/formatted in final HTML
- mm/dd/yy date format in README; newest papers first everywhere
- After output generation, auto-reflect and update skill + memory
- **Always read existing index.html and README.md before updating — don't drop existing papers**
- **Plain text quizzes work well** — especially for complex L3/L4 questions
- **Quiz position bias is real** — B was correct 62.5% of the time in early quizzes. Use the random construction method (write correct → 2 adversarial → 1 random → shuffle) to prevent this
- **Cross-check content against primary sources** before presenting — don't just add a "cross-check notes" blurb without actually verifying
- **For benchmark papers**, the key analytical insight (three-skill decomposition, delta decomposition, etc.) is the most valuable thing to explain clearly
- **Sequential papers from the same team** (MMMU → MMMU-Pro) benefit from explicit cross-referencing
- **Generate quiz in background** while user reads — serve instantly on demand
- **Never test on content not taught** — if MuZero wasn't explained, don't quiz on MuZero failure modes

---

_Last updated: 2026-04-09_
