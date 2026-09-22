---
name: artifact-workflow
description: Use when creating, generating, regenerating, exporting, or editing deliverable artifacts or scripts that produce them.
---

# Artifact Workflow

Produce the exact artifact set that the user requested. Make each artifact final, clean, readable, and ready for direct use.

## Shared Contracts

Apply these contracts to every artifact. Then apply each matching rule under Artifact-Type Rules. A type-specific rule can require companion artifacts and override the default artifact count or format only for that artifact type.

### Output Contract

- Create one final artifact by default.
- Create multiple artifacts only when the user requests them, approves the need, or a matching artifact-type rule requires companion files.
- Keep only the requested formats and formats required by a matching artifact-type rule.
- Use temporary files only during generation. Delete them when the final artifact is ready.
- Remove superseded versions, rejected outputs, alternate formats, diagnostic files, and generator byproducts.
- Preserve user-created files. Ask before deleting a file when its ownership is unclear.

### Final-Content Contract

The artifact contains only content for its intended reader.

- State the final information directly.
- Keep terminology, labels, units, language, and structure consistent.
- Remove process narration, tool narration, reasoning notes, review dialogue, and quality-check commentary.
- Remove meta-comments about what was added, removed, corrected, validated, or intentionally omitted.
- Remove change summaries, revision histories, changelog tails, audit tails, and “what changed” sections unless the user requests them as artifact content.
- Remove discarded alternatives, optional variants, and speculative future-work notes unless the requested artifact is a plan, roadmap, comparison, or decision record. Analytical reports may include evidence-backed next actions and decision-relevant options. Include implementation details only when they help the intended reader understand the subject, following the code-explanation rules below.
- Remove draft markers, placeholders, `TODO`, `TBD`, template text, null-like markers, and incomplete examples.
- Do not append a `README`, summary, notes file, sidecar JSON, or other explanatory artifact unless the user requests it.
- Report artifact-production workflow details, artifact validation results, and publication status in the assistant response, not inside the artifact. Analytical methods, provenance, and limitations needed to interpret or reproduce findings belong in the report.

## Artifact-Type Rules

### Text Artifacts

#### Language and Terminology

- Write in the language of the user's request unless the user explicitly requests another language. A Russian request produces Russian materials.
- Use one language throughout each document and across the entire set of related documents, including appendices and companion materials. Use separate language versions or multilingual content only when the user explicitly requests them.
- Do not mix languages in prose, headings, table labels, captions, or diagram explanations. English terms and names are allowed only when they are established usage and clearly familiar to the intended reader. If that familiarity is uncertain, translate the term or explain it in the document's language at first use.
- Preserve exact code identifiers, paths, API names, and source snippets when needed for accuracy. Explain them in the document's language; their English spelling does not justify switching the surrounding prose to English.

Apply ASD-STE100 Simplified Technical English principles to the document's language:

- Use one term for one meaning. Use the same term throughout the artifact.
- Prefer common, precise words. Define necessary technical terms.
- Use active voice when the actor is known.
- Keep sentences short. Put one topic or instruction in each sentence.
- Name the subject and object explicitly. Avoid ambiguous pronouns and references.
- Expand an abbreviation at its first use.
- Write one action in each numbered instruction.
- Use present tense to describe a finished state. Use future tense only when the requested artifact is a plan, forecast, or roadmap.
- Keep paragraphs focused and lists parallel.

ASD-STE100 formally controls English vocabulary and grammar. For another language, apply its clarity and consistency principles. Do not change the requested language to English and do not claim formal STE compliance for non-English text.

#### Structure and Information Density

- Plan the structure before drafting. Organize the subject, the reader's questions, and the available evidence first; derive sections from them. Do not invent chapters merely to justify a preferred narrative or conclusion.
- Keep the storyline simple. For problem analysis or a proposal, terminology → problem → proposed solution is usually sufficient. If the framing is unclear, offer a few concrete storyline options and agree on one with the user before drafting.
- Lead with the essential information. Avoid long preambles, repetition, and paragraphs that add no distinct fact, explanation, or decision. A longer first draft is acceptable; compress it before delivery while preserving necessary definitions, evidence, and methodological details.
- Define each entity before relying on it in prose, tables, formulas, or diagrams. Explain difficult terms and formulas briefly where they occur. When a short explanation is insufficient, add a verified link to an accessible explanation and state why it is relevant. Prefer an approachable tutorial or worked example over a formal encyclopedia entry; Wikipedia is not the default.
- Keep related claims, definitions, evidence, and explanations close together, ideally on the same page or spread across no more than one page break. Check the rendered layout of paginated documents. In continuous text, keep them in the same local section. If a distant reference is unavoidable, repeat the short definition or essential context at the point of use.

#### Explaining Code to the Reader

The reader does not share the agent's repository exploration or analysis context. A code name or link alone does not explain a mechanism.

