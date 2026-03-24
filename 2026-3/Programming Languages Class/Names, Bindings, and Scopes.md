**Topics Covered:**

- Introduction to names, bindings and scopes  
- Names (identifiers)  
- Variables and their attributes  
- The concept of binding  
- Binding times (static vs. dynamic)  
- Type binding mechanisms  
- Storage bindings and lifetime  
- Scalar variables by lifetime  
- Understanding scope  
- Static and dynamic scoping  
- Scope versus lifetime  
- Referencing environments  
- Named constants

**Tags:** #programming-languages #CS3204N #names #bindings #scope #variables #lifetime #constants **Source:** [[PL-PPT4.pdf]]

---

## INTRODUCTION

> [!info] Imperative programming languages are abstractions of the **von Neumann computer architecture**. Memory cells are abstracted as variables. This section introduces the fundamental attributes of variables and the concept of binding.

---

## NAMES (IDENTIFIERS)

**Names are used to identify entities in programs.** When designing a language you must decide:

- **Case sensitivity:** Are uppercase and lowercase names considered distinct?
- **Reserved words vs. keywords:** A _reserved word_ cannot be used as a user‑defined name, improving readability. A _keyword_ is special only in certain contexts (e.g., `Integer` in Fortran).
- **Length limits:** Languages impose different limits on identifier length—C99 has no limit, but only the first 63 characters are significant.

---

## VARIABLES

> [!note] A **variable** is an abstraction of a computer memory cell or collection of cells.

Variables are characterised by a **sextuple of attributes**:

1. **Name** – the identifier associated with the memory cell.
2. **Address** – the memory location; also called the **L‑value**, because it is needed when the variable appears on the left side of an assignment.
3. **Value** – the contents of the cell; the **R‑value**, required when the variable appears on the right side of an assignment.
4. **Type** – determines the range of values that can be stored and the operations defined for them.
5. **Lifetime** – the duration for which the variable is bound to a memory location.
6. **Scope** – the range of statements in which the variable is visible.

> **Note on aliases:** Aliases arise when more than one name refers to the same memory location (via pointers, references, or unions). While sometimes necessary, aliases can hinder readability.

---

## THE CONCEPT OF BINDING

**Binding** is an association between an attribute and an entity (for example, between a variable and its type or an operation and a symbol).

**Binding times:**

- **Language design time** – e.g., binding `*` to multiplication.
- **Language implementation time** – e.g., binding `int` to a particular range of values.
- **Compile time** – e.g., binding a variable to a type in C.
- **Load time** – e.g., binding a static variable to a memory cell.
- **Runtime** – e.g., binding a local variable to a memory cell during execution.

> [!warning] **Static vs. dynamic binding**

- **Static binding:** Occurs before run time and remains unchanged throughout program execution.
- **Dynamic binding:** Occurs during execution or can change while the program runs.

---

## TYPE BINDING MECHANISMS

**Static type binding:**

- **Explicit declaration:** A statement lists variable names and specifies their type.
- **Implicit declaration:** Types are assigned through default conventions rather than explicit declarations (e.g., in Fortran, variables starting with `I`–`N` are integers).
- **Type inferencing:** The type is determined from context, such as in `var sum = 0;` where `sum` is inferred to be an integer.

**Dynamic type binding:**

- A variable is bound to a type when it is assigned a value (e.g., variables in Python or JavaScript).

---

## STORAGE BINDINGS & LIFETIME

**Allocation** is obtaining a cell from an available pool of memory; **deallocation** is returning a cell to the pool.

> [!tip] **Lifetime** begins with allocation and ends with deallocation. It is the period during which a variable is bound to a specific memory location.

---

## SCALAR VARIABLES BY LIFETIME

Scalar variables can be categorised by their lifetime:

1. **Static variables** – bound to memory cells before execution begins and remain bound to the same cell throughout execution. They are highly efficient but do not support recursion.
2. **Stack‑dynamic variables** – storage bindings are created when their declaration statements are elaborated at run time, but their types are statically bound. They support recursion but incur run‑time overhead for allocation.
3. **Explicit heap‑dynamic variables** – allocated and deallocated by explicit directives at run time (e.g., `new` and `delete` in C++). Useful for dynamic structures such as trees and linked lists.
4. **Implicit heap‑dynamic variables** – allocation and deallocation are caused implicitly by assignment statements (e.g., variables in APL or strings in JavaScript). They are highly flexible but inefficient.

---

## UNDERSTANDING SCOPE

**Scope** is the range of statements in which a variable is **visible**. A variable is visible in a statement if it can be referenced in that statement.

Variables can be categorised as:

- **Local variables:** Declared within a specific block or unit.
- **Nonlocal variables:** Visible in a unit but not declared there.
- **Global variables:** A special category of nonlocal variables accessible throughout the program.

---

## STATIC SCOPING

> [!note] **Static (lexical) scoping** means that the scope of a variable can be determined at compile time based on the program’s textual structure.

Key ideas:

- **Static ancestors:** Enclosing static scopes; subprograms can be nested inside others.
- **Blocks:** A method for creating localised static scopes inside program units, such as code enclosed within braces `{ … }`.

---

## DYNAMIC SCOPING

**Dynamic scoping** is based on the _calling sequence of subprograms_ rather than their textual arrangement.

To resolve a nonlocal reference under dynamic scoping, the runtime stack is searched backward until a declaration is found.

> [!warning] Dynamic scoping lowers readability and reliability because nonlocal references cannot be statically type‑checked.

---

## SCOPE VS. LIFETIME

Scope and lifetime are often confused but are **distinct concepts**:

- **Scope** is a **spatial** concept—a textual region in the program where a name can be referenced.
- **Lifetime** is a **temporal** concept—a period during program execution when a variable is bound to a memory location.

**Example:** A `static` variable declared inside a C/C++ function has a lifetime equal to the entire program but a scope limited to that function.

---

## REFERENCING ENVIRONMENTS

The **referencing environment** is the collection of all names that are visible at a given statement in a program.

In a **static‑scoped** language, it consists of local variables plus all visible variables in enclosing scopes.

In a **dynamic‑scoped** language, it consists of local variables plus all visible variables in all active subprograms. An **active subprogram** is one whose execution has begun but has not yet terminated.

---

## NAMED CONSTANTS

A **named constant** is a variable bound to a value when it is bound to storage; it cannot be changed later.

**Manifest constants** are named constants whose values are mapped at compile time. They are used to improve readability and to parameterise programs—e.g., using `MAX_LENGTH` instead of the literal `100`.