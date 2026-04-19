# Computer Science Parallels: "Data Persists, Authority Expires"

> Patterns in existing systems where information survives but its power to drive action is curtailed
> For: Section 3/5 of the 시효 paper (existing paradigm analysis + framework comparison)
> Date: 2026-03-29

---

## Analytical Framework

For each pattern, four questions:

1. **Persistence**: Does data survive after "expiration"?
2. **Reactivation**: Can expired authority be restored?
3. **Severity differentiation**: Do different types get different treatment?
4. **Proximity to the 시효 model**: How close is this to "information persists, influence expires"?

---

## 1. Soft Delete / Tombstones in Databases

### 1.1 Cassandra

When data is deleted in Cassandra, nothing is physically removed. Instead, a **tombstone marker** is written -- a timestamped deletion record that makes the deleted data invisible to reads. The tombstone itself is an insert (Cassandra treats deletion as a write). Tombstones persist for a configurable grace period (`gc_grace_seconds`, default 10 days), after which they are eligible for removal during compaction.

Key mechanism: the tombstone doesn't erase data -- it **suppresses its visibility**. Until compaction runs, the original data and the tombstone coexist on disk. In a distributed system, this grace period ensures all replicas learn about the deletion before the marker is removed, preventing "zombie data" resurrection.

### 1.2 HBase

Identical principle: a Delete command writes a tombstone marker rather than removing data. The original cells remain physically present but invisible to queries. Tombstones are only resolved during **major compactions** (which merge all store files), because proving a tombstone has no remaining effect requires examining all cells.

### 1.3 PostgreSQL (MVCC)

PostgreSQL's Multi-Version Concurrency Control never overwrites or immediately removes rows. An UPDATE creates a new tuple and marks the old one as dead via the `xmax` system column (the transaction ID that invalidated it). The dead tuple remains physically present, visible to transactions that started before the update. The VACUUM process eventually reclaims space, but until then, the data **exists in full, invisible only to new transactions**.

This is a temporal visibility model: data doesn't lose existence, it loses the authority to appear in current reads.

### 1.4 LSM Trees (General Pattern)

Log-Structured Merge trees (used by Cassandra, HBase, RocksDB, LevelDB) treat deletion as append-only tombstone writes. The actual data removal happens asynchronously during compaction. Between write and compaction, deleted data and its tombstone coexist -- the data exists but has been stripped of its ability to appear in results.

### Analysis

| Dimension | Assessment |
|---|---|
| **Persistence** | Yes, but temporary -- eventual physical deletion during compaction/vacuum |
| **Reactivation** | No explicit mechanism. In Cassandra, if a tombstone is lost before propagating to all replicas, the "deleted" data can resurrect (an anti-pattern, not a feature) |
| **Severity differentiation** | No -- all tombstones follow the same gc_grace_seconds regardless of data type |
| **Proximity to 시효** | **Moderate**. Tombstones separate "exists" from "visible/actionable," but the intent is eventual physical deletion, not permanent persistence with expired authority. The model is transitional, not terminal. |

**Key distinction from 시효**: Tombstones are a *mechanism for deferred deletion*, not a *paradigm for authority expiration*. The data is in limbo, not in archive. The 시효 model would keep the evidence file permanently but strip the prosecution's authority to use it.

---

## 2. Capability-Based Security and Token Expiration

### 2.1 OAuth 2.0 Token Lifecycle

In OAuth, an **access token** grants time-limited permission to act on a resource. When the token expires, the resource (API, data, user account) persists unchanged -- only the **authority to access** it disappears. The resource owner's data continues to exist; what expired is the delegated capability to interact with it.

Design features:
- **Short-lived access tokens** (5-60 minutes) vs **longer-lived refresh tokens** (days/weeks)
- **Revocation**: tokens can be explicitly invalidated before expiry (RFC 7009)
- **JWT challenge**: stateless JWTs are validated locally, so revocation requires coordination mechanisms (revocation lists, short TTLs, or introspection endpoints)

### 2.2 Time-Based Access Control (TBAC)

TBAC adds a temporal layer to RBAC/ABAC: permissions are granted with explicit expiration times. Azure's Privileged Identity Management issues "eligible" role assignments that must be activated and automatically expire. The resource persists; the permission to act on it does not.

### 2.3 Certificate Revocation (PKI)

A revoked certificate is not deleted from the PKI system. It continues to exist with its full cryptographic content. What changes is its **status**: the Certificate Revocation List (CRL) or OCSP responder marks it as invalid. Any system checking the certificate's status will refuse to trust it, but the certificate itself persists.

