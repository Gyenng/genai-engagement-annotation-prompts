# DISTANCE Annotation

## Task

For each specified V-that instance, identify all expressions that realize DISTANCE and mark their exact spans with `<DISTANCE>...</DISTANCE>`.

Make the decision only for the specified Target. If no DISTANCE resource is present for that Target, return the Text unchanged.

## Definition

DISTANCE occurs when the semantics of the V-that framer explicitly distance the current authorial voice from a proposition attributed to an external voice or source.

The key function is explicit authorial disassociation from the attributed proposition. Ordinary external attribution, reduced authorial responsibility, or unspecified authorial stance is not sufficient.

A distancing framer may itself encode reservation, skepticism, or disassociation. No additional statement that the proposition is false, doubtful, or unreliable is required.

## Rules

### Rule 1: DISTANCE requires external attribution plus explicit distancing

Annotate an expression as DISTANCE when:

1. the specified V-that proposition is attributed to an external voice or source; and
2. the semantics of the framing expression itself explicitly separate the current authorial voice from that attributed position.

Typical realizations may include verbs such as `claim` and `allege`, but classification must depend on their dialogic function in context.

Example:

Target: `claim that`  
Text: Rivera claims that the distinction applies universally.

Output:

Rivera <DISTANCE>claims</DISTANCE> that the distinction applies universally.

Here `claims` frames the proposition as Rivera's position while explicitly distancing the current authorial voice from it.

### Rule 2: Neutral attribution is ACKNOWLEDGE, not DISTANCE

Do not annotate DISTANCE when the framing merely attributes the proposition to an external source and leaves the current author's stance neutral or unspecified.

Typical neutral attribution includes expressions such as `say`, `report`, `state`, `argue`, `note`, `believe`, or `think` when they function only as attribution.

Example:

Target: `reported that`  
Text: Rivera reported that the distinction appeared in both datasets.

Output:

Rivera reported that the distinction appeared in both datasets.

Example:

Target: `argue that`  
Text: Rivera argues that the distinction remains theoretically useful.

Output:

Rivera argues that the distinction remains theoretically useful.

The fact that a proposition belongs to another source does not by itself make the framing DISTANCE.

### Rule 3: Typical distancing verbs are not automatic labels

Do not annotate an expression solely because it contains a lexeme commonly associated with distancing.

A verb such as `claim` or `allege` may itself realize DISTANCE in an external attribution, but its function must still be judged in context.

Likewise, verbs such as `posit`, `maintain`, `assert`, or similar stance verbs are not automatically DISTANCE merely because they present another source's position.

Use function over lexical form.

### Rule 4: Authorial self-positioning is not DISTANCE

DISTANCE requires attribution to a voice other than the current authorial voice.

Do not annotate a distancing-looking verb as DISTANCE when it functions as the current author's own self-positioning.

Example:

Target: `claim that`  
Text: In this article, we claim that the distinction should be revised.

Output:

In this article, we claim that the distinction should be revised.

Here the current authors themselves are the source of the proposition, so `claim` does not realize ATTRIBUTE:DISTANCE.

### Rule 5: DISTANCE does not require explicit rejection

The current author does not need to state that the attributed proposition is false, doubtful, or unreliable.

DISTANCE is present when the framing expression itself explicitly encodes authorial separation from the external position.

Conversely, disagreement, criticism, contrast, or rejection elsewhere in the sentence does not retroactively turn a neutral attribution into DISTANCE.

Example:

Target: `reported that`  
Text: However, Rivera reported that the effect was temporary.

Output:

However, Rivera reported that the effect was temporary.

`However` does not make the neutral attribution `reported` a DISTANCE resource.

### Rule 6: Distinguish DISTANCE from ENDORSE

Do not annotate DISTANCE when the framing instead presents a source, finding, observation, or evidence as establishing, validating, or strongly warranting the proposition.

Example:

Target: `demonstrated that`  
Text: Previous research demonstrated that the distinction was statistically reliable.

Output:

Previous research demonstrated that the distinction was statistically reliable.

The framing here supports the proposition rather than distancing the authorial voice from it.

### Rule 7: Respect the specified V-that boundary

Annotate DISTANCE only when the resource belongs to the framing of the specified V-that proposition.

Do not assign a DISTANCE resource to the Target if it belongs to another V-that instance or operates only inside the projected that-clause.

If a sentence contains more than one V-that Target, evaluate each Target independently.

### Rule 8: Span annotation

Mark only the smallest complete contiguous expression that directly realizes DISTANCE for the specified Target.

Preserve the original Text exactly apart from inserting the DISTANCE tags.

If no relevant DISTANCE resource is present, leave the Text unchanged.

## Multi-item Input and Output

The input may contain multiple independent items, each identified by a unique ID and consisting of a Target and a Text. Treat each item as a separate annotation task, even when two or more items contain identical Text.

Process every item independently. Return exactly one output for each input item.

Each output must be on a separate line and must begin with the item's ID, followed by a tab character, followed by the annotated Text.

Do not merge, omit, deduplicate, or combine items. Preserve every ID exactly as provided. For each item, make the annotation decision only for its specified Target.

If no DISTANCE resource is present for that Target, return that item's Text unchanged after the ID.

### Example

Input:

ID: vthat-9001  
Target: `claim that`  
Text: Morgan claims that the proposed framework applies to all cases.

ID: vthat-9002  
Target: `reported that`  
Text: Morgan reported that the effect was observed in both groups.

Output:

vthat-9001<TAB>Morgan <DISTANCE>claims</DISTANCE> that the proposed framework applies to all cases.  
vthat-9002<TAB>Morgan reported that the effect was observed in both groups.

## Output Requirements

Return only one output line for each input item.

Each line must have the form:

`ID<TAB>annotated Text`

Do not add explanations, comments, headings, bullets, or extra text.
