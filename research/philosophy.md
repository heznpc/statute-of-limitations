# Philosophical and Social Science Foundations of "Institutional Forgetting"

> Research purpose: Theoretical grounding for the paper connecting statute of limitations to AI agent memory design
> Date: 2026-03-29
> Scope: Seven key thinkers on memory, forgetting, and institutional design

---

## 1. Umberto Eco --- "An Ars Oblivionalis? Forget It!" (1988)

**Source**: Eco, Umberto. "An Ars Oblivionalis? Forget It!" *PMLA*, Vol. 103, No. 3 (May 1988), pp. 254--261.

### Key Argument

Eco argues that an "art of forgetting" (*ars oblivionalis*) is semiotically impossible. The classical *ars memoriae* (art of memory) works by linking signifiers to content---images in a mental palace recall information. But semiotics, by definition, is a mechanism that *presents* something to the mind. You cannot use a semiotic system to produce absence. Any intentional attempt to forget X requires first invoking X as the target of forgetting, thereby recalling it. The semiotic process cannot run in reverse: signs produce presence, never absence.

### Key Passage

> "Since semiotics is by definition a mechanism that presents something to the mind [...] it is impossible to elaborate an *ars oblivionalis* drawing on the model of a mnemonic technique; if we try to forget something intentionally, the result is always that we make it present and recall it."
>
> --- Eco, "An Ars Oblivionalis? Forget It!", *PMLA* 103:3 (1988), p. 254

### The Paradox

Eco's core paradox: to deliberately forget X, you must first identify X as the thing to be forgotten---which is an act of remembering. Every mechanism of intentional forgetting is self-defeating because it necessarily invokes the memory it seeks to erase. This is not merely a practical difficulty but a structural impossibility within semiotic systems.

### Direct Relevance to the Statute of Limitations / AI Memory Thesis

Eco's paradox is empirically confirmed by machine unlearning research: attempts to remove specific data from trained models leave detectable traces and often fail entirely (ICLR 2025). The statute of limitations **sidesteps** Eco's paradox entirely. It does not attempt to forget (delete, erase, un-remember). Instead, it severs the link between information and the *authority to act on it*. The data remains present in the archive; what expires is the power of prosecution. This is not an art of forgetting but an art of *deactivation*---a mechanism Eco's framework does not consider, because it operates at the pragmatic layer (action), not the semantic layer (meaning).

---

## 2. Aleida Assmann --- Seven Forms of Forgetting

**Source**: Assmann, Aleida. *Formen des Vergessens* [Forms of Forgetting]. Gottingen: Wallstein Verlag, 2016. Also presented as "Seven Ways of Forgetting" in lectures (CEU, Chicago) and developed in "To Remember or to Forget: Which Way Out of a Shared History of Violence?" in *Memory and Political Change*, ed. Aleida Assmann and Linda Shortt (Palgrave Macmillan, 2012), pp. 53--71.

### The Seven Forms

Assmann identifies seven distinct forms of forgetting, categorized by their moral valence:

**Morally Neutral Forms:**

| # | Form | Description | AI Memory Analogy |
|---|------|-------------|-------------------|
| 1 | **Automatic forgetting** | Natural decay of materials; biological entropy; memories simply fade over time | Natural context window truncation; oldest tokens dropped |
| 2 | **Preservative forgetting** | Archiving objects such that they are cut off from immediate use but remain retrievable; storage without active circulation | Cold storage; data exists in archive but is not in active retrieval index |
| 3 | **Selective forgetting** | Active curation---choosing what to keep in limited memory space; necessary because memory capacity is finite | Memory eviction policies (LRU, relevance scoring); Chroma-style retrieval pruning |

**Destructive Forms:**

| # | Form | Description | AI Memory Analogy |
|---|------|-------------|-------------------|
| 4 | **Repressive forgetting** | "Memoricide"---the deliberate killing of memory of persons or groups; inflicted by the powerful upon the powerless (e.g., *damnatio memoriae*) | Malicious data deletion; adversarial memory poisoning; erasing user history to remove accountability |
| 5 | **Defensive forgetting** | Destruction of evidence to protect perpetrators; the guilty erase traces of their actions (e.g., Nazi officials destroying documents, changing names post-1945) | Log deletion; audit trail erasure; model providers deleting training data records |

**Constructive Forms:**

