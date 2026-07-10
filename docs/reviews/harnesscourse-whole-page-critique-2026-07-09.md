# Whole-page critique: harnesscourse.com

Date: 2026-07-09

Review target: local `agent-engineering-trilogy` worktree after the Weng/harness-optimization update.

Agreed intent: an authoritative public syllabus and durable reference for AI engineers, technical educators, and engineering leaders. Desired character: rigorous, editorial, quietly distinctive. It is not primarily a conversion landing page.

## Anti-pattern verdict

**Pass. This does not look like generic AI-generated interface work.**

The page avoids the common fingerprints: no dark neon palette, no purple-blue gradients, no glass cards, no fake product metrics, no giant CTA, no icon-card grid, and no decorative technical illustration. The warm paper background, serif-led typography, restrained rules, small sans-serif metadata, and volume-specific colors form a coherent editorial system.

The one AI-adjacent tell is structural rather than visual: exhaustive uniformity. Thirty-seven modules repeat the same heading -> framing -> canonical readings -> occasional lab pattern. The taxonomy is so complete and evenly formatted that the middle of the page can feel generated even though the argument and source selection feel authored.

## Overall impression

This is already a strong intellectual artifact and a credible statement of a distinctive thesis. The prompt -> context -> harness -> agent progression is memorable, useful, and better than the usual undifferentiated "agents" curriculum. The page feels like an independent technical monograph rather than marketing.

Its biggest opportunity is not to add more material. It is to make the existing material more usable as a curriculum and more navigable as a reference. At 12,831 words, 37 modules, 234 external links, and 153 unique external destinations, the page needs stronger re-entry, prioritization, and source-status mechanisms.

## What is working

### 1. The central argument is clear and genuinely useful

The stack diagram and opening thesis give readers a diagnostic model: prompt failures, context-construction failures, and runtime-control failures are different classes of problem. That idea holds the entire artifact together and distinguishes it from a bibliography assembled around fashionable terms.

The scaffold-versus-harness discussion and the new optimization ladder strengthen the argument by showing how the locus of engineering moves outward as systems become more capable.

### 2. The editorial design supports authority

The Iowan/Charter/Georgia serif stack, warm tinted background, 72-character reading measure, restrained sans-serif interface labels, and muted course colors feel deliberate. On a wide desktop, the 280-pixel sticky table of contents and approximately 681-pixel paragraph measure make long-form reading comfortable.

Color communicates course identity rather than decorating the page. The prompt, context, harness, and capstone accents are restrained and maintain meaning even without saturated UI chrome.

### 3. The source curation has a point of view

The annotations usually explain why a reading belongs, not merely what it is. The page includes counterarguments and negative results: prompt techniques aging out, self-correction limitations, benchmark rigor, partial harnessing, evidence-chain failures, and the possibility that excessive structure hurts performance. That critical posture creates more trust than a triumphalist list of agent papers would.

### 4. The implementation is admirably small

The site is one self-contained HTML file of roughly 155 KB with no framework, package manager, third-party scripts, remote fonts, or render-blocking assets. It is fast, directly printable, and easy to preserve. The internal anchors all resolve, and the active table-of-contents link correctly receives `aria-current="location"`.

## Priority issues

### 1. Mobile navigation blocks access to the document

**What:** Below 900 pixels, the complete table of contents becomes a static block above the page. At a 390 x 844 viewport it is 1,469 pixels tall, contains 47 links, and pushes the beginning of `<main>` almost two screens down. The total document grows to roughly 76,000 vertical pixels because of wrapping.

**Why it matters:** The audience will often open this from a social post, email, or saved link on a phone. Their first experience is not the thesis; it is a long navigation inventory. This is the clearest actual UX failure on the page.

**Fix:** On narrow screens, replace the full TOC with a compact sticky "Contents" control. Initially expose only Foundations / Prompt / Context / Harness / Capstone. Put module-level links inside expandable course groups. Opening a deep anchor should keep the TOC collapsed and show the content immediately.

**Command:** `/adapt`

### 2. It calls itself a graduate curriculum but is still mostly an annotated bibliography

**What:** The page declares three one-semester graduate courses and says each module is paced as lecture / paper / lab. There are 37 modules but only 13 visible labs: four in Prompt, three in Context, and six in Harness. There are no explicit course-level learning outcomes, prerequisites, workload expectations, assessment weights, project milestones, grading rubrics, or instructor-facing teaching notes.

**Why it matters:** For a reader using this as a reference, the current form is excellent. For an educator trying to teach it—or a learner trying to complete it—the curriculum promise is overstated. The missing contract makes it difficult to distinguish a serious executable syllabus from a very strong reading map.

**Fix:** Add a compact course contract before each volume:

- prerequisites;
- 4-6 measurable learning outcomes;
- expected weekly workload;
- assessment model;
- semester-long artifact;
- lab cadence and final deliverable.

Either add a lab or exercise for every module, or change the hero's pacing claim so it accurately describes the selective lab cadence. Do not pad the page with weak exercises merely to hit 36 labs.

**Command:** `/clarify`

### 3. Re-entry and prioritization are too weak for a 12,831-word reference

**What:** Nearly every module has the same visual and semantic weight. "Canonical readings" lists routinely contain several papers plus long annotations. The desktop TOC helps, but its scroll height is about 1,826 pixels inside a 1,000-pixel viewport; on smaller desktop windows it becomes the mobile-style preamble. There is no "How to use this" entry point, no self-study versus teaching path, no required/optional split, and no way to see the minimum viable reading sequence.

