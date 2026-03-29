# 시효: Designing Institutional Forgetting for AI Agent Memory Systems

Paper Outline v0.1

---

## 1. Introduction

- AI memory systems treat forgetting as deletion (TTL, unlearning, erasure)
- But the oldest human institution for forgetting — statute of limitations (기원전 5세기 아테네) — does not delete
- It extinguishes **authority to act**, not information itself
- 화성연쇄살인: DNA identified the killer in 2019, files were intact, but prosecution was impossible — data existed, action authority had expired
- This paper: extract design principles from 2,500 years of institutional forgetting across civilizations, propose a new AI memory paradigm where **information persists but influence expires**

### 1.1 The Fundamental Asymmetry

- Human memory: forgetting is default, remembering costs effort
- Digital memory: preservation is default, deletion costs effort
- Statute of limitations: society's solution to institutionalize the natural human default into a system that doesn't forget on its own
- AI needs this same transplant — but current literature doesn't have it

## 2. Background: How Societies Designed Forgetting

### 2.1 Origins and Evolution

- Athens (5th c. BCE): first known statute — purpose was **sycophant control** (system abuse prevention), not mercy
- Rome: usucapio (450 BCE) → Theodosius II's 30-year praescriptio (424 CE) → Justinian's unification
- Justification logic evolved: abuse prevention → legal stability → evidence decay → defendant's repose → human rights

### 2.2 Cross-Cultural Taxonomy of Forgetting Design