Critical detail: CRL supports a **"hold" status** -- temporary invalidity that can be reversed. If the private key is found uncompromised, the certificate can be reinstated. This is the closest to a suspension/reactivation mechanism in the 시효 model.

### Analysis

| Dimension | Assessment |
|---|---|
| **Persistence** | **Yes** -- resources and certificates persist fully after token/certificate expiry |
| **Reactivation** | **Yes** -- refresh tokens can obtain new access tokens; CRL "hold" status is reversible |
| **Severity differentiation** | **Yes** -- access tokens (minutes) vs refresh tokens (days); different certificate types have different validation policies |
| **Proximity to 시효** | **High**. This is the closest existing CS pattern. The resource (evidence) persists. The token (prosecution authority) expires. Refresh tokens parallel "reactivation on new evidence." CRL hold parallels suspension of the statute clock. |

**Key distinction from 시효**: Token expiry is designed for **security** (minimize attack window), not for **governance** (manage the relationship between information and action over time). The 시효 model adds the "why" -- severity-proportional expiration periods and policy-level justification for why different memory types deserve different authority lifespans.

---

## 3. Data Retention Policies in Enterprise Systems

### 3.1 Standard Enterprise Model

Enterprise retention policies define how long data must be kept and what happens after. After expiration, the typical outcome is **deletion or archival** -- not persistent storage with restricted authority. Microsoft Purview, for instance, supports both "retain then delete" and "retain then do nothing" policies, but the dominant pattern is eventual destruction.

### 3.2 GDPR Article 17 vs Article 18

GDPR provides an instructive split:
- **Article 17 (Right to Erasure)**: data is deleted -- the standard "forget = delete" model
- **Article 18 (Right to Restriction of Processing)**: data is **retained but processing is restricted**. The data controller must mark the data and ensure it is not processed except with consent or for legal claims

Article 18 is structurally close to the 시효 model: the data exists, but its authority to drive processing decisions is curtailed. However, Article 18 is triggered by the data subject's request, not by systematic time-based expiration.

### 3.3 Legal Hold / Litigation Hold

When litigation is anticipated, organizations must preserve relevant data regardless of normal retention policies. Data that would otherwise be deleted is placed under a **legal hold** -- it persists, and its deletion authority is suspended. This parallels the 시효 concept of "suspension of the statute clock" (tolling).

### Analysis

| Dimension | Assessment |
|---|---|
| **Persistence** | Mixed -- standard policies delete; GDPR Art. 18 and legal holds preserve |
| **Reactivation** | Legal hold can be lifted, restoring normal deletion schedules |
| **Severity differentiation** | **Yes** -- different data types (financial records, health data, employment records) have different retention periods, often mandated by sector-specific regulation |
| **Proximity to 시효** | **Low to Moderate**. Most enterprise retention is "retain then delete," which is TTL, not 시효. GDPR Art. 18 is structurally similar but reactive (user-triggered), not systematic (time-triggered). Legal hold parallels tolling/suspension. |

**Key distinction from 시효**: Enterprise retention policies manage the **data lifecycle** (when does data get deleted?), not the **authority lifecycle** (when does data lose its power to drive decisions while continuing to exist?). The two lifecycles are collapsed into one.

---

## 4. Embargo Periods in Publishing/Research

### 4.1 Mechanism

An academic embargo temporarily restricts access to published work for a defined period (typically 6-48 months). During the embargo:
- **Metadata is publicly visible** (title, abstract, author, DOI)
- **Full content is restricted** (files are private)
- After embargo expiry, content becomes publicly accessible

The embargo doesn't affect whether the data *exists* -- it affects who can *access* it and when. Figshare, institutional repositories, and publishers all implement this as a temporal access gate with automatic expiration.

### 4.2 Design Features

- Automatic expiration: no human intervention needed to lift the embargo
- Extension mechanism: authors can request embargo extensions before expiry
- Metadata visibility: the *existence* of information is never hidden, only its *substance*
- Reason-based: embargoes are justified (patent pending, publisher agreement, NDA)

### Analysis

| Dimension | Assessment |
|---|---|
| **Persistence** | **Yes** -- data exists throughout, only access is gated |
| **Reactivation** | **Automatic** at expiry; extensions possible by request |
| **Severity differentiation** | **Implicit** -- different reasons (patent, publisher, NDA) produce different embargo lengths |
| **Proximity to 시효** | **Moderate**. Embargoes restrict access, not authority. The direction is inverted from 시효: embargoes *grant* access after time passes, while 시효 *revokes* authority after time passes. But the structural principle -- temporal gates on what can be done with persistent information -- is shared. |

**Key distinction from 시효**: Embargoes are **access-granting** over time (locked -> unlocked). 시효 is **authority-revoking** over time (active -> expired). They are mirror images sharing the same structural insight: data persistence and action authorization are separable dimensions.