**Why it matters:** A durable reference succeeds when readers can return six weeks later and find the right depth quickly. Currently the page is excellent for linear close reading but inefficient for task-oriented lookup.

**Fix:** Add three entry modes near the hero:

1. Understand the thesis: Foundations + one framing reading per course.
2. Self-study: 12-week path with one required reading and one exercise per week.
3. Teach it: full reading set, labs, and capstone contract.

Within every module, distinguish **Core** from **Further reading**. Keep one or two core readings expanded and move the rest into progressive disclosure. Make the four stack-diagram layers link to their course sections.

**Command:** `/distill` followed by `/onboard`

### 4. The authority language is stronger than the evidence model

**What:** The page repeatedly uses "canonical," "clearest," "single best," "first use," "dominant," and "most common" across a young and fast-moving field. Some judgments are persuasive editorial opinions; others read as historical or consensus claims without explicit support. Peer-reviewed papers, arXiv preprints, lab engineering posts, product documentation, X posts, and secondary explainers share the same citation treatment.

**Why it matters:** The page's value rests on authority and curation. Overstated consensus claims and flattened source types are the fastest way to weaken that authority—especially when many 2026 references are recent preprints.

**Fix:** Preserve the point of view but label it honestly:

- "My recommended entry point" instead of "the single best" where the claim is editorial;
- source-status chips or text labels: peer reviewed / preprint / primary engineering report / practitioner synthesis;
- visible "last reviewed" date for each course or for the whole artifact;
- a short selection policy explaining what "canonical" means here;
- an automated link-health check for the 153 unique external destinations.

**Command:** `/normalize` and `/clarify`

### 5. Accessibility is close visually but incomplete operationally

**What:** `--ink-faint` has a contrast ratio of approximately 3.66:1 against the page background, below WCAG AA for the 10-13 pixel metadata and TOC numerals that use it. There are hover states but no explicit `:focus-visible` styles, no skip link, and smooth scrolling does not honor `prefers-reduced-motion`. The mobile TOC compounds the keyboard and screen-reader navigation burden.

**Why it matters:** This is a reading-intensive reference with hundreds of links. Keyboard navigation and visible focus are not edge cases; they are core interaction states.

**Fix:** Darken `--ink-faint`, add a skip-to-content link, provide consistent focus-visible outlines, wrap smooth scrolling in a reduced-motion media query, and use a semantic `<nav>` for the table of contents. Preserve the existing `aria-current` behavior.

**Command:** `/audit` then `/harden`

### 6. It needs visible versioning and publishing metadata

**What:** The field changes rapidly, but the page has no visible last-updated date, version, or maintenance promise. The document also lacks a meta description, Open Graph/Twitter metadata, favicon, and structured-data description. Separately, the live domain still fails HTTPS hostname validation because GitHub Pages serves a generic `*.github.io` certificate.

**Why it matters:** A reference full of current readings needs temporal provenance. Social previews and search results are how many readers will first encounter it. The HTTPS failure is a hard publishing blocker.

**Fix:** Add a visible "Last reviewed" line with a source-commit link, basic social/search metadata, and a lightweight maintenance note. Resolve GitHub Pages certificate provisioning before promoting the site.

**Command:** `/harden`

## Minor observations

- The system-only serif stack is fast and appropriate, but Windows/Linux readers may receive a materially different Georgia rendering. Check line measure and heading wraps in that fallback rather than adding a web font automatically.
- The stack diagram is the page's best visual. Make it a semantic figure and navigation device. One additional comparison table—artifact, failure layer, evaluation unit, and optimization target across prompt/context/harness—would earn its space. More decorative diagrams would not.
- Opening all 234 external links in new tabs is defensible for a research reference but can produce tab sprawl. Consider leaving stable scholarly links in the current tab or documenting the behavior visually.
- Print output is useful but currently long: roughly 56 letter-sized pages. Printing raw URLs after every citation increases noise and causes awkward wrapping. A print-only numbered bibliography would be cleaner.
- "The completing volume of the trilogy" in the Prompt course lede sounds like project-history residue. Readers encounter Prompt first; describe its intellectual role, not the order in which the author finished the material.
- The capstone is conceptually strong, but it needs an assessment rubric. The current deliverable asks the right questions without saying what excellent evidence looks like.
- The page should not acquire a large JavaScript search framework. A small client-side title/reading filter would be enough if re-entry remains difficult after navigation is fixed.

## Questions worth resolving

1. Is this ultimately a syllabus someone can teach unchanged, or an opinionated curriculum map from which instructors build a syllabus? The current page claims the former and delivers the latter.
2. What is the maintenance boundary? Will new papers accumulate indefinitely, or will each module preserve one stable core plus a small rotating frontier list?
3. Should a self-directed learner be able to complete the trilogy, or is instructor mediation assumed? That decision determines how much scaffolding the labs and assessments need.
4. What would you remove if the page could contain only 60% of its current readings? The answer would reveal the true canon more clearly than another round of additions.

## Bottom line

Do not redesign the aesthetic. It passes the AI-slop test and already expresses the agreed brand better than a more polished SaaS treatment would.

Before a serious public push, I would do three things in this order:

1. fix the mobile TOC;
2. make the curriculum contract honest and executable;
3. add source status, versioning, accessibility states, and HTTPS.

After those, the page would be more than a compelling bibliography. It would be a credible, usable public syllabus with a distinct intellectual position.
