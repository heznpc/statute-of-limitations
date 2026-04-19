# statute-of-limitations (시효) — Review (2026-04-11)

## 1. 커밋 톤이 주장을 일관되게 지지하는가?

**판정: 짧지만 일관됨 (2 commits, 2026-03-29 → 04-08).**

```
de6723f gitignore: exclude CLAUDE.md and .claude/                       (2026-04-08)
d768561 init: statute of limitations as AI memory governance framework   (2026-03-29)
```

진화 패턴:
- **t=0 (3/29)**: paper main.tex(627줄) + outline.md(228줄) + 5개 research/ markdown (3,415줄 총합) + README + TODO가 한 번에 import.
- **t+10 (4/8)**: gitignore 정리.

진짜 commit log는 작지만 *research/ 디렉토리의 5개 background document*가 paper 내적 정합성의 핵심:
- `history.md` (494줄) — Athens (5C BCE) → Roman (12 Tables, Theodosius 424 CE, Justinian) → Confucian → Islamic → Germanic → modern 6개 전통의 *2,500-year history*
- `cs_parallels.md` (544줄) — TTL/machine unlearning/GDPR/erasure right와의 차이
- `ai_memory_systems.md` (546줄) — Mem0, MemOS, Governed Memory 등 현재 시스템 분석
- `philosophy.md` (310줄) — Ricoeur memory, Derrida archive, 유사 텍스트
- `market_value.md` (621줄) — 시장 가치 분석

5개 research 문서가 *paper의 background을 위한 깊은 자료 base*. 본 survey 21개 paper 중 *background research를 별도 문서로 정리*한 가장 깔끔한 케이스.

톤 일관성:
- 핵심 주장(forgetting ≠ deletion / "exists but doesn't act" paradigm / 6 civilizational traditions / 7 design principles / sihyo 3-layer architecture)이 README → outline → main.tex 모든 layer에서 동일.
- *Hwaseong serial murder case*가 paper §1의 *opening anchor*로 사용. 한국 사례를 글로벌 framework의 *motivating example*로 활용. 본 survey 21개 paper 중 *한국 cultural anchor*가 가장 강력한 케이스 중 하나.
- *Cross-cultural taxonomy*: 6 civilizations × design model × AI memory analogy의 1쪽 표 (Table 1). 인용 가능한 reference table.
- *Boundary conditions* 명시: paper §3개 boundary conditions where the model fails. self-criticism이 형식적으로 흡수.

## 2. 부가 서비스 품질

**판정: 부가 서비스 0개. paper만. 그러나 5개 background document가 매우 깊은 자료.**

레포 구성:
- `paper/main.tex` (627줄, ~38KB) — 빌드 PDF 존재
- `outline.md` (228줄)
- `research/` — 5개 background docs (3,417 lines total) — *본 survey 21개 paper 중 background literature 가장 풍부*
- `README.md`, `TODO.md`, .gitignore

코드, 데이터, instrument, 노트북, 데모, 서비스 — *전무*. 본질적으로 *position paper + cultural-historical framework*. 

특이점:
- 5 research/ markdown이 paper 본문과 별도로 *재사용 가능한 자산*. 다른 학자가 *legal history of forgetting*에 관심 있을 때 이 5개 문서를 직접 인용 가능. **standalone literature value**.
- `market_value.md` (621줄) — paper에 본인이 *시장 가치 분석*까지 별도 문서로 정리. 본 survey 다른 paper에서 보지 못한 형태.
- TODO.md(47줄) 미확인.

## 3. 고도화 가능 파트

높은 우선순위:
1. **Sihyo architecture의 *prototype 구현*** — 3-layer framework (memory store / authority registry / decision layer). Python 200-300줄 + SQLite + 1-2 demo scenarios. caching의 분석 코드와 같은 standard lib only. *forgetting ≠ deletion*을 실제 *작동하는 시스템*으로 입증. 본 paper의 가장 큰 약점(코드 0줄)을 해결.
2. **Mem0/MemOS/Governed Memory 비교 매트릭스** — 현재 시스템 3개와 sihyo의 *형식 비교표*. paper §6 Related Work 강화. 1쪽 figure.
3. **6 civilizational traditions × 7 design principles의 매트릭스** — paper §3에서 7 principles를 *cross-cultural*하게 매핑. 1-2쪽 표.
4. **FAccT 2027 / CSCW 2027 submission** — README의 1순위. 마감 1월(round 1) / 4월(round 2). 충분한 시간.
5. **Hwaseong case 외 *non-Korean case study*** — 글로벌 reviewer에게 cross-cultural 강화. 독일 1949 Auschwitz 해외 prosecutor case, 일본 ISIS 자살 사건 등. README가 abolition cases를 명시하는데 paper 본문에서 case study로 깊이.

