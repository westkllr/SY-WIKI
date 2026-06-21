# Research Wiki — Schema

**Owner:** Prof. Kim Sooyoung (김수영), Department of Mechanical Systems Engineering, Sookmyung Women's University
**Purpose:** Track research trends, accumulate paper knowledge, and generate new research/paper ideas in vehicle control and electrified/autonomous vehicle systems.

Read this file at the start of every session before doing anything else.

## Directory Layout

```
d:\00_클로드 연구에이전트\
├── raw/
│   ├── papers/           # PDF or markdown source files (immutable — never modify)
│   └── assets/           # Downloaded images
├── wiki/
│   ├── papers/           # One summary page per ingested paper
│   ├── concepts/         # Technical concepts, methods, frameworks
│   ├── topics/           # Research area overview pages
│   ├── authors/          # Key researchers in the field
│   ├── venues/           # Journals and conferences
│   ├── research-ideas/   # Potential research directions and paper ideas
│   └── outputs/          # Comparison tables, syntheses, weekly digests
├── index.md              # Content catalog — update on every operation
├── log.md                # Append-only operation log
└── CLAUDE.md             # This file
```

## Research Profile

### Core Research Areas
1. AI-based vehicle control and modeling
2. Adaptive and personalized control for intelligent vehicle systems
3. Safety and dynamics control for electrified vehicles
4. Optimal control for electrified powertrains
5. Vehicle state and parameter estimation

### arXiv Monitoring Keywords
Primary (cs.SY, eess.SY categories):
- `electrified vehicle control`
- `regenerative braking`
- `vehicle state estimation`
- `adaptive vehicle control`
- `autonomous vehicle control`
- `physics-informed neural networks`
- `intelligent vehicle`
- `energy management`
- `robust control`
- `AI-enabled system`

### Key Journals / Venues
- IEEE Transactions on Vehicular Technology
- IEEE/ASME Transactions on Mechatronics
- Control Engineering Practice
- IEEE Transactions on Control Systems Technology
- International Journal of Robust and Nonlinear Control
- Vehicle System Dynamics
- Mechatronics
- IEEE Access

---

## Page Formats

### Paper Page (`wiki/papers/`)

```yaml
---
title: "Full paper title"
type: paper
authors: [Last, First, ...]
year: YYYY
journal: Journal name
doi: 10.xxxx/xxxxx
tags: [keyword1, keyword2]
methods: [MPC, EKF, PINN, ...]
source_file: raw/papers/filename.pdf   # if available
has_full_text: true | false
last_updated: YYYY-MM-DD
---
```

Sections:
- **Abstract** (2-3 sentences)
- **Key Contributions** (bullet list)
- **Methods** (what techniques/frameworks are used)
- **Key Results** (quantitative where possible)
- **Limitations / Open Questions** (what the paper does not address)
- **Research Ideas** (concrete follow-on directions this paper suggests — always include)
- **Connections** (wikilinks to related papers, concepts, authors, topics)
- **Notable Quotes / Figures**

### Concept Page (`wiki/concepts/`)

```yaml
---
title: "Concept name"
type: concept
tags: [tag1, tag2]
papers: [paper-slug-1, paper-slug-2]
last_updated: YYYY-MM-DD
---
```

### Research Idea Page (`wiki/research-ideas/`)

```yaml
---
title: "Idea title"
type: research-idea
status: raw | developing | ready
tags: [tag1, tag2]
inspired_by: [paper-slug-1, ...]
last_updated: YYYY-MM-DD
---
```

Sections:
- **One-line pitch**
- **Background** (what gap or observation motivates this)
- **Proposed approach**
- **Why this is feasible** (existing methods/data/tools to build on)
- **Novelty** (what makes it distinct from existing work)
- **Open questions**

### Other Page Types

All other pages (topics, authors, venues, outputs) begin with frontmatter:
```yaml
---
title: Human-readable title
type: topic | author | venue | output
tags: [tag1, tag2]
last_updated: YYYY-MM-DD
---
```

File naming: lowercase, hyphens, no spaces (e.g., `mpc-vehicle-control.md`, `ieee-tvt.md`).
Cross-references use Obsidian wikilink syntax: `[[filename-without-extension]]`. Link liberally.

---

## Operations

### 1. Ingest (interactive — follow exactly)

When the user asks to ingest a paper:

1. **Read** the source from `raw/papers/` (or from the user's pasted text / URL if no file).
2. **Discuss**: What are the 2-3 most important contributions? What is surprising or contradictory? What does this change in the research landscape?
3. **Write** the paper page in `wiki/papers/` following the paper page format above. Always include the **Research Ideas** section — extract at least 2 concrete follow-on directions.
4. **Scan** existing wiki pages for connections:
   - Update related topic, concept, and author pages
   - Add cross-references
   - Flag contradictions with `> [!warning] Contradiction with [[other-page]]`
   - Strengthen synthesis where this paper confirms existing claims
5. **Create** missing concept, author, or topic pages introduced by this paper.
6. **Check** `wiki/research-ideas/` — does this paper make any existing idea more feasible or less novel? Update accordingly.
7. **Update** `index.md`.
8. **Append** to `log.md`:
   ```
   ## [YYYY-MM-DD] ingest | Paper Title
   - Paper page: wiki/papers/filename.md
   - Pages updated: list
   - Pages created: list
   - Research ideas generated: list titles
   - Key insight: one sentence
   ```
9. **Report**: what was ingested, what changed, any contradictions, research ideas generated.

### 2. Weekly arXiv Scan (automated)

Runs weekly via scheduled agent. Search arXiv API for papers from the past 7 days matching the monitoring keywords in categories cs.SY and eess.SY.

arXiv API base URL: `https://export.arxiv.org/api/query`

For each keyword, query:
```
search_query=ti:{keyword}+OR+abs:{keyword}&cat=cs.SY+eess.SY&sortBy=submittedDate&sortOrder=descending&max_results=20
```

Steps:
1. Fetch results for all monitoring keywords.
2. Deduplicate by arXiv ID.
3. Score relevance to the 5 core research areas (high / medium / low).
4. For **high relevance** papers: create a full draft paper page in `wiki/papers/` (mark `has_full_text: false`).
5. For **medium relevance** papers: create a brief stub entry.
6. Write a weekly digest to `wiki/outputs/weekly-YYYY-MM-DD.md` — title, authors, one-line summary, relevance tag, arXiv link for each paper.
7. Update `index.md`.
8. Append to `log.md`:
   ```
   ## [YYYY-MM-DD] arxiv-scan | Weekly digest YYYY-MM-DD
   - Papers found: N total, X high, Y medium, Z low relevance
   - Digest: wiki/outputs/weekly-YYYY-MM-DD.md
   - Notable: one-sentence highlight of the most interesting paper
   ```

### 3. Research Idea Generation

When the user asks to generate research ideas (from a paper, a topic, or from scratch):

1. Read the relevant paper/topic pages.
2. Identify: open problems stated in papers, gaps between methods, cross-domain transplants (technique from field A applied to field B), extensions of existing work.
3. For each promising idea, write a page in `wiki/research-ideas/` following the research idea format.
4. Update `index.md`.
5. Report the ideas generated with a brief rationale for each.

### 4. Query

When the user asks a question:

1. Read `index.md` to find relevant pages.
2. Read those pages in full.
3. Synthesize answer with wikilink citations.
4. Ask: should this be filed as an output page? If yes, write to `wiki/outputs/` and update `index.md`.

### 5. Comparison Table

When comparing papers, methods, or approaches:

1. Gather data from relevant wiki pages.
2. Produce a markdown table with evidence quality (which paper each claim comes from).
3. Ask if this should be filed in `wiki/outputs/`.

### 6. Lint

When the user asks for a wiki health check:

1. Scan all pages for: contradictions, stale claims, orphan pages, concepts mentioned but lacking pages, missing cross-references, ideas that have become less novel due to new papers.
2. Suggest 3-5 new questions worth investigating.
3. Suggest 2-3 types of papers/sources worth finding.
4. Do NOT silently fix contradictions — surface them first.

---

## Conventions

- **Red links are intentional.** Link to concepts/entities that deserve pages even if the page doesn't exist.
- **Never delete raw sources.** If superseded, note it on the paper page.
- **File answers.** Good query outputs shouldn't disappear into chat history.
- **Contradiction callouts.** Use `> [!warning] Contradiction with [[other-page]]`
- **Research Ideas are mandatory in paper ingest.** Every paper page must have a Research Ideas section.
- **Dates.** Always YYYY-MM-DD.

## Index Format

`index.md` organized by category. Each entry: `- [[page-name]] — one-line description`

Under Papers: include year and journal. Example:
`- [[kim-2026-regenerative-braking]] — Tire-force-based regenerative braking torque limiting for EV stability (Control Engineering Practice, 2026)`

## Log Format

`log.md` entries: `## [YYYY-MM-DD] operation | label`