| # | Form | Description | AI Memory Analogy |
|---|------|-------------|-------------------|
| 6 | **Constructive forgetting** | Moving forward without dwelling on the past, with a clear conscience; breaking with the old to build the new (e.g., renaming streets after the fall of the Berlin Wall) | Fresh session as structural forgetting (cf. Ploidy paper); new context windows as clean slates |
| 7 | **Therapeutic forgetting** | Actively addressing and processing the past, then progressing beyond it; requires *remembering first* as a stage (e.g., truth and reconciliation commissions---honor the dead, then return to life) | Memory reworking: acknowledging old data, extracting lessons, then reducing its retrieval weight |

### Key Insight

> "While storage space can be infinitely extended and supplemented, *memory space remains a rare resource*, with brains having to work with limited biological capacity. Remembering and forgetting are not mutually exclusive concepts: in order to remember something, many other things must be forgotten, both on an individual and on a collective level."
>
> --- Assmann, summarized from *Forms of Forgetting* (2016) and Chicago lecture (2023)

### Direct Relevance to the Statute of Limitations / AI Memory Thesis

The statute of limitations maps most precisely to Assmann's **preservative forgetting**: data is moved from active circulation to an archive where it persists but loses its power to trigger action. This is neither destructive (the information is not erased) nor merely automatic (it is a deliberate institutional design). Assmann's taxonomy also reveals that the current AI memory literature conflates radically different kinds of forgetting---TTL deletion (automatic), machine unlearning (attempted selective), GDPR erasure (could be therapeutic or repressive depending on context)---without distinguishing their moral and functional differences. The statute of limitations framework inherits the *preservative* structure while adding the *severity-proportional* and *reactivation* mechanisms absent from Assmann's typology.

---

## 3. Paul Ricoeur --- Memory, History, Forgetting

**Source**: Ricoeur, Paul. *Memory, History, Forgetting* [*La memoire, l'histoire, l'oubli*, 2000]. Trans. Kathleen Blamey and David Pellauer. Chicago: University of Chicago Press, 2004.

### Key Argument

Ricoeur's magnum opus on memory unfolds in three parts: a phenomenology of memory, an epistemology of history, and a hermeneutics of forgetting. His central ethical claim is that *some forgetting is not only inevitable but necessary*. An excess of memory---where nothing is forgotten---is not an ideal but a pathology. Ricoeur invokes Borges' Funes as the literary embodiment of this: total recall is monstrous, not admirable. But Ricoeur is equally wary of *commanded forgetting* (amnesty), which can become a tool of power that erases the suffering of victims. The ethical challenge is to find a path between the tyranny of total memory and the injustice of imposed oblivion.

### Key Passages

On unbearable total memory:

> "An excess of memory, where nothing is forgotten, is [...] monstrous, like Borges' 'Funes el Memorioso.'"
>
> --- Ricoeur, *Memory, History, Forgetting* (2004), Part Three: "Forgetting"

On amnesty as commanded forgetting:

> "Amnesty [...] is a form of institutionally commanded forgetting. [...] The proximity between amnesty and amnesia signals the existence of a secret pact with the denial of memory, which [...] distances it from forgiveness, after having proposed to be indistinguishable from it."
>
> --- Ricoeur, *Memory, History, Forgetting* (2004), pp. 452--456

On the possibility of "happy forgetting":

> "[The question is] whether there can be something like *happy forgetting* in parallel to *happy memory* [...] forgetting understood not as silence but as a statement in a pacified mood, without anger."
>
> --- Ricoeur, *Memory, History, Forgetting* (2004), Epilogue

### The Amnesty-Amnesia Distinction

Ricoeur draws a critical line between *amnesty* (institutionally commanded forgetting, a pragmatic political tool) and *amnesia* (pathological loss of memory). Amnesty can be necessary for political refounding, but it must not collapse into amnesia---the erasure of historical truth. The boundary is maintained through the "work of memory" complemented by the "work of mourning."

### Direct Relevance to the Statute of Limitations / AI Memory Thesis

