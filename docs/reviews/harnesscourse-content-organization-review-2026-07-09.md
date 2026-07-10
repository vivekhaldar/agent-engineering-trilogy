# Content and organization review: harnesscourse.com

Date: 2026-07-09

Scope: intellectual argument, definitions, curriculum coverage, sequencing, reading hierarchy, labs, and capstone. Visual/interface feedback is secondary and covered separately.

## Bottom line

The page has a strong and useful thesis: engineering leverage moves outward from the instruction, to the assembled context, to the runtime that coordinates model calls over time. That is worth teaching, and the prompt -> context -> harness -> agent progression gives the field a vocabulary it currently lacks.

The largest content problem is that the page sometimes presents this pedagogical model as an ontological fact. Prompts are not "nondeterministic strings," harnesses are not necessarily deterministic programs, and `harness ⊃ context ⊃ prompt` is not a strict containment relationship across all systems or all uses of these disciplines. The page later admits definitional instability, but the foundational prose has already taught the stronger claim.

The largest organizational problem is that the document spends too much early attention on literature lineage and not enough on the actual course contract. It is an excellent annotated field map. It is not yet a fully executable three-course graduate curriculum.

## What the content gets right

### 1. The diagnostic stack is genuinely valuable

The distinction between elicitation failure, context-construction failure, and runtime/control failure is the strongest idea on the page. It gives working engineers a way to stop blaming every problem on "the prompt" or "the model."

The stack also creates a coherent curricular arc:

- Prompt: shape behavior within a call.
- Context: shape the information and affordances available to a call.
- Harness: shape trajectories across calls, tools, state, verification, and side effects.
- Agent: the model/harness composition acting in an environment.

That conceptual progression should remain the spine.

### 2. The page has an unusually healthy critical posture

It does not treat every technique as progress. It includes prompt-order sensitivity, self-correction failures, context collapse, benchmark inflation, evidence-chain failures, over-decomposition, and the possibility that stronger models reduce the value of some scaffolding.

The new trajectory-alignment material is particularly important because it prevents "harness engineering" from becoming a slogan for adding more machinery.

### 3. The Context course is the strongest of the three

Its progression is coherent and technically current:

1. foundations;
2. ICL substrate;
3. retrieval;
4. long-context failure;
5. memory representation;
6. compression;
7. tools/skills as context;
8. KV caching;
9. programmatic construction;
10. evolving playbooks;
11. production cases;
12. evaluation.

It moves from model behavior to systems consequences and gives production constraints such as caching and context rot proper weight.

### 4. The Harness course now has a credible frontier

The addition of AFlow, Meta-Harness, Self-Harness, DGM, and the partial-harness counterpoint produces a real research arc rather than a Claude Code case study followed by one paper.

The specialized-harness lab—comparing raw ReAct, partial structure, and full structure—is one of the best exercises on the page because it tests the thesis instead of assuming it.

## Priority content issues

### 1. Tighten the foundational definitions

Current claims include:

> "The harness is deterministic code with the LLM as a subroutine."

> "Prompts are nondeterministic strings."

> "The containment is strict: harness ⊃ context ⊃ prompt."

These are too strong or technically incorrect.

- A prompt is a deterministic artifact; model inference may be stochastic.
- Context may be assembled manually or programmatically and may contain far more than a "prompt."
- Harnesses can include nondeterministic retrieval, scheduling, routing, external systems, and side effects. Their value is conventional software control, not perfect determinism.
- A one-shot RAG pipeline has context engineering without an agentic harness.
- Tool schemas and system instructions simultaneously look like prompts, context, and harness configuration depending on the level of analysis.

A more defensible formulation:

> Prompts are instruction artifacts consumed by a model call. Context is the complete assembled input and state exposed to that call. A harness is the software control layer that assembles context and coordinates model calls, tools, state, verification, permissions, and termination over time. In agentic systems, these artifacts are nested at runtime, but the engineering disciplines overlap rather than forming strict ontological subsets.

Then state explicitly:

> This curriculum adopts `prompt -> context -> harness` as a model of increasing control scope, not as the only accepted taxonomy.

Likewise, introduce the agent definition as a chosen working definition:

> This curriculum uses an agent as the `(model, harness)` pair acting in an environment.

That preserves the thesis while removing the false certainty.

### 2. Compress Foundations and move the literature inventory later

Before Volume I, the page currently covers:

- motivation;
- three layers;
- context as harness subroutine;
- agent/scaffold/harness definitions;
- scaffold versus harness history;
- context-engineering lineage;
- harness-engineering lineage;
- harness optimization;
- all-three-together pieces;
- harness versus agent;
- three observations.

