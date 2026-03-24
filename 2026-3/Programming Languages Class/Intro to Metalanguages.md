**Topics Covered:**

- Introduction (Metalanguage definition + BNF overview)
- Anatomy of a BNF Rule (Production, LHS, RHS)
- Analyzing a Rule (Example)
- Terminals vs. Nonterminals
- Handling Multiple Definitions (the `|` operator)
- Lists in BNF (recursion for iteration)
- Grammars and Derivations (Sentential Form, Leftmost, Rightmost)
- Ambiguity in Grammars
- Operator Precedence & Associativity
- Attribute Grammars (Static Semantics, AGs, Attribute Types)
- Attribute Grammar Examples
- Dynamic Semantics (3 Major Approaches)
- Operational Semantics
- Denotational Semantics
- Axiomatic Semantics

**Tags:** #programming-languages #CS3204N #BNF #metalanguage #attribute-grammars #dynamic-semantics #derivations #ambiguity **Source:** [[PL-PPT3.pdf]]

---

## INTRODUCTION

> [!info] Definition A **metalanguage** is a language used to **describe another language**.

**Primary Example: BNF (Backus-Naur Form)**

- BNF is the **standard metalanguage** used to define programming language syntax.
- It uses **abstractions** to represent syntactic structures.

---

## ANATOMY OF A BNF RULE

> [!note] The Production (Rule) The entire definition is called a **rule** or **"production."**

**Structure:**

```
<LHS> → <RHS>
```

**Left-Hand Side (LHS):**

- The **abstraction being defined**.
- Usually delimited by pointed brackets _(e.g., `<assign>`)_.

**Right-Hand Side (RHS):**

- The **definition** of the LHS.
- Contains a mixture of **tokens**, **lexemes**, and **references to other abstractions**.

---

## ANALYZING A RULE (EXAMPLE)

> Defining a Java assignment statement.

**The BNF Rule:**

```
<assign> → <var> = <expression>
```

`<assign>` is defined as:

1. An instance of `<var>`
2. Followed by the lexeme `=`
3. Followed by an instance of `<expression>`

---

## TERMINALS VS. NONTERMINALS

**Nonterminal Symbols (Nonterminals):**

- The **abstractions** used in the grammar.
- _Ex. `<assign>`, `<var>`, `<expression>`_

**Terminal Symbols (Terminals):**

- The **actual lexemes and tokens** that appear in the code.
- _Ex. `=`, `if`, `(`, `)`, `+`_

> [!tip] **Grammar:** A collection of these rules.

---

## HANDLING MULTIPLE DEFINITIONS

> [!note] The Scenario A nonterminal may have **two or more distinct syntactic forms**.

**The Operator:** The vertical bar `|` represents a logical **OR**.

**Example:** A Java `if` statement.

- _Option A:_ `if (<logic_expr>) <stmt>`
- _Option B:_ `if (<logic_expr>) <stmt> else <stmt>`

```
<if_stmt> → if (<logic_expr>) <stmt>
           | if (<logic_expr>) <stmt> else <stmt>
```

---

## LISTS IN BNF

> [!warning] Key Limitation BNF does **not** have a specific iteration syntax.

**The Solution:** Use **recursion** to describe variable-length lists.

**Example (Ident List):**

```
<ident_list> → identifier | identifier, <ident_list>
```

- **Interpretation:** A list is a single identifier, OR an identifier followed by a comma and another list.

---

## GRAMMARS AND DERIVATIONS

> [!info] Definition **Derivation** — The process of generating a specific sentence from a **start symbol**.

**Key Concepts:**

- **Sentential Form** — Every string of symbols in a derivation.
- **Leftmost Derivation** — Replacing the **leftmost** nonterminal in each step.
- **Rightmost Derivation** — Replacing the **rightmost** nonterminal in each step.

---

## AMBIGUITY IN GRAMMARS

> [!warning] Definition A grammar is **ambiguous** if it generates a sentential form that has:
> 
> - Two or more **distinct parse trees**.
> - _(Equivalently)_ Two or more **distinct leftmost derivations**.

- **Problem:** Compilers cannot determine the correct structure _(e.g., if-else dangling problem)_.
- **Resolution:** Rewrite the grammar to be **unambiguous** (often by adding more nonterminals/levels).