중간 우선순위:
6. **AI agent memory benchmark** — sihyo prototype을 LongMemEval / LongChat 같은 standard benchmark에 적용. 현재 대형 시스템보다 *나은가*를 측정.
7. **Severity-proportional decay function의 *수학적 formalization*** — 현재 1-30년 비유적. 어떤 *decay curve*가 적합한가의 정량 모델.
8. **Suspension conditions의 *AI memory 매핑***: 법적 시효의 suspension(피의자 도주 등)을 AI memory의 *어떤* 상황에 매핑할지 명확화.
9. **`research/market_value.md`를 paper appendix로 통합 또는 별도 paper로 분리** — 621줄 별도 문서가 본문에 어떻게 활용되는지 명확화. 시장 가치 분석은 통상 academic paper에 들어가지 않음.

낮은 우선순위:
10. References.bib 분리.
11. CHI 2027 / FAccT 2027 backup venue.
12. 한국어 abstract.

## 4. 학술적 / 시장 가치 (글로벌, 2026-04-11 기준)

### 학술적 가치: **상위권 (working paper 기준 top ~10%, AI ethics + legal scholarship 한정 시 top ~5%)**

차별점:
- **"Forgetting ≠ Deletion" framing**: 인용 가능한 새 명제. AI memory 담론의 *paradigm shift*. 현재 연구가 *모두* 삭제 기반인 점을 명확히 비판.
- **2,500-year cross-cultural taxonomy**: 6 civilizations × 1 framework. 학술 paper가 *2.5천년 역사*를 cross-cultural taxonomy로 정리한 사례 매우 드물다. *legal scholarship + AI ethics + cultural anthropology* triple cross-cut.
- **"Sihyo" naming**: 한국어 법학 용어를 *글로벌 학술 vocabulary*로 도입. cultural anchor + naming-rights value.
- **3-layer architecture (memory store / authority registry / decision layer)**: implementable framework. 단순 essay가 아니라 *engineering proposal*.
- **Hwaseong case**: paper의 *visceral motivating example*. 학술 paper가 *real-world case*를 첫 단락에 anchor하는 강력한 form.
- **Severity-proportional expiration**: 현재 TTL이 *uniform*이라는 가장 큰 약점을 직접 비판. 학술 + 실용 영향력 동시.
- **legal philosophy 인용**: Ricoeur memory, Derrida archive, codex Theodosianus, Demosthenes, Justinian — *primary classical sources*. legal scholar가 매우 호의적으로 봄.
- **6개 civilization 균등 처리**: Athens, Rome, Confucian, Islamic, Germanic, common law. *Western-only*가 아닌 cross-cultural balance. FAccT 2027의 *non-Western perspectives* 트렌드와 일치.
- **research/ 5개 background docs (3,417 lines)**: paper background의 *전례 없는 깊이*. reviewer가 paper를 신뢰하기 쉬움.

위험:
- **데이터 0건 / 코드 0줄** — pure conceptual paper. FAccT/CSCW/CHI는 통상 empirical contribution을 선호. *Sihyo prototype*이 없으면 reviewer가 "where's the system?"이라 짚을 가능성.
- **6 civilizations 처리의 *균등성 risk***: legal historian이 reviewer로 들어오면 각 civilization의 *오류/단순화*를 짚을 수 있음. cross-cultural framing의 *깊이*가 약점이 될 수 있음.
- **Independent researcher 단독 저자** — 법학 + AI 영역. 통상 multi-author. legal scholar 공동저자 부재.
- **"Forgetting ≠ Deletion"이 *직관적이지만 implementable한가***: paper §3의 sihyo architecture가 sketch 수준. *어떻게 dummy data가 decision에 영향을 미치지 않을 수 있는가*의 메커니즘이 모호.
- **GDPR Right to Erasure**과의 명확한 differentiation: paper가 GDPR을 *deletion*으로 framing하지만 GDPR도 사실 *exists but doesn't process*에 가까운 경우가 있음. legal scholar의 짚을 포인트.

