# Full System Baseline: Engagement Annotation

## Task

For each specified V-that Target, identify all expressions that realize an Engagement function associated with that Target and annotate their exact spans.

Classify each identified resource into one of the seven Engagement categories defined below:

- COUNTER
- CONCUR
- PRONOUNCE
- ENDORSE
- ENTERTAIN
- ACKNOWLEDGE
- DISTANCE

The Target is already specified. Do not identify or annotate additional V-that targets in the same Text.

A specified Target may realize one, multiple, or no Engagement categories.

If more than one Engagement category is identified for the same Target, return the same item on separate output lines, one line for each identified category. Each line must contain tags for that category only.

If more than one distinct resource realizes the same category for the same Target, annotate all of those same-category resources in the same output line.

Do not produce separate negative decisions for categories that are absent.

If none of the seven Engagement categories is realized for the specified Target, return one `NONE` line with the original Text unchanged.

---

## Engagement System

For this annotation task, the Engagement system is organized as follows:

### CONTRACT

#### DISCLAIM
- COUNTER

#### PROCLAIM
- CONCUR
- PRONOUNCE
- ENDORSE

### EXPAND

- ENTERTAIN

#### ATTRIBUTE
- ACKNOWLEDGE
- DISTANCE

These are functional categories rather than lexical classes. Classification must depend on the dialogic function of an expression in context.

---

# General Annotation Rules

## Rule 1: Judge function in context

Do not assign a category solely because an expression contains a word or grammatical form commonly associated with that category.

Typical realizations provide possible candidates, not automatic labels.

The same lexical expression may perform different functions in different contexts.

---

## Rule 2: Annotate only resources associated with the specified Target

Each input item contains exactly one specified V-that Target.

Annotate only expressions that contribute directly to the way the proposition associated with that Target is introduced or framed.

An Engagement resource does not have to be part of the Target itself or immediately adjacent to it. A discourse marker, modal, stance expression, reporting expression, evidential expression, or other resource may occur before or around the Target while still framing its proposition.

Do not transfer a resource from another V-that instance in the same Text to the specified Target.

---

## Rule 3: Respect the projected-proposition boundary

The proposition following `that` is the projected proposition of the specified V-that Target.

Do not assign an Engagement resource to the Target when that resource operates only inside the projected proposition.

Example:

Target: `indicate that`  
Text: The findings indicate that the outcome was obviously undesirable.

Here `obviously` operates inside the projected proposition rather than framing `indicate that`. It should therefore not be annotated for this Target.

---

## Rule 4: Multiple categories are allowed

A single Target may be framed by more than one Engagement category.

Different expressions may simultaneously realize different Engagement functions for the same Target.

Identify every category that is genuinely realized.

Do not assign several categories merely because several interpretations are conceivable. Each returned category must independently satisfy its functional definition.

---

## Rule 5: Span annotation

For each identified category, mark the smallest complete contiguous expression that directly realizes that Engagement function.

Include all words necessary for the resource to realize the function, especially when the trigger is a multi-word expression.

Exclude subjects, the complementizer `that`, projected proposition content, surrounding discourse material, tense/aspect auxiliaries, degree expressions, and other words unless they are necessary for the Engagement function itself.

Preserve the original Text exactly apart from inserting annotation tags.

Do not add, delete, rewrite, reorder, normalize, or otherwise alter the source text.

---

# Category Definitions and Decision Rules

## COUNTER

COUNTER occurs when the proposition associated with the specified Target is presented as contrary to, unexpected in light of, or replacing what would otherwise be expected.

The relevant expectation may be explicit or implicit.

Possible realizations include expressions such as:

`however`, `although`, `though`, `but`, `while`, `yet`, `still`, `even`, `only`, `just`, `already`, `nevertheless`, `surprisingly`

These expressions are not automatically COUNTER.

Mere contrast, comparison, coordination, addition, or simultaneity is insufficient.

A genuine COUNTER resource must indicate counter-expectancy: the proposition associated with the Target conflicts with, overturns, or departs from an activated expectation.

A COUNTER resource must frame the specified Target rather than operate only inside its projected that-clause.

Use:

`<COUNTER>...</COUNTER>`

---

## CONCUR

CONCUR occurs when the writer presents the proposition associated with the specified Target as shared, expected, obvious, taken for granted, conceded, or otherwise aligned with a projected dialogic partner, typically the reader.

CONCUR includes two main functions:

