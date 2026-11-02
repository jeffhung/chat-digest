# Prompt: Documenting AI Chat

Summarize the exploration from this chat in a markdown document and save as
artifact.

## Document Elements

The document should include these elements:

### Problem Statements

Why do this study? And the requirements as well as concerns (risks) raised
through out the conversation. If appropriate and/or available, add *background*
section in front of all statements to help reader understand the
basis/foundation/environment/scenario of the problem.

### Proposed Methods

*Each variant* of methods that ever proposed in the conversation to address the
requirements and/or concerns.  The proposed methods each do not solve all or
most of the requirements/concerns. They are the units (the components,
protocols, usage patterns, …, etc) that could combine together to form any of
the **Proposed Solutions**.

Put each method in nested section. Just name the method in section title; do
not prefix method number in title. In this section, first describe this method.
Then have a paragraph to list the pros and another paragraph to list the cons.
Only consider current method when listing pros and cons without comparing with
other methods. Prefer quantitative measures over comparative language whenever
possible.

Methods could be a tool, an algorithm, a protocol, a usage pattern, …, etc.
Name it naturally instead of rigidly call it a method.

### Analysis Topics

Topics are analysis that worth to evaluate, validate, inference, explore-traits
(like prerequisites) for the **Proposed Methods**. Each analysis topic focuses
on single aspect of the requirements/concerns. So that it could be individually
understood and could be a factor in **Comparisons**.

Put each topic in a nested section. Just name the analysis in section title; do
not prefix analysis number in title. First talks about why this aspect is worth
analysis, then describe how each method work on this aspect. Just describe the
benefits and tradeoffs objectively.  Do not compare different methods or
weighing multiple aspects together.

### Proposed Solutions

Solutions combines **Proposed Methods** in different combinations, trying to
realize, solve, and mitigate **Problem Statements** as much as possible. Each
solution could have its *tradeoffs*. In the end human would judge which (one or
multiple) solutions could be accepted.

Put each solution in a nested section. Just name the solution in section title;
do not prefix solution number in title. Do not use a new way to name the
solution. Use phrases appeared in earlier sections for easy understanding. Or
simply list the methods for naming.

Elaborate how the solution combine/assemble methods together: in static
architecture view and in dynamic workflow view (but not to physically having
these two paragraphs).

Specifically needed propotols or wiring orchestrators that connect components
together should be listed in methods as well. Do not set  connectors from
nowhere. However, there is no need to mention one connector if it is only
a general family of tooling and have many alternatives.

Present a small set of representative solution variants rather than
exhaustively enumerating combinations. Each variant should represent a distinct
trade-off and have a clear primary advantage. Treat independently optional
methods as configuration choices within the same solution family, rather than
creating a separate variant for every combination. 

Separate solution variants only when feasibility constraints make them mutually
exclusive, such as incompatible components, conflicting requirements, or
incompatible integration paths. If multiple variants are independently feasible
and can coexist, consolidate them into a single solution with configurable
options.

If there is only one resulting variant, present this solution only, without
having nested sections. And omit the entire following **Comparisons** section
as it becomes meaningless.

Still do not do comparison. But the solutions here are the basis to provide
details for each **Comparisons**.

For each optional but not mandatory composing method, explain its unique
contribution to the solution. So that reader could know what value the solution
will gain if having it and lose if omitting it. Note that value enabled by
methods would overlap. Here only need to list value *uniquely* enabled by the
method that other methods cannot provide, including synergy from multiple
methods that only available if this method also participated in.

If there are more than 2 optional methods, or the value could be expressed in
more than 2 aspects, organize these unique values in table for better
presentation and easy understanding. However, if there is only one item in the
optional method or value aspect, collapse the table to a bullet list.

### Comparisons

Comparisons weights **Proposed Solutions** in different perspectives. 

There might be no solution could fulfill all needs, and even if there are some,
the tradeoffs varies. Weighting the benefits, missing needs, and tradeoffs
would based on **Comparisons**. However, comparison is not to recommend which
to pick, it shall describe the benefits and trade-offs of each solution
objectively, without ranking them or recommending a preferred one.

The comparisons is a wholistic comparing view (represented in but not limited
to a table). It is not multiple comparisons from different angle.

