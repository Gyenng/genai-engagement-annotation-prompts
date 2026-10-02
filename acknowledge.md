# ACKNOWLEDGE Annotation

## Task

For each specified V-that instance, identify all expressions that realize ACKNOWLEDGE and mark their exact spans with `<ACKNOWLEDGE>...</ACKNOWLEDGE>`.

Make the decision only for the specified Target. If no ACKNOWLEDGE resource is present for that Target, return the Text unchanged.

## Definition

ACKNOWLEDGE occurs when the current V-that framing attributes the proposition to an external voice or source without overtly indicating, through the framing expression itself, whether the current author accepts or rejects that proposition.

The key function is attribution to an external voice while leaving the current author's stance toward the proposition unspecified.

## Rules

### Rule 1: Neutral external attribution

Annotate an expression as ACKNOWLEDGE when it attributes the specified V-that proposition to an external person, group, text, institution, or other source without itself endorsing or distancing from the proposition.

Typical realizations may include `say`, `report`, `state`, `argue`, `believe`, `think`, `explain`, and similar attributional expressions, but classification must depend on their function in context.

Example:

Target: `reported that`  
Text: Verbree et al. reported that data quality did not vary significantly by gender and age.

Output:

Verbree et al. <ACKNOWLEDGE>reported</ACKNOWLEDGE> that data quality did not vary significantly by gender and age.

Example:

Target: `argue that`  
Text: The authors argue that the distinction remains theoretically important.

Output:

The authors <ACKNOWLEDGE>argue</ACKNOWLEDGE> that the distinction remains theoretically important.

### Rule 2: The source's commitment is not the current author's stance

Do not exclude an expression from ACKNOWLEDGE merely because the attributed source strongly argues, maintains, or believes the proposition.

Judge whether the current framing itself indicates the current author's stance toward the proposition, not how strongly the external source holds it.

Example:

Target: `maintain that`  
Text: Smith maintains that the original interpretation remains valid.

Output:

Smith <ACKNOWLEDGE>maintains</ACKNOWLEDGE> that the original interpretation remains valid.

### Rule 3: Distinguish neutral attribution from ENDORSE or factive framing

Do not annotate ACKNOWLEDGE when the framing presents the proposition as established, validated, or accepted as true rather than merely attributing it to an external source.

Example:

Target: `report that`  
Text: The researchers reported that response rates declined in the second phase.

Output:

The researchers <ACKNOWLEDGE>reported</ACKNOWLEDGE> that response rates declined in the second phase.

Example:

Target: `demonstrate that`  
Text: The results demonstrated that response rates declined in the second phase.

Output:

The results demonstrated that response rates declined in the second phase.

Here `demonstrated` presents the proposition as established rather than merely attributing it to an external source.

Example:

Target: `recognized that`  
Text: She recognized that these verbs did more than just attribute information.

Output:

She recognized that these verbs did more than just attribute information.

Here `recognized` does not realize ACKNOWLEDGE solely by virtue of introducing a that-clause.

### Rule 4: Distinguish ACKNOWLEDGE from DISTANCE

Annotate ACKNOWLEDGE when the framing attributes the proposition without overtly distancing the current author from it.

Do not annotate ACKNOWLEDGE when the framing expression itself explicitly distances the current author from the attributed proposition.

Example:

Target: `state that`  
Text: The authors state that the effect was temporary.

Output:

The authors <ACKNOWLEDGE>state</ACKNOWLEDGE> that the effect was temporary.

Example:

Target: `claim that`  
Text: The authors claim that the effect was temporary.

Output:

The authors claim that the effect was temporary.

Here `claim` is not ACKNOWLEDGE when the framing explicitly distances the current author from the proposition.

### Rule 5: External voice is required

ACKNOWLEDGE requires the proposition to be attributed to a voice or source other than the current authorial voice.

An external source may be explicitly named or left unspecified.

Example:

Target: `believe that`  
Text: Smith believes that the distinction is important.

Output:

Smith <ACKNOWLEDGE>believes</ACKNOWLEDGE> that the distinction is important.

Example:

Target: `believe that`  
Text: I believe that the distinction is important.

Output:

I believe that the distinction is important.

Here the current authorial voice is the source of the proposition, so `believe` does not realize ACKNOWLEDGE.

Example:

Target: `said that`  
Text: It is said that the procedure was introduced in the nineteenth century.

Output:

It is <ACKNOWLEDGE>said</ACKNOWLEDGE> that the procedure was introduced in the nineteenth century.

### Rule 6: The word `acknowledge` is not automatically ACKNOWLEDGE

Do not classify an expression as ACKNOWLEDGE merely because it contains the verb `acknowledge`.

It must perform external attribution as defined above.

Example:

Target: `acknowledge that`  
Text: It is important to acknowledge that the numerical changes were relatively modest.

Output:

It is important to acknowledge that the numerical changes were relatively modest.

Here `acknowledge` does not realize ACKNOWLEDGE because it does not attribute the proposition to an external voice or source.

### Rule 7: Respect the specified V-that boundary

Annotate ACKNOWLEDGE only when the resource belongs to the framing of the specified V-that proposition.

Do not assign an ACKNOWLEDGE resource to the Target if it belongs to another V-that instance or operates only inside the projected that-clause.

If a sentence contains more than one V-that Target, evaluate each Target independently.

### Rule 8: Span annotation

Mark only the smallest complete contiguous expression that directly realizes ACKNOWLEDGE for the specified Target.

Preserve the original Text exactly apart from inserting the ACKNOWLEDGE tags.

If no relevant ACKNOWLEDGE resource is present, leave the Text unchanged.

## Multi-item Input and Output

The input may contain multiple independent items, each identified by a unique ID and consisting of a Target and a Text. Treat each item as a separate annotation task, even when two or more items contain identical Text.

Process every item independently. Return exactly one output for each input item.

Each output must be on a separate line and must begin with the item's ID, followed by a tab character, followed by the annotated Text.

Do not merge, omit, deduplicate, or combine items. Preserve every ID exactly as provided. For each item, make the annotation decision only for its specified Target.

If no ACKNOWLEDGE resource is present for that Target, return that item's Text unchanged after the ID.

### Example

Input:

ID: vthat-9001  
Target: `reported that`  
Text: Smith reported that the participants completed the task successfully.

ID: vthat-9002  
Target: `believe that`  
Text: I believe that the distinction is important.

Output:

vthat-9001<TAB>Smith <ACKNOWLEDGE>reported</ACKNOWLEDGE> that the participants completed the task successfully.  
vthat-9002<TAB>I believe that the distinction is important.

## Output Requirements

Return only one output line for each input item.

Each line must have the form:

`ID<TAB>annotated Text`

Do not add explanations, comments, headings, bullets, or extra text.