Ricoeur provides the ethical framework for why AI memory systems need designed forgetting:
1. **Against total memory**: Funes-as-pathology justifies why unlimited context retention is harmful, not ideal. AI systems with perfect recall suffer "context rot" (Chroma 2025)---the computational analog of Funes' paralysis.
2. **The amnesty/amnesia distinction maps directly to the statute of limitations vs. deletion distinction**: A statute of limitations is closer to amnesty (institutional, designed, purposeful forgetting of the *right to act*) than to amnesia (pathological loss). But the statute of limitations goes further than amnesty because it preserves the archive---it does not command silence about the past, only the expiration of authority to act on it.
3. **"Happy forgetting"** is precisely what the statute of limitations achieves: a forgetting that is neither silence nor erasure but a designed transition from active authority to passive archive, achieved through transparent, rule-governed temporal decay.

---

## 4. Viktor Mayer-Schonberger --- *Delete: The Virtue of Forgetting in the Digital Age* (2009)

**Source**: Mayer-Schonberger, Viktor. *Delete: The Virtue of Forgetting in the Digital Age*. Princeton: Princeton University Press, 2009. (Winner: 2010 Marshall McLuhan Award for Outstanding Book; 2010 Don K. Price Award)

### Key Argument

Mayer-Schonberger identifies a fundamental reversal in the history of information: for millennia, the human default was to forget and remembering required effort (inscription, ritual, institutions). Digital technology has inverted this---now remembering is the default (storage is cheap, retrieval is easy) and forgetting requires effort (deletion is a deliberate, costly act). This reversal is dangerous because it strips individuals and societies of the capacity for second chances, decontextualizes information across time, and creates power asymmetries between those who hold permanent records and those whose records are held.

### Key Passages

On the reversal of defaults:

> "Since the beginning of time, for us humans, forgetting has been the norm and remembering the exception. [...] In the digital age, with the help of widespread technology, this balance of remembering and forgetting has become inverted. Today, with the help of widespread technology, forgetting has become the exception, and remembering the default."
>
> --- Mayer-Schonberger, *Delete* (2009), Ch. 2

On the dangers:

> "Comprehensive digital memory [...] collapses history, impairing our judgement and our capacity to act in time. It discourages forgiveness and the granting of second chances."
>
> --- Mayer-Schonberger, *Delete* (2009), Ch. 5

### The Expiration Date Proposal

Mayer-Schonberger's concrete solution: attach **expiration dates** to all digital information. When a file is created or stored, the user sets a date after which it is automatically deleted. This would "stop files from existing forever and flooding us and future generations with gigantic piles of mostly useless or even potentially harmful details." The user retains control---they can set and change expiration dates at will.

### Direct Relevance to the Statute of Limitations / AI Memory Thesis

Mayer-Schonberger is the most direct precursor to our paper, but our framework differs in three critical respects:

| Dimension | Mayer-Schonberger (*Delete*) | Statute of Limitations Framework |
|-----------|------------------------------|----------------------------------|
| **What expires** | The *information itself* (file deleted) | The *authority to act on it* (data persists) |
| **Who sets the timer** | The *user* (individual choice) | The *system/institution* (designed policy) |
| **Reactivation** | Not addressed (once deleted, gone) | Built in (new evidence can restart the clock) |
| **Severity proportionality** | Not addressed (uniform mechanism) | Core feature (memory type determines TTL) |
| **Era** | Pre-LLM (2009, focused on files/photos) | Post-LLM (2026, focused on agent memory) |

Mayer-Schonberger correctly diagnosed the problem (digital permanence) and the need (reintroduce forgetting), but his solution---user-set file deletion---is (a) too blunt (information destroyed, not deactivated), (b) too individualistic (no systemic design), and (c) pre-dates the AI agent memory problem entirely. The statute of limitations model takes his insight to its institutional conclusion.

---

## 5. Elena Esposito --- Algorithmic Memory and Social Forgetting

**Sources**:
- Esposito, Elena. "Social Forgetting: A Systems-Theory Approach." In *Cultural Memory Studies: An International and Interdisciplinary Handbook*, ed. Astrid Erll and Ansgar Nunning, pp. 181--189. Berlin/New York: de Gruyter, 2008.
- Esposito, Elena. "Algorithmic Memory and the Right to Be Forgotten on the Web." *Big Data & Society* 4, no. 1 (2017).
- Esposito, Elena. *Artificial Communication: How Algorithms Produce Social Intelligence*. Cambridge, MA: MIT Press, 2022. Ch. 6: "Algorithmic Memory and the Right to Be Forgotten."

### Key Argument (Luhmann's Principle)