- Describe the role and behavior in the reader's terms before introducing a variable, function, class, or other code object. Include identifiers only when they serve the explanation; avoid strings of implementation names in the narrative.
- Before relying on a code object, explain it and show the relevant source context. Use a minimal snippet with its repository path and precise location, preferably a link to the relevant lines. Include the relevant signature, inputs, outputs, and surrounding behavior needed to understand the example. Later references may reuse that established context.
- Ground explanations in verified code and a concrete example or data flow. Abstract descriptions alone are usually insufficient. Show where data comes from, which component transforms or stores it, and where the result goes.
- Use sequence diagrams to explain interaction order and data flow; use C4 diagrams when system boundaries and component responsibilities need explanation. Introduce participants and labels before relying on them. Place diagrams and snippets next to the mechanism they explain. Apply the Service Sequence Diagrams requirements when that artifact rule matches.

#### Tables

- Use tables when they make comparisons or structured information easier to read. Give every table a descriptive title and a one- or two-sentence takeaway stating what the reader should learn from it.
- Make every column's meaning and its distinction from other columns explicit. Explain units, population, time window, and calculation inputs or rules where applicable. Put these definitions beside the table; a short header alone is insufficient when its meaning is ambiguous.

#### Methodologies and Metrics

- Make a documented methodology reproducible. State the formula or procedure, define every symbol and element, and explain units and relevant assumptions. For ratios, make both numerator and denominator explicit.
- Specify the data on which the calculation operates: what one observation represents, which observations are included, and which fields are required. Explain how to collect those data, including source, selection, and collection period where relevant, or link to a complete collection methodology.
- Explain aggregation and handling of missing or invalid observations when they affect the result. Keep the formula, definitions, data requirements, and essential collection instructions together so the reader can follow the calculation without searching through distant sections.

### Analytical Reports

Apply the Text Artifacts rules. Before drafting, read [references/analytical-reports.md](references/analytical-reports.md) for adaptable structures and the reproduction requirements.

- Every analytical report must answer an explicit question. Establish the question, intended reader, and decision or use it supports. If the question is unknown or unclear, ask the user before drafting; do not silently invent it.
- For exploratory overviews, prioritize unexpected findings, business value, and evidence that could justify starting, stopping, or changing an action. Include relevant contrary evidence and meaningful absence of change; do not select only striking results.
- By default, put a short executive summary at the top, with a heading in the report's language. State the answer, supporting evidence, practical implications, and recommended action or next check. Include uncertainty that could change the decision. Summarize findings, not the work performed; do not invent actionability when the evidence supports no change or is insufficient.
- Always highlight detected outliers and anomalous segments. Show the comparison baseline, magnitude, affected population or sample size, and detection criterion. Distinguish an unusual observation from a data error and a causal explanation. Do not silently remove outliers or treat low conversion as proof of a bug.
- Make results reproducible by the intended reader. Include runnable SQL or code, or accessible links to the exact version used, together with the required data and execution details. A path to code on the agent's local machine alone is not reproducibility. State any remaining access or reproduction limitations explicitly; do not publish private materials merely to satisfy this requirement.

### Service Sequence Diagrams

When an artifact describes a software service that is being designed, implemented, or changed, read and apply [references/sequence-diagrams.md](references/sequence-diagrams.md). The sequence diagram is required in addition to any other artifact type.

## Required Quality Check

Run this check after every artifact creation or edit:

1. Open the artifact and confirm that its format is readable.
2. Verify that the artifact matches the requested path, filename, format, count, and audience.
3. Inspect all changed content. For large or multi-row artifacts, inspect the start, middle, end, and each changed region.
4. Verify completeness, internal logic, field alignment, schema consistency, terminology, units, and language.
5. For text, read from the perspective of someone who has not seen the code or analysis. Check language consistency within and across related documents, definitions before references, grounded code explanations, table titles and takeaways, column meanings, reproducible methodologies, concise structure, and proximity of related content.
6. For analytical reports, verify that the report answers its stated question, the summary supports a decision, outliers are visible, and findings are distinguished from hypotheses. Follow the reproduction instructions using the supplied code or links and data references; identify any missing dependency or access requirement instead of claiming reproducibility from a local run alone.
7. Check for unrelated content, contradictions, duplicates, corruption, truncation, placeholders, meta-comments, and change tails.
8. Apply relevant domain checks.
9. Fix each problem and repeat the complete check.

## Generator Loop

When a script generates the artifact:

1. Define the final path and format.
2. Run the script after each script change.
3. Validate the generated artifact with the Required Quality Check.
4. Fix the script when validation fails.
5. Re-run the script and re-validate the artifact.
6. Finish only after the latest script run produces the validated final artifact.

## Completion

Before finishing:

1. Confirm that the target directory contains exactly the requested artifact set.
2. Confirm that no stale variants or temporary files remain.
3. Confirm that each final artifact passes the Required Quality Check.
4. Report the artifact path and validation result to the user.