This is too much front matter. It repeats the nested-stack thesis several times and asks readers to process a large literature review before reaching the curriculum.

Recommended Foundations structure:

1. **The diagnostic stack** — one concise explanation plus a comparison matrix.
2. **Working definitions and contested boundaries** — state the page's model, then name serious alternatives.
3. **How to use the trilogy** — course order, prerequisites, and learning path.

Move the full lineage, terminology history, "all three together" bibliography, and detailed observations into a later **Literature and provenance** appendix. Keep only Weng and one or two framing sources in Foundations.

The comparison matrix should use:

| Layer | Primary artifact | Time horizon | Controls | Evaluation unit | Typical failure |
|---|---|---|---|---|---|
| Prompt | Instruction/example/template | One call | Elicitation | Response | Misinterpretation, format failure |
| Context | Assembled model input/state | One call or turn | Available information and affordances | Context-conditioned response | Stale, missing, diluted, poisoned context |
| Harness | Runtime/control program | Multi-step trajectory | Tools, state, permissions, verification, termination | End-to-end task | Loops, unsafe actions, brittle recovery, cost explosion |

That table would do more conceptual work than several pages of definitional prose.

### 3. Rebalance the Prompt course

The Prompt course gives three consecutive modules to Chain-of-Thought, zero-shot reasoning/decomposition, and self-consistency/ensembles. Historically that is defensible, but it overweights the 2022-2024 reasoning-prompt literature in a course whose own thesis is that hand-authored prompting is becoming less central.

Meanwhile, the course lacks a dedicated module on prompt evaluation, sensitivity, and regression testing—the discipline needed before automatic optimization can mean anything.

Recommended changes:

- Combine Chain-of-Thought and zero-shot decomposition into one historical/reasoning-pattern module.
- Keep sampling/self-consistency as a separate inference-time control module, explicitly marking its boundary with harness engineering.
- Add **Prompt Evaluation, Sensitivity, and Regression** before automatic optimization.
- Treat Multimodal Prompting as an elective/appendix unless the course will cover modality-specific evaluation deeply.
- Make Structured Output explicitly a boundary module: asking for JSON is prompting; grammar-constrained decoding is inference/harness infrastructure.
- Separate direct prompt attacks from indirect prompt injection against tool-using agents; the latter belongs primarily in Harness security.

### 4. Clarify overlaps in the Context course

The Context course is strong, but several modules duplicate other volumes:

- In-Context Learning appears in both Prompt and Context.
- Memory appears in Context Module 5 and Harness Module 5.
- DSPy/automatic construction appears in Prompt Module 10 and Context Module 9.
- Tool and skill descriptions appear as context and as harness configuration.

These overlaps are conceptually useful if the page makes the lens explicit. Each repeated topic should begin with a boundary statement:

- Prompt ICL: how examples elicit behavior.
- Context ICL: why assembled information changes inference and how position/structure affect it.
- Context memory: representation and retrieval.
- Harness memory: lifecycle, persistence, invalidation, and loading policy.
- Prompt optimization: optimize instruction artifacts.
- Context programs: optimize the function that assembles the whole window.

One missing topic deserves a full module or substantial section: **context provenance and trust**. Retrieval and memory systems need source identity, freshness, permissions, citation lineage, poisoning resistance, and conflict resolution. That is distinct from prompt injection and increasingly central to reliable agents.

### 5. Move Specialized Harness Engineering into the core

It should not be an addendum.

Specialized harness engineering is one of the page's most distinctive contributions and the practical bridge between general agent theory and real software systems. It also provides the best answer to the partial-harness research: the goal is not maximal structure, but deciding which stable responsibilities belong in code.

Recommended Harness sequence:

1. Foundations and evaluation baseline
2. Agent loop
3. Tool interfaces
4. Planning and orchestration
5. Durable execution and recovery
6. Memory and context policies
7. Verification, reflection, and inner loops
8. Security, sandboxing, and permissions
9. Human approval and escalation
10. Observability, cost, and operations
11. Specialized harness engineering
12. Harnesses as optimization targets

This also exposes the largest current omission: **durable execution and recovery**. A harness course should directly teach checkpoints, resumability, idempotency, retries, timeouts, compensation, cancellation, partial failure, and state migration. These are more central to production harness engineering than a full week on reflection.

Cost, latency, concurrency, and budget enforcement also deserve explicit treatment, even if folded into observability/operations.

