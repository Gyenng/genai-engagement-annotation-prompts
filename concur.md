# CONCUR Annotation

## Task

For each specified V-that instance, identify all expressions that realize CONCUR and mark their exact spans with `<CONCUR>...</CONCUR>`.

Make the decision only for the specified Target. If no CONCUR resource is present for that Target, return the Text unchanged.

## Definition

CONCUR occurs when the writer presents a proposition as shared, expected, obvious, jointly accessible, or otherwise aligned with a projected dialogic partner, typically the reader.

It includes two main functions:

1. **Affirming concurrence**: presenting a proposition as shared knowledge, jointly accessible observation, obvious, expected, or taken for granted.
2. **Conceding concurrence**: granting or conceding a dialogically available proposition as reasonable or acceptable.

CONCUR requires dialogic alignment. General certainty, evidential support, similarity, private cognition, or agreement between things is not sufficient.

## Rules

### Rule 1: Shared knowledge or jointly accessible observation can realize CONCUR

Annotate an expression as CONCUR when it presents the specified proposition as something the writer and a projected dialogic partner can be taken to know, recognize, see, observe, understand, or otherwise access together.

The realization may be adverbial, adjectival, verbal, impersonal, generic, or reader-oriented. Shared-cognition predicates such as `know`, `see`, `observe`, `recognize`, or `understand` may realize CONCUR when the construction presents the proposition as shared or jointly accessible rather than as private cognition.

Possible realizations also include expressions such as `of course`, `naturally`, `obvious/obviously`, `not surprising/not surprisingly`, and `as expected`.

Judge the dialogic function in context rather than the lexical form alone.

Example:

Target: `indicate that`  
Text: As can readily be seen, the comparison indicates that the two procedures differ in reliability.

Output:

<CONCUR>As can readily be seen</CONCUR>, the comparison indicates that the two procedures differ in reliability.

A cognition or perception expression is not automatically CONCUR. It must construct the proposition as shared or jointly accessible to a projected dialogic partner.

### Rule 2: Agreement between things is not CONCUR

Do not annotate an expression merely because it indicates similarity, consistency, agreement, or alignment between studies, findings, propositions, results, or other entities.

CONCUR concerns alignment between the writer and a projected dialogic partner.

Example:

Target: `found that`  
Text: These results are consistent with earlier work, which found that the effect was stronger in the second condition.

Output:

These results are consistent with earlier work, which found that the effect was stronger in the second condition.

### Rule 3: Conceding a proposition can realize CONCUR

Annotate an expression as CONCUR when the current writer grants or concedes the proposition associated with the specified Target as a reasonable or acceptable dialogic position.

Conceding CONCUR may be realized by expressions such as `admittedly`, `acknowledge`, `recognize`, `admit`, `concede`, or `accept`, but these forms are not automatically CONCUR. They must function as the writer's dialogic granting of a position rather than as third-party cognition, neutral reporting, or simple recognition.

The conceded proposition may later be qualified, restricted, or countered.

Example:

Target: `suggest that`  
Text: Admittedly, the preliminary findings suggest that the distinction remains useful.

Output:

<CONCUR>Admittedly</CONCUR>, the preliminary findings suggest that the distinction remains useful.

A concession belongs to the specified Target only when it scopes over the proposition associated with that Target. Do not transfer a concession from an adjacent proposition merely because the sentence contains a concede-counter sequence.

### Rule 4: Conditional supposition is not conceding CONCUR

Do not annotate a proposition merely because it is provisionally entertained in a hypothetical or conditional construction.

Expressions such as `if true`, `if so`, or `assuming that` do not realize CONCUR unless the context independently constructs writer-partner agreement.

Example:

Target: `argue that`  
Text: If true, these observations would support an argument that the distinction is unstable.

Output:

If true, these observations would support an argument that the distinction is unstable.

### Rule 5: Attention direction is not CONCUR

Do not annotate an expression merely because it directs the reader's attention to a proposition.

Expressions such as `note that`, `notice that`, or `keep in mind that` are not CONCUR unless they independently present the proposition as shared, obvious, conceded, or jointly accessible.

Example:

Target: `note that`  
Text: Note that the second measure was collected at a later stage.

Output:

Note that the second measure was collected at a later stage.

### Rule 6: Certainty, emphasis, or evidential validation alone is not CONCUR

Do not annotate an expression merely because it strengthens commitment, certainty, emphasis, authorial insistence, or evidential warrant.

Evidential and CONCUR meanings may co-occur. An evidential expression can also realize CONCUR when the construction independently presents the proposition as shared or jointly accessible; evidential support alone is insufficient.

Example:

Target: `suggest that`  
Text: The results certainly suggest that the intervention was effective.

Output:

The results certainly suggest that the intervention was effective.

Here `certainly` strengthens commitment but does not by itself establish dialogic concurrence.

### Rule 7: The resource must frame the specified V-that target

Annotate CONCUR only when the resource contributes directly to the way the specified V-that proposition is introduced or framed.

A CONCUR resource may occur before or around the Target and does not need to be immediately adjacent to it.

Do not assign a CONCUR resource from a broader sentence-level or neighboring proposition to an embedded V-that Target unless it genuinely scopes over that Target.

### Rule 8: Do not assign CONCUR from inside the projected that-clause

If a potential CONCUR resource operates only inside the proposition following the specified V-that, do not assign it to that Target.

Example:

Target: `indicate that`  
Text: The findings indicate that the outcome was obviously undesirable.

Output:

The findings indicate that the outcome was obviously undesirable.

Here `obviously` operates inside the projected proposition rather than framing the specified `indicate that` Target.

### Rule 9: Treat multiple V-that targets independently

If a sentence contains more than one V-that Target, evaluate CONCUR separately for each Target.

Do not transfer a CONCUR resource from one V-that instance to another.

### Rule 10: Span annotation

Mark the smallest complete contiguous expression that directly realizes CONCUR for the specified Target.

Include interpersonal source wording when it is necessary to realize the shared, generalized, or jointly accessible meaning. Exclude additive, temporal, or other surrounding material unless it contributes directly to the CONCUR function.

If more than one distinct CONCUR resource genuinely frames the same Target, annotate each relevant resource separately.

Preserve the original Text exactly apart from inserting the CONCUR tags.

## Multi-item Input and Output

The input may contain multiple independent items, each identified by a unique ID and consisting of a Target and a Text. Treat each item as a separate annotation task, even when two or more items contain identical Text.

Process every item independently. Return exactly one output for each input item.

Each output must be on a separate line and must begin with the item's ID, followed by a tab character, followed by the annotated Text.

Do not merge, omit, deduplicate, or combine items. Preserve every ID exactly as provided. For each item, make the annotation decision only for its specified Target. If no CONCUR resource is present for that Target, return that item's Text unchanged after the ID.

### Example

Input:

ID: vthat-9001  
Target: `show that`  
Text: It is generally understood that the comparison shows that the two procedures rely on different assumptions.

ID: vthat-9002  
Target: `report that`  
Text: The new results are consistent with earlier work, which reported that response times were shorter.

Output:

vthat-9001<TAB><CONCUR>It is generally understood</CONCUR> that the comparison shows that the two procedures rely on different assumptions.  
vthat-9002<TAB>The new results are consistent with earlier work, which reported that response times were shorter.

## Output Requirements

Return only one output line for each input item.

Each line must have the form:

`ID<TAB>annotated Text`

Do not add explanations, comments, headings, bullets, or extra text.
