# Research Wiki Log

## [2026-06-23] arxiv-scan | FAILED — Weekly digest 2026-06-23
- Status: FAILED — network egress policy blocks export.arxiv.org (and api.semanticscholar.org, api.crossref.org)
- All 10 keyword queries returned: "Host not in allowlist: export.arxiv.org"
- Papers found: 0 (scan could not execute)
- Action required: Add `export.arxiv.org` to the network egress allowlist in Claude Code on the Web environment settings (https://code.claude.com/docs/en/claude-code-on-the-web)
- Digest: wiki/research/outputs/weekly-2026-06-23.md (failure record)
- Notable: No papers retrieved — arXiv scan infrastructure fix needed before next run

## [2026-06-21] restructure | Wiki 3-domain structure (research / teaching / projects)
- wiki/ reorganized: existing pages moved to wiki/research/
- New domains: wiki/teaching/ (GitHub 동기화), wiki/projects/ (로컬 전용 — 기밀)
- .gitignore 추가: wiki/projects/ 제외
- CLAUDE.md 업데이트: Teaching(op 7), Industry Project(op 8) 워크플로우 추가

## [2026-06-21] ingest | Partitioning techniques for non-centralized predictive control (Riccardi et al. 2026)
- Paper page: wiki/papers/riccardi-2026-noncentralized-mpc-partitioning.md
- Pages updated: index.md
- Pages created: wiki/concepts/noncentralized-mpc.md, wiki/concepts/graph-partitioning-control.md, wiki/research-ideas/adaptive-partitioning-ev-chassis.md, wiki/research-ideas/data-driven-partitioning-energy-management.md
- Research ideas generated: (1) 적응형 분산 MPC 파티셔닝 for EV 섀시 제어, (2) 데이터 기반 파티셔닝 for EV 에너지 관리
- Key insight: EV 운전 모드 전환이 곧 토폴로지 변화이며, 논문이 명시한 "교통 분야 파티셔닝 공백"과 "데이터 기반 파티셔닝 미개척"이 교수님의 연구 확장 기회

## [2026-06-21] init | Research wiki initialized
- Owner: Prof. Kim Sooyoung, Sookmyung Women's University, Dept. Mechanical Systems Engineering
- Schema written: CLAUDE.md (research-focused, arXiv monitoring enabled)
- Directories: raw/papers/, wiki/papers/, wiki/concepts/, wiki/topics/, wiki/authors/, wiki/venues/, wiki/research-ideas/, wiki/outputs/
- Monitoring keywords: electrified vehicle control, regenerative braking, vehicle state estimation, adaptive vehicle control, autonomous vehicle control, physics-informed neural networks, intelligent vehicle, energy management, robust control, AI-enabled system
- arXiv categories: cs.SY, eess.SY