---

## 5. Sunset Clauses in Legislation

### 5.1 Mechanism

A sunset provision writes an expiration date into law. When the date arrives, the law ceases to have effect unless the legislature explicitly renews it. The law doesn't disappear from the legal record -- it remains in statute books, accessible for reference, but loses its **binding authority**.

Types:
- **Date-specific**: expires on a calendar date
- **Event-based**: expires when a condition is met
- **Conditional**: depends on meeting/failing a metric
- Review triggers: the approaching sunset forces evaluation (e.g., Texas Sunset Advisory Commission)

### 5.2 Historical Effectiveness

Introduced widely in US states in the 1970s, sunset clauses were intended to combat "legislative lethargy." In practice, they had mixed results: the burden of proof often shifted from agencies to reviewing staff, and renewal became routine. Most sunseted programs were renewed rather than terminated.

### Analysis

| Dimension | Assessment |
|---|---|
| **Persistence** | **Yes** -- the law remains in the record, only its binding authority expires |
| **Reactivation** | **Yes** -- explicit legislative renewal restores authority |
| **Severity differentiation** | **Yes** -- different laws get different sunset periods; some have no sunset (permanent legislation) |
| **Proximity to 시효** | **Very High**. This is the legislative equivalent: the rule (information) persists in the record, but its power to compel (authority) expires. Renewal parallels reactivation. The key difference is that sunset clauses are designed for prospective governance (should this law continue?), while 시효 is about retrospective limitation (should past events still drive action?). |

**Key insight for paper**: Sunset clauses demonstrate that even within legal systems, the "data persists, authority expires" pattern exists *outside* the statute of limitations context. It is a general governance principle, not limited to criminal law.

---

## 6. Cooldown Periods in Game Design

### 6.1 Mechanism

A cooldown is a mandatory waiting period after an ability is used, during which that ability exists in the player's inventory but cannot be activated. The ability is visible, its properties are known, but it is **temporarily stripped of execution authority**.

