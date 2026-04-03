# Research Paper Summaries

Three-level explainers (Beginner → Intermediate → Expert) for quickly understanding research papers.

**Live site:** `https://<your-username>.github.io/research-paper-summaries/`

## Papers

| # | Paper | Topic | Date |
|:--|:------|:------|:-----|
| 1 | [Claudini](papers/claudini.md) | AI safety, adversarial attacks, autoresearch | Mar 2026 |

## Setup (one time)

1. Create a new GitHub repo named `research-paper-summaries`
2. Upload all files from this directory maintaining the folder structure
3. Go to **Settings → Pages → Source**: Deploy from branch → `main` / `root`
4. Your site will be live in ~60 seconds

## Adding a new paper

1. Go through the paper learning exercise in Claude (beginner → quiz → intermediate → quiz → expert)
2. At the end, ask Claude to generate a GitHub Pages compatible summary
3. Claude will produce a new `.md` file — add it to the `papers/` folder
4. Update the table in `index.md` with a new row linking to it
5. Commit and push — the site updates automatically

## Repo structure

```
research-paper-summaries/
├── index.md              ← Home page / table of contents
├── _config.yml           ← Jekyll theme config
├── README.md             ← This file
└── papers/
    ├── claudini.md       ← Paper #1
    ├── next-paper.md     ← Paper #2 (future)
    └── ...
```

## How each summary works

Each paper has three collapsible levels:

- **Level 1 — Beginner**: Plain language, analogies, no jargon
- **Level 2 — Intermediate**: How methods work, key concepts, comparisons
- **Level 3 — Expert**: Full math, algorithms, related work, critical evaluation

## License

Content summaries are for personal educational use. All cited papers retain their original licenses.