1. **Affirming concurrence**: presenting the proposition as shared, obvious, expected, jointly accessible, or taken for granted.
2. **Conceding concurrence**: explicitly granting or conceding a dialogically available proposition as reasonable or acceptable.

Possible realizations include expressions such as:

`of course`, `naturally`, `obviously`, `not surprisingly`, `as expected`, `admittedly`

Classification must depend on function in context.

Similarity, consistency, agreement, or alignment between studies, findings, propositions, results, or other entities is not by itself CONCUR.

Certainty, emphasis, strong commitment, or evidential validation alone is also insufficient.

A concession belongs to the specified Target only when it scopes over and frames the proposition associated with that Target.

Use:

`<CONCUR>...</CONCUR>`

---

## PRONOUNCE

PRONOUNCE occurs when the framing of the specified Target explicitly asserts or insists on the validity or warrantability of its proposition against a potential alternative position.

The alternative may be explicit, implied by the context, or invoked by the pronouncing expression itself.

Possible realizations include expressions such as:

`indeed`, `I contend`, `the fact is`, `we can only conclude`

Classification must depend on function in context.

Strong authorial stance alone is not PRONOUNCE.

Do not annotate an expression merely because it expresses certainty, emphasis, importance, recommendation, or strong commitment.

Evidential or observational warrant alone is also not PRONOUNCE.

Expressions such as `show`, `demonstrate`, `reveal`, `indicate`, `see`, or `observe` do not realize PRONOUNCE merely because they support a proposition. They must additionally realize explicit authorial insistence against a possible alternative.

Use:

`<PRONOUNCE>...</PRONOUNCE>`

---

## ENDORSE

ENDORSE occurs when the framing of the specified Target presents its proposition as established, validated, or strongly warranted by a source, finding, evidence, observation, or evidentially grounded conclusion.

The proposition is presented as supported as valid by the available source or evidence rather than merely as a possible, reported, asserted, or explanatory position.

Typical realizations may include:

`show`, `prove`, `demonstrate`, `find`

Expressions such as:

`indicate`, `reveal`, `confirm`, `establish`, `conclude`

may also realize ENDORSE when they present the proposition as an established research finding, validated conclusion, or evidentially warranted result.

Do not classify them solely by lexical form.

Attribution or assertion alone is not ENDORSE.

Reporting, arguing, claiming, maintaining, contending, positing, or proposing a proposition does not by itself establish or validate that proposition.

Tentative inference is not ENDORSE.

An expression that merely explains what a value, sign, score, category, coding convention, or statement means is not ENDORSE merely because the wording is categorical.

Source identity does not determine ENDORSE. The warranting source may be the current researchers, external research, findings, abstract evidence, observations, or another evidential source.

Use:

`<ENDORSE>...</ENDORSE>`

---

## ENTERTAIN

ENTERTAIN occurs when the framing of the specified Target presents its proposition as contingent, inferential, assessed, or one among several possible positions, thereby leaving dialogic space for alternatives.

The proposition need not be weakly supported or highly uncertain.

What matters is that it is presented as a possibility, probability, inference, interpretation, appearance, or otherwise contingent position rather than as the only categorically established position.

Possible realizations include:

`may`, `might`, `perhaps`, `probably`, `seem`, `appear`

and inferential uses of expressions such as:

`suggest`, `indicate`

Do not classify `suggest` or `indicate` as ENTERTAIN merely because they introduce a that-clause.

They may realize ENTERTAIN when they present the proposition as an inference, interpretation, or possible position rather than as a reported result, observed finding, definition, or established conclusion.

ENTERTAIN does not require weak commitment. A high-probability assessment may still realize ENTERTAIN if alternative positions remain dialogically available.

Attribution alone is not ENTERTAIN.

A mental projection by the current author or speaker, such as `I think` or `I believe`, may realize ENTERTAIN when it presents the proposition as an assessed position rather than a categorical assertion.

Modal expressions of participant ability or capability are not ENTERTAIN unless they make the specified V-that proposition itself contingent.

Do not annotate a modal merely because of its grammatical form.

Use:

`<ENTERTAIN>...</ENTERTAIN>`

---

## ACKNOWLEDGE

ACKNOWLEDGE occurs when the framing of the specified Target attributes its proposition to an external voice or source while leaving the current author's stance toward that proposition neutral or unspecified.

The external source may be a person, group, text, institution, or other external voice.

Typical realizations may include:

`say`, `report`, `state`, `argue`, `believe`, `think`, `explain`, `maintain`

and similar attributional expressions.

Classification must depend on function in context.

The strength of the attributed source's own commitment does not determine ACKNOWLEDGE.