### 6. Remove the leaked-source framing from the core canon

Module 12 still says the Claude Code "source exposure" made a production harness publicly readable and assigns community analyses of "the leak."

That is a weak foundation for an authoritative graduate syllabus:

- provenance and legality are awkward;
- the material may disappear;
- community reverse engineering is difficult to verify;
- it is now redundant because Weng, Meta-Harness, Self-Harness, and official harness-engineering reports support the same instructional goal.

Keep Claude Code as a product case study if useful, but use official public documentation and engineering posts. Move leak analysis to optional historical context or remove it.

### 7. Make evaluation a spine, not a final module

Each course puts evaluation near the end, but the pedagogical notes say students should watch their systems improve or regress throughout the semester. The organization should reflect that.

Week one of every course should establish:

- task set;
- baseline;
- success metric;
- variance protocol;
- cost/latency budget;
- failure taxonomy;
- run-record format.

Every subsequent lab should modify one layer and rerun the same evaluation. The final evaluation module can then cover benchmark design, validity, and evidence quality rather than introducing measurement late.

This would also solve the current lab mismatch: 37 modules but only 13 explicit labs. Not every week needs a large implementation, but every module should have an observable exercise, ablation, replication, or design critique tied to the accumulating artifact.

### 8. Turn the capstone from a second synthesis essay into an engineering brief

The capstone repeats material already taught in Foundations:

- agent = model + harness;
- scaffold versus harness;
- how the three layers compose;
- where the frontier is heading.

That repetition would be useful in a lecture, but it makes the page longer without making the capstone more executable.

Reduce the explanatory prose and specify the deliverables:

1. Working agent/harness repository.
2. Fixed baseline model and task environment.
3. Prompt, context, and harness variants with layer-by-layer ablations.
4. Held-out evaluation set.
5. Pass^k, cost, latency, safety, and traceability results.
6. Failure ledger including negative results.
7. Trace/source/code/metric evidence chain.
8. Demo and technical paper.

The current sentence "The paper is the trilogy's exit exam" is elegant, but an engineering trilogy should require the system and evidence package as well as the paper.

## Reading-list organization

The annotations are useful, but "Canonical readings" has become too inclusive. Use three tiers:

- **Core** — one or two readings every student must read.
- **Counterpoint or replication** — one reading that complicates the core claim.
- **Further reading** — optional depth.

Repeated sources across courses should be explicitly labeled "Revisit through the X lens." The page does this sometimes; make it systematic.

Add source type and status:

- peer reviewed;
- preprint;
- official engineering report;
- documentation;
- practitioner synthesis.

Replace time-relative prose such as "six months old" with absolute dates. Replace claims such as "put the term in everyone's mouth" with factual descriptions of influence. Use "recommended entry point" where "single best" is editorial judgment.

## A cleaner top-level organization

Recommended page structure:

1. **Hero and stack diagram**
2. **How to use this curriculum**
3. **Foundations**
   - diagnostic stack
   - comparison matrix
   - working definitions and alternatives
4. **Volume I: Prompt Engineering**
   - course contract
   - modules
   - final artifact
5. **Volume II: Context Engineering**
   - course contract
   - modules
   - final artifact
6. **Volume III: Harness Engineering**
   - course contract
   - modules
   - final artifact
7. **Capstone engineering brief and rubric**
8. **Literature, terminology history, and provenance appendix**

This keeps the thesis upfront, lets learners reach the curriculum sooner, and preserves the valuable literature work without making it the entrance fee.

## Recommended content changes before publishing

In order:

1. Correct the determinism and strict-containment language.
2. Promote Specialized Harness Engineering into Module 11 and add durable execution/recovery.
3. Introduce evaluation at the start of every course and make exercises cumulative.
4. Rebalance the Prompt course around evaluation rather than three weeks of reasoning prompts.
5. Add provenance/trust to Context Engineering.
6. Convert the capstone into a concrete engineering deliverable and rubric.
7. Move most of the literature lineage to an appendix and tier the readings.
8. Remove leaked-source analysis from the core reading list.

## Final assessment

The page is not suffering from a weak idea. It is suffering from an excess of material around a strong idea and from a few definitions that are more rhetorically clean than technically defensible.

The right revision is subtraction plus curricular hardening:

- fewer repeated explanations;
- more precise boundaries;
- stronger missing engineering topics;
- evaluation from day one;
- executable course and capstone contracts;
- a smaller, clearer core canon.

With those changes, the trilogy would teach more than a vocabulary. It would teach a method for building and evaluating AI systems across three layers of control.
