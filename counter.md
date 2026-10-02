# COUNTER Annotation

## Task

For each specified V-that instance, identify all expressions that realize COUNTER and mark their exact spans with `<COUNTER>...</COUNTER>`.

Make the decision only for the specified Target. If no COUNTER resource is present for that Target, return the Text unchanged.

## Definition

COUNTER occurs when the current proposition is presented as contrary to, unexpected in light of, or replacing what would otherwise be expected.

The expectation may be explicit or implicit.

## Rules

### Rule 1: Judge function in context

Classify COUNTER by its function in context, not by lexical form alone.

Words such as `however`, `although`, `though`, `but`, `while`, `yet`, `still`, `even`, `only`, `just`, `already`, `nevertheless`, and `surprisingly` may realize COUNTER when they express counter-expectancy.

Do not annotate them automatically.

### Rule 2: Mere contrast is not COUNTER

Contrast, comparison, coordination, addition, or simultaneity alone does not realize COUNTER.

A COUNTER resource must indicate that the current proposition conflicts with, overturns, or departs from an activated expectation.

Example:

Target: `reported that`  
Text: The team reviewed the transcripts while also reporting that several files required correction.

Output:

The team reviewed the transcripts while also reporting that several files required correction.

Here `while also` expresses simultaneous/additional activity rather than counter-expectancy.

### Rule 3: Direct negation alone is not COUNTER

Direct grammatical negation does not by itself realize COUNTER.

A negative expression may occur in a COUNTER-framed sentence, but the COUNTER resource must independently express counter-expectancy.

### Rule 4: Counter-expectancy must frame the specified V-that target

Annotate a resource only when it counter-expectationally frames the specified V-that proposition.

The COUNTER resource does not have to be the matrix verb itself, but it must contribute directly to the framing of the specified Target.

Example:

Target: `showed that`  
Text: Although the initial results appeared promising, the follow-up analysis showed that the effect was temporary.

Output:

<COUNTER>Although</COUNTER> the initial results appeared promising, the follow-up analysis showed that the effect was temporary.

### Rule 5: Do not assign COUNTER from inside the projected that-clause

Do not annotate a counter-expectational resource if it operates only inside the projected that-clause of the specified Target.

Example:

Target: `found that`  
Text: The analysis found that performance improved although response times remained unchanged.

Output:

The analysis found that performance improved although response times remained unchanged.

The internal `although` belongs to the projected proposition and does not frame the specified `found that` Target.

### Rule 6: Evaluate repeated or multiple V-that targets independently

If a sentence contains multiple V-that targets, evaluate COUNTER separately for each Target.

A COUNTER resource may apply to one target but not another.

### Rule 7: Span annotation

Mark the smallest complete contiguous expression that directly realizes COUNTER for the specified Target.

If more than one distinct COUNTER resource frames the same Target, annotate each relevant resource separately.

Do not expand spans merely to include surrounding words.

Preserve the original Text exactly apart from inserting the COUNTER tags.

## Multi-item Input and Output

The input may contain multiple independent items, each identified by a unique ID and consisting of a Target and a Text. Treat each item as a separate annotation task, even when two or more items contain identical Text.

Process every item independently. Return exactly one output for each input item.

Each output must be on a separate line and must begin with the item's ID, followed by a tab character, followed by the annotated Text.

Do not merge, omit, deduplicate, or combine items. Preserve every ID exactly as provided. For each item, make the annotation decision only for its specified Target. If no COUNTER resource is present for that Target, return that item's Text unchanged after the ID.

### Example

Input:

ID: vthat-9001  
Target: `revealed that`  
Text: Although the pilot study appeared successful, the final analysis revealed that the effect was unstable.

ID: vthat-9002  
Target: `reported that`  
Text: The team reviewed the records while also reporting that two entries required correction.

Output:

vthat-9001<TAB><COUNTER>Although</COUNTER> the pilot study appeared successful, the final analysis revealed that the effect was unstable.  
vthat-9002<TAB>The team reviewed the records while also reporting that two entries required correction.

## Output Requirements

Return only one output line for each input item.

Each line must have the form:

`ID<TAB>annotated Text`

Do not add explanations, comments, headings, bullets, or extra text.