Design properties:
- **Severity-proportional**: high-impact abilities have longer cooldowns (seconds for basic attacks, minutes/hours for ultimate abilities)
- **Visual indicator**: desaturated icon with a "cooldown swirl" -- the ability is *visibly present but visibly inert*
- **Automatic reactivation**: authority restores when the timer completes
- **No user override**: cooldowns generally cannot be bypassed (though some abilities reduce others' cooldowns)

### Analysis

| Dimension | Assessment |
|---|---|
| **Persistence** | **Yes** -- the ability never disappears, it just becomes temporarily unusable |
| **Reactivation** | **Yes** -- automatic after time elapses |
| **Severity differentiation** | **Yes** -- the cooldown duration is proportional to the ability's power |
| **Proximity to 시효** | **Moderate**. The structural pattern matches (exists but cannot act), and severity-proportional timing is a shared feature. But cooldowns are *cyclical* (repeatedly triggered by use) while 시효 is *linear* (triggered once by an event, counts down once). Cooldowns also lack the irreversibility dimension -- an expired statute of limitations typically cannot be restored by "using the ability again." |

**Key insight for paper**: Game design independently discovered that "the power of an action should be inversely proportional to its availability over time" -- the same intuition behind severity-proportional statute of limitations periods. This convergent design suggests the pattern is a fundamental balance mechanism.

---

## 7. Quarantine in Email/Security

### 7.1 Mechanism

Email quarantine isolates suspicious messages from the user's inbox. The message is fully preserved -- headers, body, attachments -- but removed from active processing. It exists in a holding area where it cannot influence the user's workflow unless explicitly released.

Properties:
- **Automatic expiration**: quarantined messages are deleted after 15-30 days if not acted upon
- **Release mechanism**: admin or user can review and release a quarantined message to the inbox, restoring its ability to be read and acted upon
- **Classification-based**: different threat levels trigger different quarantine policies (phishing vs spam vs bulk mail)

### 7.2 Security Quarantine (General)

Antivirus quarantine isolates infected files in an encrypted container. The file persists but cannot execute. It can be restored if determined to be a false positive, or deleted after review.

### Analysis

| Dimension | Assessment |
|---|---|
| **Persistence** | **Yes** -- full message/file preserved during quarantine; eventual deletion after grace period |
| **Reactivation** | **Yes** -- release from quarantine restores full actionability |
| **Severity differentiation** | **Yes** -- different threat classifications get different quarantine treatments |
| **Proximity to 시효** | **Moderate to High**. Quarantine separates existence from actionability, supports classification-based treatment, and provides reactivation. The key difference: quarantine is a *suspicion-based* temporary hold pending review, while 시효 is a *time-based* permanent (or semi-permanent) authority expiration. Quarantine expects eventual resolution (release or delete); 시효 expects the passage of time itself to be the resolution. |

**Key insight for paper**: Quarantine introduces the concept of an "authority holding pattern" -- data exists, cannot act, awaits a determination. This maps to the 시효 concept of tolling (statute clock paused while suspect is abroad), where authority is neither active nor expired but suspended.

---

## 8. Archive Tiers in Storage (Hot/Warm/Cold/Glacier)

### 8.1 Mechanism

Cloud storage providers implement tiered accessibility:

| Tier | Access latency | Use case | Data status |
|---|---|---|---|
| **Hot** | Milliseconds | Active workloads | Fully actionable |
| **Warm/Cool** | Milliseconds (higher cost per access) | Infrequent access | Actionable with cost penalty |
| **Cold** | Milliseconds (much higher cost per access) | Rarely accessed | Actionable with significant cost penalty |
| **Archive/Glacier** | Hours (rehydration required) | Compliance/regulatory | Exists but not immediately actionable |
| **Frozen** (Elasticsearch) | Seconds-minutes (lazy fetch from S3) | Historical search | Searchable but with latency penalty |

The data is identical across tiers -- only its **accessibility** changes. Moving data to colder tiers doesn't alter it; it reduces the system's ability to retrieve and act on it quickly. Automated lifecycle policies move data between tiers based on age and access patterns.

### 8.2 Elasticsearch Frozen Tier (Notable Case)

Elasticsearch's frozen tier is particularly interesting: data lives in object storage (S3) and is searchable without manual rehydration, but queries are significantly slower. The data has not been altered or restricted -- it has been placed in a context where acting on it requires more effort. This is an **accessibility gradient**, not a binary on/off.

### Analysis

| Dimension | Assessment |
|---|---|
| **Persistence** | **Yes** -- data is identical across all tiers |
| **Reactivation** | **Yes** -- data can be promoted back to hotter tiers |
| **Severity differentiation** | **Implicit** -- different data types move through tiers at different rates based on access frequency |
| **Proximity to 시효** | **Low to Moderate**. Storage tiers modulate *accessibility cost*, not *authority*. Cold data can still be retrieved and acted upon -- it's just slower and more expensive. There is no point at which the data becomes "inactionable." The gradient is economic (cost to access), not jurisdictional (permission to act). |

**Key distinction from 시효**: Storage tiers create a **friction gradient** -- data becomes harder to act on, not impossible to act on. 시효 creates an **authority cliff** -- at expiration, action becomes categorically impossible regardless of effort. The difference between "expensive to prosecute" and "legally barred from prosecuting."

---

## 9. Certificate Revocation Lists (CRL) in PKI

(Covered in Section 2.3 above; expanded here for completeness)

### 9.1 Mechanism

When a certificate is compromised, it is added to a Certificate Revocation List. The certificate retains all its cryptographic content -- public key, subject name, issuer signature. It is not deleted or modified. What changes is its **trust status**: systems checking the CRL or querying OCSP will receive a "revoked" response and refuse to accept the certificate.

### 9.2 Hold and Reinstatement

CRL uniquely supports a **"hold" reason code** -- a certificate can be temporarily marked as invalid. If the security concern is resolved (e.g., the private key wasn't actually compromised), the hold can be lifted and the certificate reinstated to valid status. This is a reversible authority suspension.

### 9.3 Expiration vs Revocation

Certificates also have a natural expiration date (validity period). After expiry, the certificate exists but is no longer accepted. The distinction: **revocation** is event-triggered (key compromise detected), while **expiry** is time-triggered (validity period elapsed). The 시효 model encompasses both: time-based authority expiration with event-based suspension and reactivation.

### Analysis

| Dimension | Assessment |
|---|---|
| **Persistence** | **Yes** -- certificate exists unchanged in full after revocation/expiry |
| **Reactivation** | **Yes** -- "hold" status is reversible; new certificates can be issued for the same entity |
| **Severity differentiation** | **Yes** -- different certificate types (DV, OV, EV) have different validity periods and revocation handling |
| **Proximity to 시효** | **Very High**. CRL is perhaps the most structurally isomorphic pattern: the artifact (certificate/evidence) persists, its authority (trust/prosecution power) is revoked, the revocation can be temporary ("hold"/tolling) or permanent, and different severity levels get different treatment. |

---

## 10. Dead Letter Queues (DLQ) in Messaging

### 10.1 Mechanism

A dead letter queue receives messages that cannot be processed by the primary consumer. The message is preserved in full but **removed from active processing**. It cannot trigger actions in the normal workflow. Instead, it is stored separately for diagnostic analysis, manual review, or potential reprocessing.

Messages enter the DLQ when:
- Maximum delivery attempts are exceeded
- Message TTL expires
- Message is explicitly rejected by consumers
- Queue capacity is exceeded

### 10.2 Redrive / Reprocessing

AWS SQS and Azure Service Bus support **dead-letter queue redrive**: messages can be moved from the DLQ back to the source queue for reprocessing. This restores their ability to trigger actions. The decision to redrive is manual (human review determines the message should be retried).

### Analysis

| Dimension | Assessment |
|---|---|
| **Persistence** | **Yes** -- messages are fully preserved in the DLQ |
| **Reactivation** | **Yes** -- redrive moves messages back to active processing |
| **Severity differentiation** | **Partial** -- max delivery attempts can be configured per queue, but not typically per message type |
| **Proximity to 시효** | **High**. DLQ cleanly separates existence (message preserved) from actionability (removed from processing pipeline). Redrive parallels reactivation on new evidence. The key difference: DLQ placement is triggered by *processing failure*, not by *time*. A message ends up in the DLQ because something went wrong, not because a clock ran out. The 시효 model's time-based authority expiration is absent. |

**Key insight for paper**: DLQs provide the concept of a "processing purgatory" -- data exists, cannot drive action through normal channels, but remains available for extraordinary review. This maps to how evidence in a statute-expired case exists in the archive, cannot drive prosecution, but remains available for historical research or civil proceedings.

---

## 11. Bonus Patterns (Not in Original List)

### 11.1 Bitemporal Databases

Bitemporal modeling tracks two independent time dimensions:
- **Valid time**: when a fact is true in the real world
- **Transaction time**: when a fact was recorded in the system

A third dimension, **decision time**, records when a decision was made about a fact. This creates scenarios where data is factually valid but superseded by later decisions -- structurally similar to evidence that exists but whose prosecutorial authority has expired.

**Proximity to 시효**: **High**. Bitemporal databases explicitly separate "the data is true" from "the data is current/actionable." The valid-time dimension parallels the information layer; the decision-time dimension parallels the authority layer.

### 11.2 Git Reflog and Garbage Collection

When a git commit is "deleted" (e.g., via `git reset --hard`), it is not immediately removed. It persists in the **reflog** for 90 days (reachable) or 30 days (unreachable), recoverable via `git reflog` or `git fsck`. After the grace period, `git gc` permanently prunes unreachable objects.

This is a time-limited persistence window: the commit exists but is invisible to normal operations (`git log`), recoverable by explicit effort (reflog), and eventually permanently deleted. The 90/30-day distinction is a rudimentary severity-based differentiation (reachable objects get longer retention).

**Proximity to 시효**: **Moderate**. Data persists after "deletion" with a time-limited recovery window, but the endpoint is still permanent deletion, not permanent persistence with expired authority.

### 11.3 Redis Key Expiration (Lazy + Active Deletion)

Redis uses a hybrid expiration model:
- **Lazy deletion**: expired keys are only removed when accessed (checked at read time)
- **Active deletion**: a background process samples random expired keys every 100ms and deletes them

Between the key's logical expiration (TTL reached) and physical deletion (lazy/active cleanup), the data **exists but cannot be returned**. A GET on an expired key returns nil, but the data is still on disk until cleanup runs.

**Proximity to 시효**: **Low**. This is an implementation artifact of deferred cleanup, not a designed "authority expiration" pattern. The expired key has no reactivation mechanism and no severity differentiation.

### 11.4 GDPR Article 18: Right to Restriction of Processing

As distinct from Article 17 (erasure), Article 18 allows a data subject to request that their data be **retained but not processed**. The data controller must mark the data and restrict its use to storage only, legal claims, consent-based processing, or public interest.

This is structurally identical to the 시효 model: data persists, but its authority to drive processing decisions is restricted. The restriction is subject-triggered (not time-triggered), but the structural separation of data lifecycle from authority lifecycle is present.

**Proximity to 시효**: **Very High**, except for the trigger mechanism (user request vs time-based expiration).

---

## 12. Academic Literature: Adjacent Concepts

### 12.1 Information Decay vs Authority Decay

The concept of **information decay** is well-established: information loses value over time as it becomes outdated. The "half-life of knowledge" metaphor (analogous to radioactive half-life) describes how facts become obsolete at domain-specific rates (engineering knowledge decays faster than mathematical proofs).

However, information decay describes the **degradation of the data itself** (it becomes wrong or irrelevant). This is fundamentally different from **authority decay**, where the data remains accurate but its power to drive action diminishes. A murder victim's DNA profile does not decay -- the evidence is as valid in year 30 as in year 1. What decays is the legal system's authority to prosecute based on it.

**Gap identified**: No existing literature explicitly theorizes "authority decay" as distinct from "information decay." The 시효 paper would be the first to name and formalize this distinction in the context of AI memory systems.

### 12.2 Forgetting in Machine Learning (Survey Literature)

Key surveys:
- **"Forgetting in Machine Learning and Beyond"** (arXiv:2405.20620, 2024): Comprehensive survey treating forgetting as potentially adaptive rather than purely detrimental, drawing on neuroscience. Covers catastrophic forgetting, machine unlearning, and continual learning -- but all mechanisms involve **modifying or removing information from model weights**, not separating information from authority.
- **"A Comprehensive Survey of Forgetting in Deep Learning Beyond Continual Learning"** (arXiv:2307.09218, 2024): Extends forgetting analysis beyond continual learning to regularization, knowledge distillation, and transfer learning.
- **Machine unlearning failure** (ICLR 2025, "Machine Unlearning Fails to Remove Data Poisoning Attacks"): Demonstrates that approximate unlearning methods fail to remove the effects of data poisoning. Even when membership inference suggests successful unlearning, residual traces remain. Standard quantization recovers ~89% of "unlearned" knowledge. This confirms Eco's paradox as applied to ML: **intentional deletion fails because the act of removing leaves traces**.

**Critical observation**: The ML forgetting literature treats forgetting as a **data-level operation** (modify weights, remove training samples, retrain). No surveyed work proposes a **metadata-level operation** where the data is preserved but an authority/influence layer is independently managed. The 시효 model operates at this metadata level.

### 12.3 Belief Revision in AI Agent Memory

Recent work on formal belief revision for AI agents (arXiv:2603.17244, 2026) introduces versioned memory architectures where beliefs can be updated, superseded, or retracted. Temporal knowledge graphs track when facts were believed and when beliefs changed. Decay policies give old information lower retrieval priority.

This is closer to the 시효 model than ML forgetting, because beliefs are not deleted -- they are *versioned and deprioritized*. However, the decay is **gradual and continuous** (retrieval weight decreases smoothly over time), not **categorical and threshold-based** (authority is active until a date, then expired). The 시효 model introduces a binary state transition (active -> expired) rather than a continuous decay function.

### 12.4 Mayer-Schonberger's *Delete* (2009)

Viktor Mayer-Schonberger proposed **information expiration dates** -- metadata tags on digital files specifying when they should be deleted. This was the first major work arguing that digital systems need designed forgetting.

Critical differences from the 시효 model:
- Mayer-Schonberger's expiration dates trigger **deletion** (data disappears)
- 시효 expiration triggers **authority revocation** (data persists, action power disappears)
- Mayer-Schonberger's model is **user-set** (individuals choose expiration dates)
- 시효 model is **system-designed** (governance framework determines expiration by type/severity)
- *Delete* predates the LLM era (2009) -- agent memory systems didn't exist

The 시효 paper can position itself as: "Mayer-Schonberger asked the right question (how do we design digital forgetting?) but proposed the wrong mechanism (deletion). 2,500 years of legal history suggests a better one: authority expiration."

### 12.5 Tiered/Graduated Retention in Information Management

Enterprise information management widely practices **type-based retention periods** (financial records: 7 years; health records: varies by jurisdiction; employment records: 3-7 years). Microsoft Purview and similar platforms support differentiated retention labels where different content types get different retention and disposal rules.

However, this remains within the "retain then delete" paradigm. The "graduation" is in *how long* to retain, not in *what happens* at expiration. At expiration, data is deleted or archived for compliance -- not preserved with restricted authority.

**Gap identified**: No information management framework implements "retain permanently but revoke processing authority after type-specific periods." The 시효 model fills this gap.

---

## 13. Synthesis: Proximity Matrix

| Pattern | Persistence | Reactivation | Severity-based | Authority/Data Separation | Proximity |
|---|---|---|---|---|---|
| **Tombstones (DB)** | Temporary | Accidental only | No | Partial (visibility, not authority) | Moderate |
| **Token expiry (OAuth)** | Full | Yes (refresh) | Yes | **Yes** | **High** |
| **CRL / PKI** | Full | Yes (hold) | Yes | **Yes** | **Very High** |
| **Enterprise retention** | Usually no | Legal hold only | Yes | No (delete at expiry) | Low |
| **GDPR Art. 18** | Full | Yes | Partial | **Yes** | **Very High** |
| **Embargo** | Full | Automatic | Implicit | Partial (access, not authority) | Moderate |
| **Sunset clause** | Full (in record) | Yes (renewal) | Yes | **Yes** | **Very High** |
| **Cooldown** | Full | Automatic | Yes | Yes (cyclical) | Moderate |
| **Quarantine** | Full (temporary) | Yes (release) | Yes | Yes | Moderate-High |
| **Storage tiers** | Full | Yes (promotion) | Implicit | No (friction, not authority) | Low |
| **DLQ** | Full | Yes (redrive) | Partial | Yes | High |
| **Bitemporal DB** | Full | N/A (historical) | No | **Yes** (valid time vs decision time) | **High** |
| **Git reflog** | Temporary (30-90d) | Yes (checkout) | Rudimentary | Partial | Moderate |
| **Redis TTL** | Brief (deferred cleanup) | No | No | No | Low |

---

## 14. Key Arguments for the Paper

### 14.1 No Existing System Combines All Four Properties

The 시효 model requires:
1. Permanent data persistence
2. Reactivation mechanism
3. Severity-proportional authority periods
4. Explicit separation of information layer from authority layer

**No single existing CS pattern provides all four.** CRL/PKI comes closest (persistence + reactivation + severity + separation), but CRL operates at the certificate level, not as a general memory governance framework. OAuth provides excellent token/resource separation but lacks severity-proportional design. Sunset clauses provide the full pattern but exist in legislation, not in systems design.

### 14.2 The Missing Abstraction

Existing systems accidentally implement fragments of the 시효 pattern:
- Databases separate existence from visibility (tombstones)
- Security systems separate resources from access authority (tokens/CRL)
- Messaging systems separate preservation from processability (DLQ)
- Legal systems separate record persistence from binding authority (sunset clauses)
- Temporal databases separate factual validity from decision currency (bitemporal)

But no system has **named** this as a coherent design pattern, formalized its properties, or applied it to AI memory governance. The 시효 paper provides the unifying abstraction.

### 14.3 Information Decay vs Authority Decay: A Novel Distinction

The existing literature knows "information decay" (data becomes stale/wrong).
The existing literature knows "forgetting" (data is removed from weights/storage).
The existing literature does NOT have "authority decay" (data remains valid but loses its power to drive action).

This is the paper's core conceptual contribution: naming and formalizing the "authority decay" pattern that 2,500 years of legal history developed and that fragments of CS practice accidentally implement.

### 14.4 Why ML Unlearning's Failure Validates the Approach

ICLR 2025 demonstrated that machine unlearning fails: attempting to delete information from model weights leaves recoverable traces (~89% recoverable via quantization alone). This is empirical confirmation that **deletion-based forgetting doesn't work** in neural systems, just as Eco theorized it cannot work in human cognition.

The 시효 model sidesteps this failure entirely. If you don't attempt to delete information, you cannot fail at deleting it. Instead, you manage a separate authority layer -- a metadata structure that is orthogonal to the information itself and can be modified without touching the underlying data.

---

## Sources

### Database Tombstones and MVCC
- [Managing Tombstones in Apache Cassandra](https://www.instaclustr.com/support/documentation/cassandra/using-cassandra/managing-tombstones-in-cassandra/)
- [Apache Cassandra Tombstones Documentation](https://cassandra.apache.org/doc/latest/cassandra/managing/operating/compaction/tombstones.html)
- [About Deletes and Tombstones in Cassandra](https://thelastpickle.com/blog/2016/07/27/about-deletes-and-tombstones.html)
- [PostgreSQL Dead Tuples: MVCC, Autovacuum](https://skylinecodes.substack.com/p/postgresql-dead-tuples-mvcc-autovacuum)
- [Deep Dive into PostgreSQL VACUUM](https://cloud.google.com/blog/products/databases/deep-dive-into-postgresql-vacuum-garbage-collector)

### Security and Access Control
- [How to Implement Capability-Based Security](https://oneuptime.com/blog/post/2026-01-30-capability-based-security/view)
- [Token Expiration & Refresh Best Practices](https://duendesoftware.com/learn/best-practices-managing-token-expiration-refresh-revocation-in-web-apis)
- [OAuth 2.0 Token Revocation (RFC 7009)](https://datatracker.ietf.org/doc/html/rfc7009)
- [Time-Based Access Control: A Complete Guide](https://goteleport.com/learn/time-based-access-control/)
- [Certificate Revocation List (CRL) Definition](https://www.techtarget.com/searchsecurity/definition/Certificate-Revocation-List)
- [CRL vs OCSP](https://www.keyfactor.com/blog/what-is-a-certificate-revocation-list-crl-vs-ocsp/)

### Data Retention and GDPR
- [Microsoft Purview: Retention Policies & Labels](https://learn.microsoft.com/en-us/purview/retention)
- [Data Retention Policy Overview (Druva)](https://www.druva.com/glossary/what-is-a-data-retention-policy-definition-and-related-faqs)
- [GDPR Art. 17: Right to Erasure](https://gdpr-info.eu/art-17-gdpr/)
- [GDPR Right to Be Forgotten Overview](https://gdpr.eu/right-to-be-forgotten/)

### Embargo and Publishing
- [Embargo in Academic Publishing (Wikipedia)](https://en.wikipedia.org/wiki/Embargo_(academic_publishing))
- [Figshare: Embargoes and Restricted Access](https://info.figshare.com/user-guide/embargoes-and-restricted-access-publishing/)

### Sunset Clauses
- [Sunset Provision (Wikipedia)](https://en.wikipedia.org/wiki/Sunset_provision)
- [Sunset Provision (Ballotpedia)](https://ballotpedia.org/Sunset_provision)
- [Sunset Law (Britannica)](https://www.britannica.com/topic/sunset-law)

### Game Design
- [Cooldowns Can Be Used to Balance Games](https://game-design-snacks.fandom.com/wiki/Cooldowns_can_be_used_to_balance_games)
- [Design by Numbers: Cooldowns](https://rewardingplay.com/2012/01/09/design-by-numbers-cooldowns/)

### Quarantine
- [Microsoft Defender: Quarantined Email Messages](https://learn.microsoft.com/en-us/defender-office-365/quarantine-about)

### Storage Tiers
- [Azure Storage Access Tiers](https://learn.microsoft.com/en-us/azure/storage/blobs/access-tiers-overview)
- [Elasticsearch Data Tiers](https://www.elastic.co/docs/manage-data/lifecycle/data-tiers)
- [Introducing Elasticsearch Frozen Tier](https://www.elastic.co/blog/introducing-elasticsearch-frozen-tier-searchbox-on-s3)

### Dead Letter Queues
- [AWS SQS Dead Letter Queues](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/sqs-dead-letter-queues.html)
- [Dead Letter Channel (Enterprise Integration Patterns)](https://www.enterpriseintegrationpatterns.com/patterns/messaging/DeadLetterChannel.html)
- [Dead Letter Queue (AWS Explainer)](https://aws.amazon.com/what-is/dead-letter-queue/)

### Temporal Databases
- [Temporal Database (Wikipedia)](https://en.wikipedia.org/wiki/Temporal_database)
- [Bitemporality (XTDB Docs)](https://v1-docs.xtdb.com/concepts/bitemporality/)

### ML Forgetting and Unlearning
- ["Forgetting" in Machine Learning and Beyond: A Survey (arXiv:2405.20620)](https://arxiv.org/abs/2405.20620)
- [Comprehensive Survey of Forgetting in Deep Learning (arXiv:2307.09218)](https://arxiv.org/abs/2307.09218)
- [Machine Unlearning Fails to Remove Data Poisoning (ICLR 2025)](https://proceedings.iclr.cc/paper_files/paper/2025/file/7e810b2c75d69be186cadd2fe3febeab-Paper-Conference.pdf)
- [Unlearning or Obfuscating? (CMU ML Blog)](https://blog.ml.cmu.edu/2025/05/22/unlearning-or-obfuscating-jogging-the-memory-of-unlearned-llms-via-benign-relearning/)

### AI Agent Memory
- [Graph-Native Cognitive Memory for AI Agents (arXiv:2603.17244)](https://arxiv.org/html/2603.17244)
- [From Human Memory to AI Memory Survey (arXiv:2504.15965)](https://arxiv.org/html/2504.15965v2)

### Information Decay and Knowledge Half-Life
- [Data Assets: Information Decay (Analytics Magazine)](https://pubsonline.informs.org/do/10.1287/LYTX.2014.02.02/full/)
- [Half-Life of Knowledge (Simplicable)](https://simplicable.com/new/half-life-of-knowledge)
- [Half-Life of Knowledge and Strategic Human Capital (ScienceDirect)](https://www.sciencedirect.com/science/article/pii/S1053482223000426)

### Digital Forgetting
- [Mayer-Schonberger, *Delete: The Virtue of Forgetting in the Digital Age* (Princeton, 2009)](https://press.princeton.edu/books/paperback/9780691150369/delete)

### Other
- [Redis Key Expiration Internals](https://www.pankajtanwar.in/blog/how-redis-expires-keys-a-deep-dive-into-how-ttl-works-internally-in-redis)
- [Git Reflog and Data Recovery](https://git-scm.com/book/en/v2/Git-Internals-Maintenance-and-Data-Recovery)
- [LSM Tree (Wikipedia)](https://en.wikipedia.org/wiki/Log-structured_merge-tree)
