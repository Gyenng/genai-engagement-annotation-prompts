# PRONOUNCE Annotation

## Task

For each specified V-that instance, identify all expressions that realize PRONOUNCE and mark their exact spans with `<PRONOUNCE>...</PRONOUNCE>`.

Make the decision only for the specified Target. If no PRONOUNCE resource is present for that Target, return the Text unchanged.

## Definition

PRONOUNCE occurs when the current V-that framing explicitly asserts or insists on the validity or warrantability of a proposition against a potential alternative position.

The alternative may be explicit, implied by the context, or invoked by the pronouncing expression itself.

## Rules

### Rule 1: Explicit authorial insistence

Annotate an expression as PRONOUNCE when the current V-that framing explicitly reinforces the proposition as valid in the face of possible doubt, challenge, or a competing position.

Typical realizations may include `I contend that`, `the fact is that`, `indeed`, and `we can only conclude that`, but classification must depend on their function in context.

Example:

Target: `contend that`  
Text: I contend that this interpretation provides a better explanation of the evidence.

Output:

I <PRONOUNCE>contend</PRONOUNCE> that this interpretation provides a better explanation of the evidence.

Example:

Target: `demonstrate that`  
Text: However, the evidence indeed demonstrates that the distinction remains important.

Output:

However, the evidence <PRONOUNCE>indeed</PRONOUNCE> demonstrates that the distinction remains important.

### Rule 2: Strong authorial stance alone is not PRONOUNCE

Do not annotate PRONOUNCE merely because an expression shows certainty, emphasis, importance, or recommendation.

PRONOUNCE requires explicit insistence on the validity or warrantability of the proposition against a potential alternative, not simply a strong or explicit authorial stance.

Example:

Target: `noting that`  
Text: It is worth noting that the sample primarily consisted of teachers.

Output:

It is worth noting that the sample primarily consisted of teachers.

Example:

Target: `believe that`  
Text: I am firmly convinced that the explanation is correct.

Output:

I am firmly convinced that the explanation is correct.

Example:

Target: `recommend that`  
Text: We recommend that researchers interact with participants before the survey.

Output:

We recommend that researchers interact with participants before the survey.

### Rule 3: Evidential or observational warrant alone is not PRONOUNCE

Do not annotate PRONOUNCE merely because evidence, findings, research, or observation supports the proposition.

Expressions such as `show that`, `demonstrate that`, `reveal that`, `indicate that`, or `we can see/observe that` are not PRONOUNCE unless they additionally realize explicit authorial insistence against an alternative position.

Example:

Target: `demonstrate that`  
Text: The results demonstrate that the intervention improved performance.

Output:

The results demonstrate that the intervention improved performance.

Example:

Target: `see that`  
Text: In this regard, we can see that Elena had some understanding of the concept.

Output:

In this regard, we can see that Elena had some understanding of the concept.

### Rule 4: The resource must frame the specified V-that instance

Annotate PRONOUNCE only when the resource contributes directly to the framing of the specified V-that proposition.

A PRONOUNCE resource may occur before or around the Target and does not need to be immediately adjacent to it, but it must function as part of the framing of that Target.

Example:

Target: `demonstrate that`  
Text: The evidence indeed demonstrates that the two groups differ systematically.

Output:

The evidence <PRONOUNCE>indeed</PRONOUNCE> demonstrates that the two groups differ systematically.

### Rule 5: Respect the specified V-that boundary

Do not assign a PRONOUNCE resource to the Target if it belongs to another V-that instance or operates only inside the projected that-clause.

If a sentence contains more than one V-that Target, evaluate each Target independently.

Example:

Target: `indicate that`  
Text: The findings indicate that this is indeed an important distinction.

Output:

The findings indicate that this is indeed an important distinction.

Here `indeed` occurs inside the projected that-clause and does not frame the specified `indicate that` Target.

### Rule 6: Span annotation

Mark only the smallest complete contiguous expression that directly realizes PRONOUNCE for the specified Target.

Preserve the original Text exactly apart from inserting the PRONOUNCE tags.

If no relevant PRONOUNCE resource is present, leave the Text unchanged.

## Multi-item Input and Output

The input may contain multiple independent items, each identified by a unique ID and consisting of a Target and a Text. Treat each item as a separate annotation task, even when two or more items contain identical Text.

Process every item independently. Return exactly one output for each input item.

Each output must be on a separate line and must begin with the item's ID, followed by a tab character, followed by the annotated Text.

Do not merge, omit, deduplicate, or combine items. Preserve every ID exactly as provided. For each item, make the annotation decision only for its specified Target.

If no PRONOUNCE resource is present for that Target, return that item's Text unchanged after the ID.

### Example

Input:

ID: vthat-9001  
Target: `contend that`  
Text: I contend that this interpretation provides a better explanation of the evidence.

ID: vthat-9002  
Target: `indicate that`  
Text: The findings indicate that this is indeed an important distinction.

Output:

vthat-9001<TAB>I <PRONOUNCE>contend</PRONOUNCE> that this interpretation provides a better explanation of the evidence.  
vthat-9002<TAB>The findings indicate that this is indeed an important distinction.

## Output Requirements

Return only one output line for each input item.

Each line must have the form:

`ID<TAB>annotated Text`

Do not add explanations, comments, headings, bullets, or extra text.