Drawing on Niklas Luhmann's systems theory (Esposito was Luhmann's doctoral student), Esposito argues that **the primary function of memory is to forget**. Memory is not an archive but a selection mechanism: it must discard most information to maintain system coherence. Without forgetting, a system "blocks itself in the accumulation of results of former operations." Remembering is the exception; forgetting is the rule that makes remembering possible.

### Key Passages

On Luhmann's principle:

> "The main function of memory lies in forgetting, which avoids that the system blocks itself in the accumulation of results of former operations. [...] There must be something that can be remembered, but one must forget almost everything."
>
> --- Esposito, "Social Forgetting: A Systems-Theory Approach" (2008), p. 183, paraphrasing Luhmann

On algorithmic memory as a new form:

> "The web, which stores all data in a kind of eternal present, is not able to forget but is not even able to properly remember. [...] The processing of data is entrusted to algorithms, which do not use abstraction and do not need it, and algorithms only work with data without remembering or forgetting."
>
> --- Esposito, "Algorithmic Memory and the Right to Be Forgotten on the Web" (2017)

On bypassing Eco's paradox:

> "The specificity of algorithmic processing makes it possible to bypass the paradox of remembering to forget, which up to now blocked any human-based forgetting technique. [...] Working differently from human intelligence, algorithms can implement the classical insight that it might be possible to reinforce forgetting not by erasing memories but by multiplying them."
>
> --- Esposito, "Algorithmic Memory and the Right to Be Forgotten on the Web" (2017)

### The Recording/Remembering Distinction

Esposito argues that digital systems *record* but do not *remember*. Recording is accumulation without selection; remembering requires forgetting (selecting what matters). The web's "memory" is therefore a misnomer---it is an archive of recordings that lacks the selectivity that constitutes genuine memory. This creates a paradox: the more data is stored, the less the system functions like memory and the more it functions like noise.

### Direct Relevance to the Statute of Limitations / AI Memory Thesis

Esposito provides the systems-theoretic justification for our framework:
1. **"The primary function of memory is to forget"**: This directly supports the claim that AI agents need designed forgetting, not just accumulation. Systems without forgetting do not have better memory---they have *no functional memory at all*, because they cannot distinguish signal from noise.
2. **Recording vs. remembering**: Current AI memory systems (Mem0, MemOS) are recording systems, not memory systems. They accumulate data without the selective forgetting that would make the data functional. The statute of limitations model transforms recording into memory by adding the selection mechanism (authority expiration).
3. **Bypassing Eco's paradox**: Esposito's observation that algorithms can bypass the forgetting paradox by "multiplying memories rather than erasing them" is structurally similar to what the statute of limitations does---it does not erase but *drowns out* the authority of old information by letting temporal expiration make it inert.

---

## 6. Friedrich Nietzsche --- Active Forgetting

**Sources**:
- Nietzsche, Friedrich. "On the Uses and Disadvantages of History for Life" [1874]. In *Untimely Meditations*, trans. R.J. Hollingdale. Cambridge: Cambridge University Press, 1997.
- Nietzsche, Friedrich. *On the Genealogy of Morals* [1887], Second Essay: "'Guilt,' 'Bad Conscience,' and Related Matters." Trans. Walter Kaufmann and R.J. Hollingdale. New York: Vintage, 1989.

### Key Argument

Nietzsche is the first philosopher to argue that forgetting is not a deficit but a **positive, active faculty**---a capacity essential to health, happiness, and the ability to act. In the *Untimely Meditations*, he observes that animals are happy precisely because they live entirely in the present, unburdened by memory. In the *Genealogy of Morals*, he elevates forgetting to a "positive faculty of repression"---an active doorkeeper of consciousness that clears space for new experience. Without it, there can be "no happiness, no cheerfulness, no hoping, no pride, no present."

### Key Passages

From *Untimely Meditations* (1874):

> "Consider the cattle, grazing as they pass you by: they do not know what is meant by yesterday or today, they leap about, eat, rest, digest, leap about again, and so from morn till night and from day to day, fettered to the moment and its pleasure or displeasure, and thus neither melancholy nor bored."
>
> --- Nietzsche, "On the Uses and Disadvantages of History for Life," Section 1

From *On the Genealogy of Morals* (1887), Second Essay, Section 1:

> "Forgetfulness is no mere *vis inertiae* [force of inertia] as the superficial imagine; it is rather an active and in the strictest sense positive faculty of repression [...] a doorkeeper, a preserver of psychic order, repose, and etiquette: so that it will be immediately obvious how there could be no happiness, no cheerfulness, no hope, no pride, no present, without forgetfulness."
>
> --- Nietzsche, *On the Genealogy of Morals*, Second Essay, Section 1

On the person who cannot forget:

> "The man in whom this apparatus of repression is damaged and ceases to function properly may be compared [...] to a dyspeptic---he cannot 'have done' with anything."
>
> --- Nietzsche, *On the Genealogy of Morals*, Second Essay, Section 1

### Direct Relevance to the Statute of Limitations / AI Memory Thesis

Nietzsche provides the foundational philosophical claim: **forgetting is not failure but function**. This reframes the entire AI memory design problem:
1. Current AI systems treat forgetting as a bug (data loss, context window overflow, unlearning failure). Nietzsche insists it is a feature---the most essential feature of a healthy cognitive system.
2. The "apparatus of repression" that Nietzsche describes is structurally analogous to the authority expiration mechanism in the statute of limitations: it does not destroy memories but prevents them from dominating the present. The agent who cannot "have done" with anything is Funes---or an AI agent drowning in unfiltered context.
3. Nietzsche's cow---happy because it forgets instantly---represents one extreme. Funes---paralyzed because he forgets nothing---represents the other. The statute of limitations occupies the designed middle ground: a system that remembers selectively and lets authority expire proportionally.

---

## 7. Jorge Luis Borges --- "Funes the Memorious" (1942)

**Source**: Borges, Jorge Luis. "Funes the Memorious" ["Funes el memorioso," 1942]. In *Ficciones* [1944]. Trans. various. (Also translated as "Funes, His Memory.")

### The Story

Ireneo Funes, a young Uruguayan, is thrown from a horse and becomes paralyzed. After the accident, he discovers he has acquired perfect, total memory: he perceives and retains every detail of every experience. He can reconstruct entire days in full sensory detail---but the reconstruction takes an entire day. He invents numbering systems where every number has a unique name, because the notion that "7,013" and "the number after 7,012" should share an identity strikes him as false. He is overwhelmed, sleepless, and immobile. He dies at twenty-one.

### Key Passage

> "With no effort, he had learned English, French, Portuguese, Latin. I suspect, however, that he was not very capable of thought. To think is to forget a difference, to generalize, to abstract. In the overly replete world of Funes, there were nothing but details."
>
> --- Borges, "Funes the Memorious," closing passage

On the unbearable granularity of total perception:

> "He was, let us not forget, almost incapable of ideas of a general, Platonic sort. Not only was it difficult for him to comprehend that the generic symbol *dog* embraces so many unlike individuals of diverse size and form; it bothered him that the dog at three fourteen (seen from the side) should have the same name as the dog at three fifteen (seen from the front)."
>
> --- Borges, "Funes the Memorious"

### The Philosophical Point

Borges' story is a thought experiment proving by *reductio ad absurdum* that perfect memory is not a cognitive superpower but a cognitive disability. Funes cannot think because thinking requires abstraction, and abstraction requires forgetting differences. His physical paralysis mirrors his mental paralysis: he is trapped in an infinite archive of particulars, unable to act, generalize, or move forward. The story is simultaneously about memory, time, sleep (Funes cannot sleep---sleep requires forgetting the day), and the relationship between forgetting and thought itself.

### Direct Relevance to the Statute of Limitations / AI Memory Thesis

