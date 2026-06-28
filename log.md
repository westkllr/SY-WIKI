# Research Wiki Log

## [2026-06-28] arxiv-scan | 주간 동향 2026-06-28
- 발견 논문: 총 15편 (높음 4, 보통 4, 낮음 7)
- 다이제스트: wiki/research/outputs/weekly-2026-06-28.md
- 스캔 방식: WebSearch (Google) — arXiv API (export.arxiv.org) 차단 지속
- 높음 페이지 생성: wang-2026-pinn-ev-thermal-mpc.md, wang-2026-dbpnet-wheel-load.md, faghihian-2026-lyapunov-cacc-ev.md, miao-2026-physics-koopman-ev-trucks.md
- 보통 페이지 생성: lokur-2026-energy-optimal-thermal-bev.md, ngo-2026-adaptive-mpc-uam-lpv.md, loya-2026-koopman-offroad-vehicle.md, moyalan-2026-ecm-ev-evacuation.md
- 주목 논문: faghihian-2026-lyapunov-cacc-ev — 회생제동 동역학 내재화 Lyapunov 안정적 CACC, IEEE 학술대회 채택, 교수님 회생제동·적응형 제어·EV 안전 3개 영역 직접 연결

## [2026-06-24] process-update | 개념 페이지 작성 기준 강화 (CLAUDE.md 업데이트)
- CLAUDE.md Step 5 갱신: 개념 페이지에 (1) 교수님 연구 적용 방안, (2) 기존 방법론 비교표 필수 포함
- Concept Page 형식에 필수 섹션 추가 (한 줄 요약, 핵심 원리, 교수님 연구 적용, 기존 방법론 비교, 언제 사용)
- 소급 적용: adaptive-robust-estimation, gaussian-process-regression-control, dynamic-mode-decomposition 생성

## [2026-06-24] concept-expand | 핵심 알고리즘 개념 페이지 3종 소급 생성
- adaptive-robust-estimation.md (ARC): EKF 대비 이상값 강건성 + 공분산 적응; EV 상태추정 적용
- gaussian-process-regression-control.md (GPR): 불확실성 정량화 제어; 기존 물리모델+MPC 대비 비교
- dynamic-mode-decomposition.md (DMDc): 데이터 기반 선형 모델 추출; Koopman 관계, 배터리 ECM 적용
- 계기: 모든 wiki 업데이트 시 핵심 방법론 개념을 교수님 기존 방법론 비교 포함하여 상세 정리하는 새 지침

## [2026-06-24] concept-expand | Koopman Operator 기반 MPC — 교수님 관심 주제 심화 정리
- 생성: wiki/research/concepts/koopman-operator-control.md
- 내용: Koopman 연산자 원리, EDMD 학습 절차, 기존 MPC·NMPC·PINN MPC와 비교표, Zhang(2026) 기여 해설, EV 연구 적용 조건
- 계기: 교수님이 weekly digest에서 Koopman MPC에 관심 표명; MPC 전문가 / Koopman 생소 수준에 맞춰 작성
- 업데이트: zhang-2026 Connections에 [[koopman-operator-control]] 링크 추가, index.md 갱신

## [2026-06-24] delete | lin-2026-ai-power-converter-review
- 삭제: wiki/research/papers/lin-2026-ai-power-converter-review.md
- 사유: 교수님 연구 영역(차량 제어·추정·전동화 파워트레인)과 관련도 낮음 — 전력변환기 설계·운용 리뷰
- index.md에서 항목 제거

## [2026-06-24] ingest | Generalizable and Fast Surrogates: MPC of Articulated Soft Robots Using PINNs (Habich et al., IEEE TRO 2026)
- Paper page: wiki/research/papers/habich-2026-pinn-mpc-soft-robot.md
- Pages created: wiki/research/concepts/physics-informed-neural-networks.md, wiki/research/authors/leibniz-imes-group.md, wiki/research/research-ideas/pinn-surrogate-ev-nmpc.md
- Pages updated: schafke-2026-virtual-wheel-speed-sensor.md (Connections 추가), adaptive-partitioning-ev-chassis.md (PINN 결합 가능성 추가), index.md, log.md
- Research ideas generated: (1) PINN 서로게이트 기반 EV 파워트레인·섀시 NMPC [pinn-surrogate-ev-nmpc]
- Key insight: DD-PINN이 제1원리 모델 대비 467× 빠른 추론(2 μs)으로 47 Hz NMPC 실현 — EV 섀시·파워트레인 비선형 MPC에 직접 이전 가능; 동일 그룹(Ehlers)이 차량 동역학 PINN 논문(Zeipel et al. TechRxiv 2024) 투고 중으로 후속 ingest 필요

## [2026-06-23] arxiv-scan | Weekly digest 2026-06-23 — WebSearch 대체 스캔 성공
- Papers found: 18 total, 6 high, 6 medium, 6 low relevance
- Digest: wiki/research/outputs/weekly-2026-06-23.md (updated from FAILED to complete)
- Scan method: WebSearch (Google) — arXiv API (export.arxiv.org) remains blocked in network egress; all 10 keyword queries executed via WebSearch as alternative
- Pages created (HIGH): hadji-thomas-2026-arc-adaptive-robust-estimation.md, zhang-2026-koopman-mpc-time-delayed.md, sarkar-2026-data-driven-multi-fuel-engine.md, schafke-2026-virtual-wheel-speed-sensor.md, labib-2026-battery-voltage-dmdc-transformer.md, rachavelpula-2026-personalized-ev-energy.md
- Pages created (MEDIUM): ashraf-2026-frequency-domain-neural-ode.md, classens-2026-fault-detection-uncertain.md, lin-2026-ai-power-converter-review.md, barat-2026-battery-ecm-ensemble-kalman.md, vedula-2026-predictive-energy-hybrid-powertrain.md, he-2026-eco-driving-ev-multi-speed.md
- Notable: schafke-2026-virtual-wheel-speed-sensor — NN 가상 휠속도 센서로 ID.7에서 85% 오차 저감, IFAC World Congress 2026 (부산) 채택 — 한국 자동차 산업 및 교수님 EV 상태추정 연구와 직접 연관

## [2026-06-23] arxiv-scan | FAILED — Weekly digest 2026-06-23 (superseded by successful retry above)
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