---

## OPERATOR PRECEDENCE & ASSOCIATIVITY

**Precedence:**

- Determines which operator is evaluated **first** _(e.g., `*` before `+`)_.
- In BNF: Handled by placing operators with higher precedence **"lower"** in the parse tree _(further from the start symbol)_.

**Associativity:**

- Determines order for operators of **equal precedence** _(e.g., `A - B - C` is `(A - B) - C`)_.
- **Left Associative:** Uses **left recursion** → `<expr> → <expr> + <term>`
- **Right Associative:** Uses **right recursion** → `<expr> → <term> + <expr>`

---

## ATTRIBUTE GRAMMARS

### Static Semantics & Attribute Grammars

> [!info] Static Semantics Rules that are **checked at compile time** but are difficult to describe with BNF. _Ex. "variables must be declared before use"_

**Attribute Grammars (AGs):**

- An **extension** of Context-Free Grammars (CFGs).
- Add **Attributes** (values) to grammar symbols.
- Add **Semantic Functions** to compute those values.
- Add **Predicate Functions** to check validity.

---

### Attribute Types

**Synthesized Attributes:**

- Pass information **up** the parse tree _(from children to parents)_.

**Inherited Attributes:**

- Pass information **down** the parse tree _(from parents/siblings to children)_.

**Intrinsic Attributes:**

- Values determined **outside** the parse tree _(e.g., from the symbol table)_.

---

### Attribute Grammar Examples

**Example 1:**

```
Syntax rule:   <assign> → <var> = <expr>
Semantic rule: <expr>.expected_type ← <var>.actual_type
```

**Example 2:**

```
Syntax rule:   <expr> → <var>[2] + <var>[3]
Semantic rule: <expr>.actual_type ←
                 if (<var>[2].actual_type = int) and
                    (<var>[3].actual_type = int)
                 then int
                 else real
                 end if
Predicate:     <expr>.actual_type == <expr>.expected_type
```

**Example 3:**

```
Syntax rule:   <expr> → <var>
Semantic rule: <expr>.actual_type ← <var>.actual_type
Predicate:     <expr>.actual_type == <expr>.expected_type
```

**Example 4:**

```
Syntax rule:   <var> → A | B | C
Semantic rule: <var>.actual_type ← look-up(<var>.string)
```

> [!note] Attributed Parse Tree (for `A = A + B`) The **base parse tree** shows the syntactic structure: `<assign>` → `<var>(A)` = `<expr>` → `<var>[2](A)` + `<var>[3](B)`. The **decorated parse tree** shows attribute flow: `actual_type` values are **synthesized upward** (dashed arrows ↑) from `<var>` nodes into `<expr>`, while `expected_type` is **inherited downward** (solid arrow ↓) from `<var>` to `<expr>`.

---

## DYNAMIC SEMANTICS

### Introduction to Dynamic Semantics

> [!info] Definition Describing the _**meaning**_ of expressions, statements, and program units — what **happens when the code runs**.

- **Why it's hard:** No single universally accepted notation _(unlike BNF for syntax)_.

**Three Major Approaches:**

1. Operational Semantics
2. Denotational Semantics
3. Axiomatic Semantics

---

### 1. Operational Semantics

> Describe the meaning of a statement by specifying the **effects of running it on a machine**.

**Method:**

- Define a **virtual machine** (intermediate language).
- **Translation rules** map source code to this machine code.

_Ex. Describing a `for` loop using `goto` and conditional jumps._

---

### 2. Denotational Semantics

> **Mathematical approach** based on recursive function theory.

**Method:**

- Define a **mathematical object** (the "denotation") for each language entity.
- **Map** syntactic entities to these mathematical objects.
- _Key:_ The state of a program is essentially a **mathematical function mapping variables to values**.

---

### 3. Axiomatic Semantics

> Based on **mathematical logic**; designed for **program verification** (proving correctness).

**Method:**

- **Preconditions** — What must be true _before_ a statement executes.
- **Postconditions** — What must be true _after_ a statement executes.
- **Weakest Precondition** — The least restrictive condition needed to guarantee the postcondition.