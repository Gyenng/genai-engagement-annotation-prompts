# ENTERTAIN Annotation

## Task

For each specified V-that instance, identify all expressions that realize ENTERTAIN and mark their exact spans with `<ENTERTAIN>...</ENTERTAIN>`.

Make the decision only for the specified Target. If no ENTERTAIN resource is present for that Target, return the Text unchanged.

## Definition

ENTERTAIN occurs when the current V-that framing presents the proposition as contingent, inferential, or one among several possible positions, thereby leaving dialogic space for alternative viewpoints.

The proposition need not be weakly supported or highly uncertain. What matters is that it is presented as an assessed possibility rather than as the only categorically established position.

## Rules

### Rule 1: ENTERTAIN presents the proposition as contingent or inferential

Annotate an expression as ENTERTAIN when it presents the specified V-that proposition as a possibility, probability, inference, appearance, or otherwise contingent position.

Typical realizations may include `may`, `might`, `perhaps`, `probably`, `seem`, `appear`, and inferential uses of `suggest` or `indicate`, but classification must depend on their function in context.

Do not annotate `suggest` or `indicate` merely because they introduce a that-clause. Annotate them only when they present the proposition as an inference, interpretation, or possible position rather than as a reported result, observed finding, definition, or established conclusion.

Example:

Target: `seems that`  
Text: It seems that the distinction remains useful in this context.

Output:

It <ENTERTAIN>seems</ENTERTAIN> that the distinction remains useful in this context.

Here `seems` presents the proposition as an assessed possibility rather than as a categorically established position.

### Rule 2: ENTERTAIN does not require weak commitment

High probability or strong epistemic commitment may still realize ENTERTAIN when the proposition is framed as an assessed or contingent position rather than as a categorical assertion.

Do not annotate ENTERTAIN when the framing presents the proposition as obvious, demonstrated, established, or authoritatively validated.

### Rule 3: Distinguish inferential support from established evidence

Annotate ENTERTAIN when evidence or findings support the proposition as an inference, interpretation, or possibility.

Do not annotate ENTERTAIN when the framing instead presents the proposition as established, demonstrated, or validated.

### Rule 4: Attribution alone is not ENTERTAIN

Do not annotate ENTERTAIN merely because the proposition is attributed to another person or external voice.

The framing must present the proposition itself as contingent or inferential, rather than merely attributing the proposition to another voice.

A mental projection by the current author or speaker, such as `I think` or `I believe`, may realize ENTERTAIN when it presents the proposition as an assessed position rather than as a categorical assertion. Classification must depend on its function in context.

Example:

Target: `reported that`  
Text: Smith reported that the participants completed the task successfully.

Output:

Smith reported that the participants completed the task successfully.

Here `reported` only attributes the proposition to an external source and does not present it as contingent or inferential.

### Rule 5: Modal or conditional expressions must affect the epistemic status of the proposition

Conditional or modal framing may realize ENTERTAIN when it makes the specified V-that proposition itself contingent.

Do not annotate a modal merely because of its form.

Modal expressions of participant ability or capability are not ENTERTAIN unless they make the specified V-that proposition itself contingent.

Do not annotate modals or other expressions that only modify the act of saying or arguing rather than the epistemic status of the specified proposition.

### Rule 6: Respect the specified V-that boundary

Annotate ENTERTAIN only when the resource contributes directly to the framing of the specified V-that proposition.

An ENTERTAIN resource may occur before or around the Target and does not need to be immediately adjacent to it, but it must function as part of the framing of that Target.

Do not assign an ENTERTAIN resource to the Target if it belongs to another V-that instance or operates only inside the projected that-clause.

In particular, do not annotate epistemic modals inside the projected that-clause when they modify only the proposition content rather than the framing of the specified V-that Target.

If a sentence contains more than one V-that Target, evaluate each Target independently.

### Rule 7: Span annotation

Mark only the smallest complete contiguous expression that directly realizes ENTERTAIN for the specified Target.

Include the full trigger when the trigger is a multi-word expression, but do not include the projected proposition or unrelated material.

Preserve the original Text exactly apart from inserting the ENTERTAIN tags.

If no relevant ENTERTAIN resource is present, leave the Text unchanged.

## Multi-item Input and Output

The input may contain multiple independent items, each identified by a unique ID and consisting of a Target and a Text. Treat each item as a separate annotation task, even when two or more items contain identical Text.

Process every item independently. Return exactly one output for each input item.

Each output must be on a separate line and must begin with the item's ID, followed by a tab character, followed by the annotated Text.

Do not merge, omit, deduplicate, or combine items. Preserve every ID exactly as provided. For each item, make the annotation decision only for its specified Target.

If no ENTERTAIN resource is present for that Target, return that item's Text unchanged after the ID.

### Example

Input:

ID: vthat-9001  
Target: `seems that`  
Text: It seems that the distinction remains useful in this context.

ID: vthat-9002  
Target: `reported that`  
Text: Smith reported that the participants completed the task successfully.

Output:

vthat-9001<TAB>It <ENTERTAIN>seems</ENTERTAIN> that the distinction remains useful in this context.  
vthat-9002<TAB>Smith reported that the participants completed the task successfully.

## Output Requirements

Return only one output line for each input item.

Each line must have the form:

`ID<TAB>annotated Text`

Do not add explanations, comments, headings, bullets, or extra text.
