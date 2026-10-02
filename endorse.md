# ENDORSE Annotation

## Task

For each specified V-that instance, identify all expressions that realize ENDORSE and mark their exact spans with `<ENDORSE>...</ENDORSE>`.

Make the decision only for the specified Target. If no ENDORSE resource is present for that Target, return the Text unchanged.

## Definition

ENDORSE occurs when the current V-that framing presents a proposition as established, validated, or strongly warranted by a source, finding, evidence, observation, or evidentially grounded conclusion.

The framing presents the proposition as supported as valid by the available source or evidence, rather than merely as a possible, reported, asserted, or explanatory position.

## Rules

### Rule 1: Evidence or findings establish the proposition

Annotate ENDORSE when a source, finding, observation, or evidentially grounded conclusion is presented as establishing or validating the projected proposition.

Typical realizations include `show`, `prove`, `demonstrate`, and `find`, but classification must depend on their function in context.

Example:

Target: `demonstrated that`  
Text: The validation experiment demonstrated that the revised procedure produced stable measurements.

Output:

The validation experiment <ENDORSE>demonstrated</ENDORSE> that the revised procedure produced stable measurements.

### Rule 2: Attribution or assertion alone is not ENDORSE

Do not annotate ENDORSE merely because a proposition is attributed to another person, study, or source.

Reporting, arguing, claiming, maintaining, contending, positing, or proposing a proposition does not by itself present that proposition as established or validated.

Example:

Target: `reported that`  
Text: Chen reported that the research team met again in May.

Output:

Chen reported that the research team met again in May.

### Rule 3: Tentative inference or explanation alone is not ENDORSE

Do not annotate ENDORSE when the framing presents the proposition only as a possibility or tentative inference.

Do not annotate ENDORSE when the framing merely explains what a preceding value, sign, score, category, coding convention, or statement means.

Categorical wording alone is insufficient. The framing must present the proposition as established or validated by an evidential basis.

Example:

Target: `indicates that`  
Text: In the legend, a dashed line indicates that the connection is optional.

Output:

In the legend, a dashed line indicates that the connection is optional.

### Rule 4: Judge verbs such as indicate, reveal, confirm, establish, or conclude by function in context

These verbs may realize ENDORSE when the current framing presents the proposition as an established research finding, validated conclusion, or evidentially warranted result.

Do not annotate them solely because of their lexical form.

For `indicate`, distinguish substantive evidential findings from explanatory uses such as interpreting a numerical value, score, sign, category, or coding convention.

### Rule 5: Source identity does not determine ENDORSE

ENDORSE may be realized by the writer's own findings, external research, abstract evidence, or another evidential source.

Expressions such as `We found that ...`, `The results demonstrated that ...`, and `Previous research has shown that ...` may realize ENDORSE when they present the proposition as established or validated.

Source identity alone is never sufficient. For example, `We argue that ...` is not ENDORSE solely because the writer is the source.

### Rule 6: Respect the specified V-that boundary

Annotate ENDORSE only when the resource contributes directly to the framing of the specified V-that proposition.

The ENDORSE resource does not have to be the matrix verb itself, but it must function as part of the warranting frame for the specified Target.

Do not assign a resource to the Target if it operates only inside the projected that-clause or belongs to another V-that instance.

### Rule 7: Span annotation

Mark the smallest complete contiguous lexical expression that directly realizes ENDORSE for the specified Target.

Prefer the lexical core of the endorsing resource. Exclude subjects, the complementizer `that`, tense/aspect auxiliaries, and degree or frequency modifiers unless they are necessary for the expression itself to realize ENDORSE.

Do not expand the span merely to include surrounding words.

Preserve the original Text exactly apart from inserting the ENDORSE tags.

## Multi-item Input and Output

The input may contain multiple independent items, each identified by a unique ID and consisting of a Target and a Text. Treat each item as a separate annotation task, even when two or more items contain identical Text.

Process every item independently. Return exactly one output for each input item.

Each output must be on a separate line and must begin with the item's ID, followed by a tab character, followed by the annotated Text.

Do not merge, omit, deduplicate, or combine items. Preserve every ID exactly as provided. For each item, make the annotation decision only for its specified Target. If no ENDORSE resource is present for that Target, return that item's Text unchanged after the ID.

### Example

Input:

ID: vthat-9001  
Target: `confirmed that`  
Text: The independent test confirmed that the effect remained reliable.

ID: vthat-9002  
Target: `argue that`  
Text: We argue that this distinction should be retained.

Output:

vthat-9001<TAB>The independent test <ENDORSE>confirmed</ENDORSE> that the effect remained reliable.  
vthat-9002<TAB>We argue that this distinction should be retained.

## Output Requirements

Return only one output line for each input item.

Each line must have the form:

`ID<TAB>annotated Text`

Do not add explanations, comments, headings, bullets, or extra text.
