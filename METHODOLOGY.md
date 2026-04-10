# Study System Methodology

## Paper Study Flow

Each paper goes through **4 levels**, each followed by a 5-question quiz:

| Level | Name | Focus |
|-------|------|-------|
| 1 | **Beginner** | Core idea, why it matters, key results |
| 2 | **Intermediate** | Architecture details, training pipeline, evaluation |
| 3 | **Expert** | Technical depth, ablations, engineering decisions, math |
| 4 | **Frontier** | Limitations, post-paper landscape, open problems, legacy |

**Rules:**
- All 4 levels must be completed with all quizzes passed before pushing to GitHub
- ONE paper per commit
- Update `index.html` and `README.md` with each new paper

## Content Generation Rules

### Accuracy
1. Generate content first
2. **Cross-check claims** against primary sources (paper, Wikipedia, official blogs) via web search
3. Correct any errors found
4. Only then present to the learner

### Quality
- Explain concepts with concrete examples, not just abstractions
- Use tables for comparisons, code blocks for architecture diagrams
- When a concept deserves deep explanation (e.g., CoCa, CLS Token, Beam Search), give it a standalone deep dive and save to the ML Concepts Library
- Never test on content not covered in the material
- Scrub all internal/proprietary references before pushing to GitHub

### Quiz Workflow
- **Generate quiz in background** while the user reads each section
- Serve instantly when the user is ready — no waiting

## Quiz Design Rules

### Option Construction (per question)
1. Write the **correct answer**
2. Write **2 close-but-wrong distractors** (adversarial — require real understanding to eliminate)
3. Write **1 clearly wrong option** (plausible-sounding but fundamentally off)
4. **Randomly assign** all 4 to positions A/B/C/D

### Bias Prevention
- **No position bias:** Correct answers must be distributed across A/B/C/D. Over time across levels and papers, each position should appear ~25%. No single position should dominate within a quiz.
- **No length bias:** All 4 options should be similar in length and detail. The correct answer should NOT be obviously longer or more nuanced than distractors.
- **No pattern bias:** Avoid predictable sequences (e.g., never having D as correct, always using B).

### Difficulty Scaling
- **Levels 1-2:** Straightforward recall and comprehension. Each option is clearly distinct.
- **Levels 3-4:** Add complexity:
  - "All of the above" / "None of the above" options
  - Roman numeral compound options (e.g., "I, II, and III only")
  - Distractors that are partially true but subtly wrong
  - Questions requiring synthesis across multiple sections

### Hard Constraints
- Across 5 questions in a quiz, correct answers must hit **at least 3 of the 4 positions**
- No position may be correct more than **twice** in a single quiz
- **Never test on content not covered** in the material presented at that level or earlier levels
- Questions must be answerable from the study material alone — no outside knowledge required

## Scoring

- 5 questions per quiz, 4 quizzes per paper = 20 questions per paper
- Running cumulative score tracked across all papers
- Perfect streak tracking for motivation

## ML Concepts Library

When a concept deserves a standalone deep dive during paper study (e.g., FID, CoCa, CLS Token, Beam Search, Nucleus Sampling), it gets:
1. A full explanation with training flow, inference flow, and comparisons
2. Saved to the ML Concepts Library space
3. Referenced in future papers when relevant

---

_Last updated: 2026-04-09_
