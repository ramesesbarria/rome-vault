**Topics Covered:**

- Flow of control in programs  
- Control statements and control structures  
- Importance of control structures  
- Selection statements and two‑way selection  
- Control expressions and clauses  
- Nested selectors and the dangling else problem  
- Solutions to the dangling else problem  
- Multiple selection and case constructs  
- Iterative statements and loops  
- Loop control mechanisms (counter‑controlled, logically controlled, pretest, posttest)  
- User‑located loop control and data‑structure‑based iteration  
- Iterators and unconditional branches  
- Goto statements and spaghetti code  
- Guarded commands and guarded loops  
- Guard clauses (early return)  
- Nondeterministic selection

**Tags:** #programming-languages #CS3204N #control-flow #selection #iteration #loops **Source:** [[PL-PPT6.pdf]]

---

## FLOW OF CONTROL IN PROGRAMS

A program executes statements in a certain order called the **execution sequence**. Control flow in a program can be considered at three levels:

1. **Within expressions**
2. **Among statements**
3. **Among program units**

---

## CONTROL STATEMENTS AND CONTROL STRUCTURES

> [!info] A **control statement** determines the order in which other statements are executed. Its purpose is to control program flow, enable decisions, and enable repetition.

A **control structure** is a combination of a control statement and the statements whose execution it controls. For example:

if(x > y)  // control statement  
    max = x;  // controlled statement

---

## IMPORTANCE OF CONTROL STRUCTURES

Without control structures, programs would execute only sequentially and complex algorithms could not be implemented. Two fundamental programming needs are:

- **Selection**
- **Iteration**

---

## SELECTION

Selection allows a program to choose between two or more alternative paths of execution based on a condition. Example:

if (score >= 75)  
    print("Passed");

**Selection statements** provide this capability. Common examples include:

- `if`
- `if‑else`
- `switch` or `case`

---

## TWO‑WAY SELECTION STATEMENT

A **two‑way selection statement** allows the program to choose between two alternative paths. The general form is:

if (condition)  
    statement1  
else  
    statement2

The **control expression** in a selection or iteration statement is evaluated to determine which statements should be executed. In `if (x > 10)`, the expression `x > 10` is the control expression.

**Then clause and else clause:**

- **Then clause:** The part of an `if` statement executed when the control expression is true.
- **Else clause:** The part executed when the control expression is false.

Example:

if (x > y)  
    max = x;   // then clause  
else  
    max = y;   // else clause

---

## NESTED SELECTOR AND THE DANGLING ELSE PROBLEM

A **nested selector** occurs when a selection statement appears inside another selection statement. For example:

if (x > 0)  
    if (y > 0)  
        print("positive")

> [!warning] **Dangling else problem:** In nested `if` statements it can be ambiguous which `if` an `else` clause belongs to. Consider:

if (x > 0)  
    if (y > 0)  
        print("A")  
    else  
        print("B")

Which `if` does the `else` belong to?

---

## SOLUTIONS TO THE DANGLING ELSE PROBLEM

Programming languages solve the dangling else problem by one or more of the following:

- **Associating the `else` with the nearest unmatched `if`.**
- **Using block delimiters:** for example, `{ }` in C/Java.
- **Using explicit terminators:** for example, `end if` in Ada.
- **Using indentation:** Python uses indentation to make the structure clear.

---

## MULTIPLE SELECTION

A **multiple selection** statement allows the program to choose among several alternative execution paths. An example using C‑style `switch`:

switch(day)  
{  
    case 1: Monday  
    case 2: Tuesday  
}

Important terms:

- **Selector expression:** The expression whose value determines which case branch will be executed. In `switch(day)`, `day` is the selector expression.
- **Case label:** A constant value associated with a branch in a multiple selection statement that determines when that branch is executed (e.g., `case 1:`).
- **Default clause:** An optional branch executed when none of the case labels match the selector expression. Example:
    
      default:  
          print("Invalid input");
    

---

## ITERATIVE STATEMENTS

> [!info] An **iterative statement** repeatedly executes a block of code as long as a specified condition holds.

Common loop constructs include `for`, `while`, and `do‑while`.

**Iteration** is the repeated execution of a block of code within a loop structure (for example, printing numbers 1–10).

---

## COUNTER‑CONTROLLED AND LOGICALLY CONTROLLED LOOPS

**Counter‑controlled loop:**

A loop whose number of iterations is controlled by a loop variable that changes by a fixed amount each iteration. Example:

for (i = 1; i <= 10; i++)

Here `i` is the **loop variable** controlling the number of times the loop executes. The **stepsize** is the amount by which the loop variable changes each iteration; in `i = i + 2`, the stepsize is 2.

**Logically controlled loop:**

A loop whose execution depends on the truth value of a Boolean expression. Examples include `while` and `do‑while` loops.

---

## PRETEST AND POSTTEST LOOPS

**Pretest loop:** The control expression is evaluated before the loop body executes. Example:

while (condition)  
    // loop body

If the condition is false initially, the loop body never executes.

**Posttest loop:** The control expression is evaluated after the loop body executes. Example:

do  
{  
    // loop body  
}  
while (condition);

The loop executes at least once because the condition is checked after executing the body.

---

## USER‑LOCATED LOOP CONTROL AND DATA STRUCTURE‑BASED ITERATION

**User‑located loop control mechanism:** A loop control method where the programmer places statements inside the loop body to alter loop execution. Examples include `break` and `continue`.

**Iteration based on data structures:** A loop mechanism that automatically iterates over elements of a collection or data structure. For example, in Python:

for item in list:  
    // process item

An **iterator** is an object or mechanism that allows a program to traverse the elements of a data structure sequentially, such as iterating through a list or array.

---

## UNCONDITIONAL BRANCHES AND GOTO STATEMENT

An **unconditional branch** is a control statement that transfers execution to another part of the program without evaluating a condition. Examples include `goto`, `break`, and `return`.

The **goto statement** causes an unconditional jump to another labeled statement in the program. Example:

goto label;

---

## SPAGHETTI CODE

> [!warning] **Spaghetti code** refers to a program structure characterised by complex and tangled control flow caused by excessive use of `goto` statements.

Problems with spaghetti code include:

- Hard to read
- Hard to debug
- Hard to maintain

---

## GUARDED COMMANDS AND GUARDED SELECTION

A **guarded command** consists of a Boolean expression (the **guard**) and a statement that executes when the guard is true. A simple notation is:

B → S

Where `B` is the guard and `S` is the statement.

In a **guarded selection**, multiple guards are listed. For example:

if  
    B1 → S1  
[] B2 → S2  
fi

If multiple guards are true, one is chosen nondeterministically.

A **guarded loop** repeats guarded commands while at least one guard remains true. Example:

do  
    B1 → S1  
[] B2 → S2  
od

---

## GUARD CLAUSES (EARLY RETURN)

Modern **guard clauses** provide an early return from a function or block when a condition is met. The PDF distinguishes between code **without guard clauses** and **with guard clauses**, but specific examples are not provided.

[Unclear from PDF]

---

## NONDETERMINISTIC SELECTION

**Nondeterministic selection** is a selection mechanism in which multiple guards may be true and the language allows any one of them to be chosen for execution.