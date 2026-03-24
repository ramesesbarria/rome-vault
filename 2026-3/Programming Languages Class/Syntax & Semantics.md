
**Topics Covered:**

- Syntax vs. Semantics (definitions + examples)
- Relationship of Syntax & Semantics
- Sentences, Lexemes, and Tokens
- Language Recognizers
- Language Generators
- Formal Methods of Describing Syntax
- Context-free Grammars (CFG)
- Backus-Naur Form (BNF)
- BNF Simple Example (An Integer)
- Metalanguage
- Grammars and Derivations
- Parse Trees

**Tags:** #programming-languages #CS3204N #syntax #semantics #BNF #context-free-grammar #parse-trees **Source:** [[PL-PPT2.pdf]]

---

## SYNTAX VS. SEMANTICS

> [!info] Definitions

**Syntax**

- Structure or **form** of statements.
- _Ex. `int num = 5;`_

**Semantics**

- **Meaning or behavior** of statements.
- _Ex. Integer 5 assigned to variable `num`_

---

## RELATIONSHIP OF SYNTAX & SEMANTICS

> [!note] Good Language Design
> 
> - **Meaning follows appearance**
> - **Syntax suggests behavior**

> _Syntax is easier to describe than semantics._

---

## SENTENCES

> Strings of a language, also called _**statements**_.

**Lexemes** — small units of a language

- Includes numeric literals, operators, and special words, among others
- Forms a group called _**identifiers**_
- A _**token**_ of a language is a category of its lexemes

### Lexeme → Token Example

```
index = 2 * count + 17;
```

|Lexeme|Token|
|---|---|
|`index`|identifier|
|`=`|equal_sign|
|`2`|int_literal|
|`*`|mult_op|
|`count`|identifier|
|`+`|plus_op|
|`17`|int_literal|
|`;`|semicolon|

---

## LANGUAGE RECOGNIZERS

> [!info] Definition A **recognizer** is a device that:
> 
> - Determines if a string **belongs** to a language
> - **Accepts or rejects** input

_Ex. Compiler syntax analyzer (parser)_

---

## LANGUAGE GENERATORS

> [!info] Definition A **generator** is a device that:
> 
> - **Produces valid sentences** of a language

_Ex. Compiler syntax analyzer (parser)_

---

## FORMAL METHODS OF DESCRIBING SYNTAX

> [!abstract] Overview Formal systems used to precisely and unambiguously define the syntax of a programming language.

---

## CONTEXT-FREE GRAMMARS

> [!info] Definition The **formal mathematical system** used to define the syntax of languages.

$$G = (V, E, R, S)$$

- **Terminals (E):** The basic symbols from which strings are formed. These are your **Tokens** _(e.g., `if`, `+`, `id`, numbers)_.
- **Variables / Non-terminals (V):** Placeholders that stand for patterns of strings _(e.g., `<sentence>`, `<expression>`)_.
- **Start Symbol (S):** The special variable where the derivation begins _(usually the top-level concept, like `<Program>`)_.
- **Productions / Rules (R):** The rules that say how to replace Variables with Terminals or other Variables.

---

## BACKUS-NAUR FORM (BNF)

|Component|Symbol|Description|
|---|---|---|
|**Non-Terminal**|`<name>`|A placeholder or category _(like `<sentence>` or `<loop>`)_. These need to be broken down further.|
|**Terminal**|`"text"`|The final pieces _(like `"if"`, `"+"`, or `0-9`)_. **These are your Tokens.** They cannot be broken down further.|
|**Definition**|`::=`|Means _"is defined as"_ or _"can be replaced by"_.|
|**Choice**|`\|`|Means _"or"_ — separates alternative options.|

---

## BNF SIMPLE EXAMPLE — AN INTEGER

```
<integer> ::= <sign> <digits>
<sign>    ::= "+" | "-" | <empty>
<digits>  ::= <digit> | <digit> <digits>
<digit>   ::= "0" | "1" | "2" | "3" | "4" | "5" | "6" | "7" | "8" | "9"
```

**How to read this:**

1. **`<integer>`** — An integer consists of a `<sign>` followed by `<digits>`.
2. **`<sign>`** — A sign can be a plus, a minus, or nothing (empty).
3. **`<digits>`** — This is a **recursive** rule. It says digits are either a single `<digit>`, OR a single `<digit>` followed by more `<digits>`. This allows numbers of infinite length _(e.g., `1`, `10`, `199`, `1000...`)_.
4. **`<digit>`** — These are the actual terminals (`"0"` through `"9"`).

---

## METALANGUAGE

> [!info] Definition A **metalanguage** is a language that is used to **describe another language**.

> _BNF is a metalanguage for programming languages._

_Ex._

```
<assign> -> <var> = <expression>
```

---

## GRAMMARS AND DERIVATIONS

- Sentences of a language start with a special nonterminal of the grammar called the **start symbol**.
- A sequence of rule applications is called a **derivation**.

### Example Grammar

```
<program>    → begin <stmt_list> end
<stmt_list>  → <stmt>
             | <stmt> ; <stmt_list>
<stmt>       → <var> = <expression>
<var>        → A | B | C
<expression> → <var> + <var>
             | <var> - <var>
             | <var>
```

---

## PARSE TREES

> [!info] Definition A **parse tree** shows the **hierarchical syntactic structure** of the sentences of a language.

### Example Parse Tree

> Represents the derivation of the statement: `A = B * (A + C)`

```
             <assign>
           /    |     \
         <id>   =    <expr>
          |         /   |   \
          A       <id>  *  <expr>
                   |       /  |  \
                   B      (  <expr> )
                            /  |   \
                          <id> +  <expr>
                           |         |
                           A       <id>
                                     |
                                     C
```