| Design model | Civilizations | AI memory analogy |
|---|---|---|
| **No forgetting** (perpetual memory) | Confucian East Asia (China/Korea/Japan pre-modern) | Unlimited context window, no eviction |
| **Dual-rights hierarchy** | Islamic law (God's rights = no expiry, human rights = expiry) | System safety rules (no TTL) vs user preferences (TTL) |
| **Codified uniform decay** | Roman/Continental law (30yr → 3yr) | Uniform TTL for all memory types |
| **Pragmatic incremental** | English common law (1623 Act, "why 6 years?" — unknown) | Ad hoc retention policies |
| **Severity-proportional** | Modern criminal law (misdemeanor 1yr → murder never) | Memory-type-proportional TTL |
| **Abolition after failure** | Korea 2015, Japan 2010, Germany 1979 | Policy reversal when forgetting causes visible harm |

### 2.3 The Abolition Cases: What Happens When Forgetting Fails

- Germany 1965-1979: Nazi war criminal statute debate → abolition for murder
- Japan 2010: same-day enforcement to save a case expiring at midnight
- Korea 2015: 화성연쇄살인 + 태완이법 → abolition, but non-retroactive → killer identified but unpunishable
- Pattern: abolition is triggered when **new technology (DNA) invalidates the original justification (evidence decay)**

## 3. The Missing Paradigm: Exists But Doesn't Act

### 3.1 Current AI Memory Forgetting Models

| Approach | Mechanism | Problem |
|---|---|---|
| TTL/Expiration | Delete after time | Information irrecoverably lost |
| Machine unlearning | Remove from model weights | Technically fails (ICLR 2025) |
| GDPR erasure | Delete on request | Reactive, not systematic |
| Temporal decay | Reduce retrieval weight over time | Uniform decay, no severity distinction |
| Context window truncation | Drop oldest tokens | Accidental forgetting, not designed |

### 3.2 The Statute of Limitations Paradigm

- Information layer: data persists indefinitely (evidence archive)
- Authority layer: permission to act on data expires (prosecution power)
- Reactivation mechanism: new evidence can restart the clock (DNA → cold case reopened... but only if statute hasn't expired)
- Suspension conditions: clock pauses under specific circumstances (suspect flees jurisdiction)
- Non-retroactivity: new expiration policies don't apply to already-expired items

### 3.3 Eco's Paradox and Its Resolution

- Eco: "Intentional forgetting is impossible — the act of deletion evokes the memory"
- Machine unlearning confirms this: attempting to remove data leaves traces
- Statute of limitations **sidesteps** this paradox: it doesn't delete, so there's nothing to evoke
- Instead, it severs the link between information and action

## 4. Cross-Cultural Design Space for AI Memory Governance

### 4.1 The Confucian Model: Why "Never Forget" Fails

- Traditional East Asian law had no statute of limitations
- Moral violations don't expire → total retention
- AI parallel: systems that never evict memory → context rot (Chroma 2025), performance degradation
- The 1911 Qing adoption of Western statutes = acknowledging that perpetual memory is unsustainable even for states

### 4.2 The Islamic Dual-Rights Model: Hierarchical TTL

- God's rights (حق الله): murder, apostasy → no expiry
- Human rights (حق العبد): theft, slander → expiry applies
- AI translation: **system-level safety constraints** (no TTL) vs **user-level preferences** (TTL applies)
- Ottoman innovation: even God's rights got 15-year limits → pragmatism overriding theology

### 4.3 The Germanic/Modern Model: Severity-Proportional Decay

- Misdemeanor: 1-3 years
- Felony: 5-25 years
- Murder: no expiry
- AI translation: **memory type determines retention**
  - Formatting preference: short TTL
  - Factual correction: medium TTL
  - Safety-critical lesson: no TTL

### 4.4 The Abolition Pattern: When to Reverse Forgetting Policy

- Triggered by: (1) new technology invalidating justification, (2) catastrophic failure case, (3) social/political pressure
- AI parallel: when should an agent's memory governance policy be updated?
- Key tension: retroactivity — do new policies apply to already-forgotten items?

## 5. Framework: 시효-Based Memory Governance for AI Agents

### 5.1 Architecture

```
┌─────────────────────────────────┐
│         Decision Layer          │  ← checks authority before acting
├─────────────────────────────────┤
│       Authority Registry        │  ← tracks expiration status
├─────────────────────────────────┤
│     Memory Store (persistent)   │  ← data never deleted
└─────────────────────────────────┘
```

### 5.2 Design Principles (from 2,500 years of legal history)

1. **Separate storage from authority**: data persists, influence expires
2. **Severity-proportional expiration**: memory type determines TTL
3. **Suspension conditions**: clock pauses when memory is actively relevant
4. **Non-retroactivity**: policy changes don't affect already-expired items
5. **Reactivation mechanism**: new context can restore expired authority
6. **Hierarchical rights**: system safety vs user preference distinction
7. **Transparent expiration**: user/system can query why something expired

### 5.3 Comparison with Existing Systems

| Feature | Mem0 | MemOS | Governed Memory | 시효 |
|---|---|---|---|---|
| Data persistence after expiry | No | No | No | **Yes** |
| Severity-proportional TTL | No | No | No | **Yes** |
| Reactivation mechanism | No | No | No | **Yes** |
| Suspension conditions | No | No | No | **Yes** |
| Non-retroactive policy changes | No | No | No | **Yes** |
| Cross-cultural design taxonomy | No | No | No | **Yes** |

## 6. Discussion

### 6.1 Connections to Adjacent Work

- Mayer-Schönberger's *Delete* (2009): proposed user-set expiration dates, but pre-LLM and mechanism is different (user-set vs system-designed)
- GDPR right to be forgotten: reactive deletion vs systematic expiration
- Esposito's algorithmic memory sociology: theoretical but no design principles
- Ploidy (own work): fresh session as structural forgetting — 시효 provides the theoretical grounding

### 6.2 Complementary Evidence from Adjacent Research

The 시효 framework addresses a gap visible across multiple lines of AI-human interaction research:

**시효 as the missing design layer:**

| Phenomenon (observed) | What 시효 adds |
|---|---|
| **Context accumulation → confirmation bias** (Narcissus): Deep sessions produce 12:0 biased validation because accumulated context retains full decision authority indefinitely | Authority expiration on older context would force periodic re-evaluation, structurally breaking the entrenchment loop |
| **Amplification-Degradation-Correction cycle** (Meta): AI-mediated research degrades as context accumulates, requiring manual correction passes | 시효 explains *why* correction is needed — context without expiration degrades signal-to-noise — and provides a design principle to automate it |
| **Accumulation automatic, curation costly** (Tidal): AI amplifies digital hoarding by default; mitigation requires active effort | 시효 is the 2,500-year-old institutional solution to this exact asymmetry — systematic, automatic authority decay without requiring user action |
| **Streak mechanics → persistent low-quality content** (Sediment): Platform UIs that reward temporal continuity produce filler that persists indefinitely | Authority expiration on older contributions would reduce the visibility/influence of accumulated sediment without deleting it |
| **Information pollution co-evolves with algorithms** (AI Slop): Algorithms grant action authority to old slop content via recommendation, perpetuating the cycle | 시효 breaks the feedback loop by expiring algorithmic action authority on aging content |
| **ADHD as natural 시효** (Eddy): Rapid context-switching = fast authority expiration on previous context, which becomes an advantage when AI handles reconstruction | Reframes ADHD not as deficit but as naturally aggressive authority expiration — the biological version of what 시효 proposes for AI |

### 6.3 Boundary Conditions: Where 시효 Fails

Three adjacent research findings expose the limits of the 시효 model:

#### 6.3.1 Collection Bias is Prior to Expiration (Silo)

Recommendation algorithms create confirmation-biased digital hoards by filtering what users *encounter* — counter-evidence is never saved in the first place. 시효 governs what happens to information *after* acquisition. It cannot fix a collection that was biased at intake.

**Implication for framework:** Authority expiration on a biased memory store still produces biased decisions. 시효 must be paired with acquisition-diversity mechanisms — it is necessary but not sufficient.

#### 6.3.2 Expert Knowledge Resists Expiration (Caching)

Expert users practice deliberate scatter-caching across multiple tools, framing it as "knowledge management." Applying uniform authority expiration to expert-curated knowledge risks destroying carefully maintained reference systems.

**Implication for framework:** The severity-proportional design in Section 5.2 must include a "user-validated" tier where explicit curation acts as a suspension condition (analogous to how filing a legal claim pauses the statute clock). Memory that the user actively maintains should resist expiration.

#### 6.3.3 The Elixir Problem: Expiration Blocks Future Need (Elixir)

In-game "elixir hoarding" — saving powerful items for a moment that never comes — mirrors a real risk of authority expiration. If a memory's action authority expires and the agent later encounters the exact situation where that memory was critical, the system has created the 화성연쇄살인 pattern: the evidence exists, but the authority to act was extinguished too early.

**Implication for framework:** Reactivation mechanisms (Section 5.2, Principle 5) are not optional — they are structurally essential. The framework must provide low-cost reactivation paths when new context matches expired memories, just as DNA evidence can reopen cold cases (in jurisdictions where the statute hasn't expired).

### 6.4 The False Positive / False Negative Tradeoff

- 화성연쇄살인: statute meant killer went free (false negative)
- 윤성여: absence of statute might have prolonged wrongful imprisonment (false positive)
- AI parallel: aggressive retention risks acting on stale data, aggressive expiry risks losing critical context
- No perfect policy — but 2,500 years of legal evolution provides the best available heuristics
- The three boundary conditions above (Silo, Caching, Elixir) delineate where the tradeoff is sharpest

## 7. Conclusion

- "Forgetting = deletion" is a design poverty
- Human societies spent 2,500 years developing a richer model: information persists, authority expires
- Cross-cultural variation provides a taxonomy of design choices
- AI agent memory systems should import this distinction

---

## References (Key)

### Legal History
- Demosthenes on prothesmia and sycophant control
- Codex Theodosianus 4.14.1 (424 CE)
- Limitation Act 1623 (England)
- German Verjährungsdebatte (1965-1979)
- Korean 태완이법 (2015)
- ICC Rome Statute Art. 29 (2002)

### AI Memory
- Mem0 (2025), arXiv 2504.19413
- MemOS (2025)
- Governed Memory (2026), arXiv 2603.17787
- "Memory in the Age of AI Agents" (2025), arXiv 2512.13564
- Machine unlearning failures, ICLR 2025
- Context rot, Chroma (2025)

### Philosophy / Social Science
- Eco, "Ars Oblivionalis" — impossibility of intentional forgetting
- Mayer-Schönberger, *Delete: The Virtue of Forgetting in the Digital Age* (2009)
- Esposito, "Algorithmic Memory and the Right to be Forgotten" (2017)
- Assmann, 7 forms of forgetting
- Ricoeur on unbearable total memory