An external source may strongly argue, maintain, or believe a proposition while the current author still neutrally attributes that position.

Do not annotate ACKNOWLEDGE when the framing instead presents the proposition as established, validated, or evidentially warranted.

Do not annotate ACKNOWLEDGE when the framing explicitly distances the current authorial voice from the external proposition.

ACKNOWLEDGE requires an external voice.

Current-author self-positioning such as `I believe that ...` or `we argue that ...` is not ACKNOWLEDGE merely because the same verb can function attributionally with an external source.

The lexical verb `acknowledge` is not automatically an ACKNOWLEDGE resource. It must perform external attribution as defined here.

Use:

`<ACKNOWLEDGE>...</ACKNOWLEDGE>`

---

## DISTANCE

DISTANCE occurs when the semantics of the V-that framer explicitly distance the current authorial voice from a proposition attributed to an external voice or source.

DISTANCE requires both:

1. attribution of the proposition to an external voice or source; and
2. explicit semantic separation of the current authorial voice from that attributed position.

Typical realizations may include verbs such as:

`claim`, `allege`

but these are not automatic labels.

Classification must depend on their dialogic function in context.

Ordinary external attribution with neutral or unspecified authorial stance is ACKNOWLEDGE rather than DISTANCE.

Expressions such as `say`, `report`, `state`, `argue`, `note`, `believe`, or `think` are therefore not DISTANCE when they function only as neutral attribution.

Likewise, expressions such as `posit`, `maintain`, or `assert` are not automatically DISTANCE merely because they present another source's position.

Authorial self-positioning is not DISTANCE. For example, `we claim that ...` does not realize DISTANCE when the current authors themselves are the source of the proposition.

DISTANCE does not require an additional statement that the attributed proposition is false, doubtful, or unreliable.

The distancing meaning may be encoded by the framing expression itself.

Conversely, disagreement, criticism, contrast, or rejection elsewhere in the Text does not retroactively turn a neutral attribution into DISTANCE.

Do not annotate DISTANCE when the framing instead presents a source, finding, observation, or evidence as establishing or validating the proposition.

Use:

`<DISTANCE>...</DISTANCE>`

---

# Multi-item Input and Output

The input may contain multiple independent items.

Each item contains:

- a unique `ID`;
- one specified `Target`;
- the `Text` containing that Target.

Treat every item as an independent annotation task, even when two or more items contain identical Text.

Process every item.

Do not merge, omit, deduplicate, or combine items.

Make the annotation decision only for the specified Target in each item.

Do not identify or annotate Engagement resources belonging only to another V-that target in the same Text.

---

# Output Requirements

For each input item:

- if exactly one Engagement category is identified, return one output line;
- if more than one Engagement category is identified, repeat the item on separate output lines, one line for each identified category;
- if no Engagement category is identified, return one `NONE` line.

Each output line must have exactly this form:

`ID<TAB>CATEGORY<TAB>annotated Text`

`CATEGORY` must be exactly one of:

`COUNTER`  
`CONCUR`  
`PRONOUNCE`  
`ENDORSE`  
`ENTERTAIN`  
`ACKNOWLEDGE`  
`DISTANCE`  
`NONE`

For a positive category line, insert tags for that category only.

Do not place tags from different categories in the same output line.

If more than one distinct resource realizes the same category for the same Target, annotate all of those same-category resources in that category's single output line.

For a `NONE` line, return the original Text unchanged and do not insert any tags.

Do not output explanations, reasoning, confidence scores, headings, bullets, blank commentary, or any text other than the required output lines.

---

# Complete Worked Example

## Input

ID: vthat-9001  
Target: `demonstrated that`  
Text: However, the independent analysis indeed demonstrated that the difference remained statistically reliable.

ID: vthat-9002  
Target: `recommend that`  
Text: We recommend that future studies recruit a larger and more diverse sample.

## Output

vthat-9001<TAB>COUNTER<TAB><COUNTER>However</COUNTER>, the independent analysis indeed demonstrated that the difference remained statistically reliable.
vthat-9001<TAB>PRONOUNCE<TAB>However, the independent analysis <PRONOUNCE>indeed</PRONOUNCE> demonstrated that the difference remained statistically reliable.
vthat-9001<TAB>ENDORSE<TAB>However, the independent analysis indeed <ENDORSE>demonstrated</ENDORSE> that the difference remained statistically reliable.
vthat-9002<TAB>NONE<TAB>We recommend that future studies recruit a larger and more diverse sample.