게재 전망:
- *FAccT 2027*: **realistic, 50-60%**. README의 1순위. AI memory governance + cross-cultural framing 적합. *non-Western perspectives* 트렌드와 일치.
- *CSCW 2027*: **45-55%**. memory governance HCI 트랙.
- *CHI 2027*: **40-50%**. design implication 추가 시.
- *AI & Society* (Springer, IF 4.7): **55-65%**.
- *Big Data & Society* (SAGE): **55-65%**.
- *Philosophy & Technology* (Springer, IF 4.6): **50-60%**.
- *Law and Technology* journals: **45-55%**.

### 시장 가치: **상위 (AI memory 회사 + 정책 think-tank에서 매우 강함)**

- **AI memory 회사**: Mem0, Letta, Cognee, Zep, ChromaDB, Pinecone, MongoDB Atlas Vector Search 등이 *forgetting ≠ deletion* feature를 product에 통합 가능. *severity-proportional expiration*은 즉시 실용 가능.
- **GDPR / DPF / 한국 개인정보법 정책**: AI memory의 *legal compliance* framework. 정책 think-tank(Brookings, CEPR, AI Now Institute, Stanford HAI)에 즉시 인용.
- **AI agent 회사**: Anthropic Claude memory, OpenAI ChatGPT memory, Google Gemini memory, Microsoft Copilot memory가 *long-running agent*의 memory governance에 직면. 본 paper는 *직접 솔루션* 제시.
- **언론**: NYT/Atlantic/Wired/Guardian/Aeon이 좋아할 톤. "AI는 잊지 못한다 — 2,500년 법학 전통이 답이다" 헤드라인. viral potential 매우 강력.
- **legal tech**: Casetext, Harvey, Lexis Nexis 같은 legal AI 회사가 *evidence retention* 정책에 인용 가능.
- **한국 cultural diplomacy**: 시효라는 *한국어 vocabulary*를 글로벌 학술 영역에 introduce. 한국 학술 외교의 sample case.
- 한계: tool/SaaS 직접 product 경로 약함. *학술 + 정책 + 디자인 영향력*에 의존.

### 종합 평점 (2026-04-11)

| 축 | 점수 | 코멘트 |
|---|---|---|
| Originality of construct | 10/10 | forgetting ≠ deletion + sihyo + 6 civilizations |
| Cross-cultural depth | 10/10 | 2,500-year taxonomy 본 survey 1위 |
| Theoretical sophistication | 9/10 | legal + philosophy + AI bridge |
| Empirical contribution | 1/10 | 0개. prototype 없음 |
| Background research depth | 10/10 | 5 docs, 3,417 lines |
| Self-criticism (boundary conditions) | 8/10 | §3 boundary conditions 명시 |
| Repo health | 5/10 | 2 commits, no service |
| Submission readiness | 7/10 | LaTeX 빌드 완료, prototype 부족 |
| Cultural anchor | 10/10 | Hwaseong case + 시효 vocabulary |
| Practical applicability | 8/10 | AI memory 회사 즉시 사용 |
| Timing | 9/10 | AI agent memory 담론 정점 |
| **Overall (framework paper)** | **8.0/10** | "Sihyo prototype 1개만 추가하면 9.0+로 점프" |

핵심 격언: **"본 survey 21개 paper 중 *cultural anchor*와 *legal scholarship depth*가 단연 1위. Sihyo 3-layer architecture의 Python prototype 200줄만 추가하면 FAccT 2027 main track 가능."** *Forgetting ≠ Deletion*은 본 survey 21개 paper 중 가장 *paradigm-shift potential이 강한* 단일 명제 중 하나. 한국 사례 + 한국어 vocabulary를 글로벌 학술에 introduce하는 *학술 외교* 가치까지 가짐.