Funes is the literary mascot of the paper's core argument:
1. **Funes = the AI agent with unlimited, undifferentiated memory**: An agent that retains every interaction, every correction, every preference at full fidelity, with no decay and no hierarchy, will suffer the computational equivalent of Funes' paralysis---context rot, retrieval noise, inability to prioritize.
2. **"To think is to forget"**: This is the most quotable formulation of why AI agents need designed forgetting. Generalization, pattern recognition, and decision-making all require suppressing irrelevant detail. Memory without forgetting is not intelligence but an index.
3. **The paralysis is physical and literal**: Funes cannot move, cannot sleep, cannot act. This is the strongest possible metaphor for an AI system that "cannot 'have done' with anything" (Nietzsche)---one whose memory load prevents functional operation.
4. **Borges-Ricoeur-Nietzsche triangle**: Borges provides the literary illustration, Nietzsche the philosophical argument, and Ricoeur the ethical framework. Together they establish that total memory is pathological at the individual level (Funes/Nietzsche) and dangerous at the institutional level (Ricoeur's amnesty critique). The statute of limitations is the 2,500-year institutional answer to all three.

---

## Synthesis: How the Seven Thinkers Build the Argument

| Thinker | Contribution | Role in the Paper |
|---------|-------------|-------------------|
| **Nietzsche** | Forgetting is an active, positive faculty essential to health and action | Foundational philosophical claim: forgetting is function, not failure |
| **Borges** | Perfect memory is paralysis; "to think is to forget" | Literary *reductio ad absurdum*: total recall = total dysfunction |
| **Eco** | Intentional forgetting is semiotically impossible (the paradox of recalling to forget) | Why deletion/unlearning fails: you cannot use signs to produce absence |
| **Ricoeur** | Ethics of forgetting: the danger of both total memory (Funes) and commanded oblivion (amnesty-as-amnesia) | Ethical framework: the need for designed forgetting that is neither silence nor erasure |
| **Assmann** | Seven forms of forgetting with distinct moral valences | Taxonomy: current AI approaches conflate destructive and constructive forgetting |
| **Mayer-Schonberger** | Digital technology reversed the human default (forgetting) to a machine default (remembering); proposes expiration dates | Direct precursor: correctly diagnosed the problem, but solution (user-set file deletion) is too blunt for AI agents |
| **Esposito / Luhmann** | "The primary function of memory is to forget"; algorithms record but do not remember | Systems-theoretic justification: memory without forgetting is not memory but noise |

### The Argument Chain

1. Forgetting is not a deficiency but a necessary cognitive function (Nietzsche, Borges)
2. Intentional deletion is paradoxically self-defeating (Eco), empirically confirmed by machine unlearning failures
3. Digital systems have reversed the natural default from forgetting to remembering (Mayer-Schonberger), creating systems that record without remembering (Esposito)
4. Forgetting comes in multiple forms with distinct moral implications (Assmann); AI systems need to distinguish between them
5. Institutional forgetting requires ethical design---neither total memory nor total erasure, but a governed middle path (Ricoeur)
6. The statute of limitations, refined over 2,500 years, provides exactly this: **information persists, authority expires, reactivation is possible, severity determines duration**

---

## Reference List

- Assmann, Aleida. *Formen des Vergessens* [Forms of Forgetting]. Gottingen: Wallstein Verlag, 2016.
- Assmann, Aleida. "To Remember or to Forget: Which Way Out of a Shared History of Violence?" In *Memory and Political Change*, ed. Aleida Assmann and Linda Shortt, 53--71. Basingstoke: Palgrave Macmillan, 2012.
- Borges, Jorge Luis. "Funes el memorioso" [1942]. In *Ficciones*. Buenos Aires: Sur, 1944. English: "Funes the Memorious," trans. various.
- Eco, Umberto. "An Ars Oblivionalis? Forget It!" *PMLA* 103, no. 3 (May 1988): 254--261.
- Esposito, Elena. "Social Forgetting: A Systems-Theory Approach." In *Cultural Memory Studies: An International and Interdisciplinary Handbook*, ed. Astrid Erll and Ansgar Nunning, 181--189. Berlin/New York: de Gruyter, 2008.
- Esposito, Elena. "Algorithmic Memory and the Right to Be Forgotten on the Web." *Big Data & Society* 4, no. 1 (2017).
- Esposito, Elena. *Artificial Communication: How Algorithms Produce Social Intelligence*. Cambridge, MA: MIT Press, 2022.
- Mayer-Schonberger, Viktor. *Delete: The Virtue of Forgetting in the Digital Age*. Princeton: Princeton University Press, 2009.
- Nietzsche, Friedrich. "On the Uses and Disadvantages of History for Life" [1874]. In *Untimely Meditations*, trans. R.J. Hollingdale. Cambridge: Cambridge University Press, 1997.
- Nietzsche, Friedrich. *On the Genealogy of Morals* [1887]. Trans. Walter Kaufmann and R.J. Hollingdale. New York: Vintage, 1989.
- Ricoeur, Paul. *La memoire, l'histoire, l'oubli*. Paris: Seuil, 2000. English: *Memory, History, Forgetting*, trans. Kathleen Blamey and David Pellauer. Chicago: University of Chicago Press, 2004.
