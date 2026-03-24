**Topics Covered:**

- Introduction & Descriptors  
- Primitive Data Types (Numeric & Boolean)  
- Character & String Types  
- User‑Defined Ordinal Types  
- Array Types & Subscript Binding  
- Array Implementation & Memory Layout  
- Associative Arrays  
- Record Types  
- Tuple and List Types  
- Union Types  
- Pointer Types & Memory Problems  
- Reference Types & Garbage Collection  
- Strong Typing & Type Equivalence

**Tags:** #programming-languages #CS3204N #data-types #arrays #pointers #typing **Source:** [[PL-PPT5.pdf]]

---

## INTRODUCTION & DESCRIPTORS

> [!info] **Concept:** Data types play a central role in programming languages. Compilers track data types through **descriptors**—collections of attributes for variables.

Key points:

- **Descriptors** are needed at compile‑time for static types and at run‑time for dynamic types.
- **Abstract Data Types** separate the interface from the implementation; they are a foundational concept in programming languages.

---

## PRIMITIVE DATA TYPES (NUMERIC & BOOLEAN)

> [!note] **Primitive data types** are not defined in terms of other data types.

**Numeric types:**

- **Integer:** Representations depend on the hardware; most systems use two’s complement.
- **Floating‑point:** Approximate real numbers, usually following **IEEE 754** standards.
- **Decimal:** Use a fixed number of decimal digits (BCD format) and are crucial for financial applications.

**Boolean type:**

- Represents the values **true** and **false**.
- Often implemented as a single byte for efficient memory access.

---

## CHARACTER & STRING TYPES

**Character types:**

- Characters are mapped to integers through encodings such as **ASCII** (8‑bit) or **Unicode** (16‑ or 32‑bit).

**String types:**

- **String length options:**
    - **Static:** Length is fixed at compile time.
    - **Limited dynamic:** Maximum length is fixed, but actual length can vary at run time.
    - **Dynamic:** Length can change during execution.
- **C‑style strings:** Arrays of characters terminated by a null character (`\0`).
- **Modern strings:** Often implemented as **immutable objects** (e.g., in Java and Python).

---

## USER‑DEFINED ORDINAL TYPES

An **ordinal type** is one where the range of possible values can be easily associated with the set of positive integers.

Examples:

- **Enumerations:** The possible values are named constants provided in the definition.
- **Subranges:** Ordered, contiguous subsequences of an ordinal type (e.g., a range in Ada).

> [!tip] Using enumerations and subranges drastically improves readability and reliability compared to using raw integer codes.

---

## ARRAY TYPES & SUBSCRIPT BINDING

> [!note] An **array** is a homogeneous aggregate of data elements accessed by relative position.

**Subscript binding and allocation strategies:**

- **Static arrays:** Subscript ranges are statically bound and memory is allocated statically (e.g., `static` arrays in C).
- **Fixed stack‑dynamic arrays:** Ranges are statically bound, but allocation happens at run time on the stack (e.g., local arrays in C).
- **Fixed heap‑dynamic arrays:** Storage is bound to the heap at run time; length remains fixed (e.g., Java arrays).
- **Heap‑dynamic arrays:** Both length and storage are dynamic and can change during execution (e.g., Python lists, `List` in C#).

---

## ARRAY IMPLEMENTATION & MEMORY LAYOUT

Array storage requires a mechanism to map **logical subscripts** to **physical addresses**.

**Memory layout strategies:**

- **Row‑major order:** Elements of a row are placed in contiguous memory.
- **Column‑major order:** Elements of a column are placed in contiguous memory (historically used in Fortran).
- **Slices:** Substructures of an array that can be extracted as a new array; common in languages such as Python.

---

## ASSOCIATIVE ARRAYS

**Associative arrays** are unordered collections of data elements indexed by keys.

Key aspects:

- **Implementation:** Typically implemented via **hash tables**.
- **Language examples:** Hashes in Perl, dictionaries in Python, and maps in Java/C++.
- **Design issue:** What types are allowed as keys?

---

## RECORD TYPES

> [!info] A **record** is an aggregate of data elements (fields) where each element is uniquely named and fields can be heterogeneous.

Characteristics:

- **Access:** Fields are accessed by name using dot notation (e.g., `student.GPA`).
- **Implementation:** Fields are stored in adjacent memory locations, with offsets calculated at compile time.
- **Comparison:** Records are safer than parallel arrays for grouping related data.

---

## TUPLE AND LIST TYPES

**Tuples:**

- Similar to records but the elements are **not named**.
- Often **immutable** (e.g., Python tuples).

**Lists:**

- Ordered, mutable sequences; fundamental to functional languages such as LISP, ML, and F#.
- **List comprehensions:** A powerful mechanism to generate lists derived from mathematics (e.g., in Haskell and Python).

---

## UNION TYPES

A **union type** allows variables to store different type values at different times during execution.

- **Free unions:** No type checking is done (e.g., `union` in C/C++). These are highly unsafe.
- **Discriminated unions:** Include a **type indicator** (a tag) to enforce type checking (e.g., in Ada, ML, and F#).

---

## POINTER TYPES & MEMORY PROBLEMS

> [!note] A **pointer** is a variable whose value is a memory address (or the special value `null`).

Pointer operations:

- **Allocation:** Obtaining a new memory cell.
- **Dereferencing:** Accessing the value at the referenced address.

Common issues:

- **Dangling pointers:** A pointer containing the address of a heap‑dynamic variable that has been deallocated.
- **Memory leaks:** A heap‑dynamic variable that is no longer accessible by the program (a lost object).

---

## REFERENCE TYPES & GARBAGE COLLECTION

**References** are similar to pointers, but they refer to an **object** or **value** in memory, not a raw physical address (e.g., objects in Java).

**Garbage collection strategies:**

- **Reference counters:** Maintain a tally of references to an object and reclaim memory when the tally hits zero.
- **Mark‑sweep algorithm:** Periodically pauses program execution, marks all reachable objects from the roots, and sweeps away the unmarked ones.

---

## STRONG TYPING & TYPE EQUIVALENCE

**Type checking** is the activity of ensuring that the operands of an operator are of compatible types.

**Strong typing:** A language is strongly typed if it reliably detects all type errors at compile time or run time.

**Type equivalence:**

- **Name equivalence:** Two variables have equivalent types if they appear in the same declaration or use the same type name.
- **Structural equivalence:** Two variables have equivalent types if their underlying memory structures are identical.