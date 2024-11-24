# Applied Mathematics III

- [Applied Mathematics III](#applied-mathematics-iii)
  - [Module 1 - Introduction to Set Theory \& Proofing Techniques](#module-1---introduction-to-set-theory--proofing-techniques)
    - [**Introduction to Set Theory**](#introduction-to-set-theory)
      - [1. **Definition of Sets**](#1-definition-of-sets)
      - [2. **Methods of Describing Sets**](#2-methods-of-describing-sets)
      - [3. **Types of Sets**](#3-types-of-sets)
      - [4. **Venn Diagrams**](#4-venn-diagrams)
      - [5. **Set Operations**](#5-set-operations)
      - [6. **Properties of Set Operations**](#6-properties-of-set-operations)
      - [7. **De Morgan’s Laws**](#7-de-morgans-laws)
      - [8. **Applications of Set Theory**](#8-applications-of-set-theory)
      - [9. **Cartesian Product of Sets**](#9-cartesian-product-of-sets)
    - [**Solved Questions on Set Theory**](#solved-questions-on-set-theory)
    - [**Pigeonhole Principle**](#pigeonhole-principle)
      - [Definition:](#definition)
      - [Types:](#types)
      - [Example Problems:](#example-problems)
    - [**Mathematical Induction**](#mathematical-induction)
      - [1. **Definition**](#1-definition)
      - [2. **Principle of Mathematical Induction**](#2-principle-of-mathematical-induction)
      - [3. **Steps of a Proof by Induction**](#3-steps-of-a-proof-by-induction)
      - [4. **Example Problems**](#4-example-problems)
        - [Example 1: Proving a Sum Formula](#example-1-proving-a-sum-formula)
        - [Example 2: Proving an Inequality](#example-2-proving-an-inequality)
      - [5. **Why Mathematical Induction Works**](#5-why-mathematical-induction-works)
      - [6. **Common Mistakes in Mathematical Induction**](#6-common-mistakes-in-mathematical-induction)


## Module 1 - Introduction to Set Theory & Proofing Techniques

### **Introduction to Set Theory**

#### 1. **Definition of Sets**
   - A **set** is a well-defined collection of distinct objects, often represented by uppercase letters (e.g., \( A, B, C \)).
   - Elements (or members) in a set are written as \( x \in A \) if \( x \) is in the set \( A \), and \( x \notin A \) if it is not.

#### 2. **Methods of Describing Sets**
   - **Roster or Tabular Form**: Lists all elements explicitly, e.g., \( A = \{1, 2, 3\} \).
   - **Set-Builder Form**: Defines elements based on a property, e.g., \( B = \{ x \ | \ x \text{ is an even number} \} \).

#### 3. **Types of Sets**
   - **Finite Set**: A set with a limited number of elements, e.g., \( C = \{1, 2, 3\} \).
   - **Infinite Set**: A set with an unlimited number of elements, e.g., the set of all natural numbers.
   - **Empty Set (Null Set)**: A set with no elements, denoted \( \emptyset \).
   - **Singleton Set**: A set with exactly one element, e.g., \( D = \{5\} \).
   - **Subset**: A set \( A \) is a subset of \( B \) if every element of \( A \) is in \( B \), written \( A \subseteq B \).
   - **Power Set**: The set of all subsets of a set \( A \), denoted \( P(A) \).

#### 4. **Venn Diagrams**
   - **Venn Diagrams** visually represent sets and their relationships, showing unions, intersections, and complements within a universal set.
  
```md
- Note: This document does not contain any venn diagrams, Refer to the handwritten notes for this.
```

#### 5. **Set Operations**
   - **Union** (\( A \cup B \)): The set of elements in \( A \), \( B \), or both. \( A \cup B = \{ x | x \in A \text{ or } x \in B \} \).
   - **Intersection** (\( A \cap B \)): The set of elements in both \( A \) and \( B \). \( A \cap B = \{ x | x \in A \text{ and } x \in B \} \).
   - **Difference** (\( A - B \) or \( A \setminus B \)): The set of elements in \( A \) but not in \( B \).
   - **Complement** (\( A' \)): The set of elements in the universal set \( U \) that are not in \( A \).

#### 6. **Properties of Set Operations**
   - **Commutative Laws**: \( A \cup B = B \cup A \); \( A \cap B = B \cap A \)
   - **Associative Laws**: \( (A \cup B) \cup C = A \cup (B \cup C) \); \( (A \cap B) \cap C = A \cap (B \cap C) \)
   - **Distributive Laws**: \( A \cup (B \cap C) = (A \cup B) \cap (A \cup C) \); \( A \cap (B \cup C) = (A \cap B) \cup (A \cap C) \)
   - **Identity Laws**: \( A \cup \emptyset = A \); \( A \cap U = A \)
   - **Complement Laws**: \( A \cup A' = U \); \( A \cap A' = \emptyset \)
   - **Idempotent Laws**: \( A \cup A = A \); \( A \cap A = A \)

#### 7. **De Morgan’s Laws**
   - **De Morgan's Laws** are useful for complements of unions and intersections:
     - \( (A \cup B)' = A' \cap B' \)
     - \( (A \cap B)' = A' \cup B' \)

#### 8. **Applications of Set Theory**
   - Used in **mathematics**, **computer science**, **statistics**, **probability**, and **linguistics**.

#### 9. **Cartesian Product of Sets**
   - The **Cartesian Product** of two sets \( A \) and \( B \), denoted \( A \times B \), is the set of ordered pairs \( (a, b) \) where \( a \in A \) and \( b \in B \).
   - **Example**: If \( A = \{1, 2\} \) and \( B = \{x, y\} \), then \( A \times B = \{(1, x), (1, y), (2, x), (2, y)\} \).

### **Solved Questions on Set Theory**

1. **Union and Intersection Example**:
   - **Question**: Given \( A = \{1, 2, 3\} \) and \( B = \{3, 4, 5\} \), find \( A \cup B \) and \( A \cap B \).
   - **Solution**:
     - \( A \cup B = \{1, 2, 3, 4, 5\} \)
     - \( A \cap B = \{3\} \)

2. **Complement Example**:
   - **Question**: Let \( U = \{1, 2, 3, 4, 5\} \) and \( A = \{2, 4\} \). Find \( A' \).
   - **Solution**:
     - \( A' = \{1, 3, 5\} \)

3. **De Morgan's Laws Example**:
   - **Question**: For \( A = \{1, 2\} \) and \( B = \{2, 3\} \) within \( U = \{1, 2, 3, 4\} \), verify \( (A \cup B)' = A' \cap B' \).
   - **Solution**:
     - \( A \cup B = \{1, 2, 3\} \), so \( (A \cup B)' = \{4\} \)
     - \( A' = \{3, 4\} \), \( B' = \{1, 4\} \), and \( A' \cap B' = \{4\} \)
     - This verifies \( (A \cup B)' = A' \cap B' \).

4. **Power Set Example**:
   - **Question**: Find the power set of \( C = \{1, 2\} \).
   - **Solution**:
     - \( P(C) = \{\emptyset, \{1\}, \{2\}, \{1, 2\}\} \)

### **Pigeonhole Principle**

#### Definition:
The **Pigeonhole Principle** states that if \( n \) items are put into \( m \) containers, and \( n > m \), at least one container will contain more than one item.

#### Types:
1. **Basic Pigeonhole Principle**: If more than \( m \) items are placed into \( m \) containers, at least one container will contain more than one item.
2. **Generalized Pigeonhole Principle**: If \( n \) items are placed into \( m \) containers, at least one container will contain at least \( \lceil \frac{n}{m} \rceil \) items.

#### Example Problems:
1. **Basic Example**:
   - **Question**: Suppose you have 10 pairs of socks and you randomly pick 11 socks. Prove that you have a matching pair.
   - **Solution**: There are only 10 types of socks. Since 11 socks are selected, the Pigeonhole Principle guarantees that at least one type will contain more than one sock, resulting in a matching pair.

2. **Generalized Example**:
   - **Question**: In a group of 25 people, prove that at least 3 people share the same birth month.
   - **Solution**: There are 12 months, so with 25 people distributed among 12 months, the Generalized Pigeonhole Principle guarantees that at least one month will contain \( \lceil \frac{25}{12} \rceil = 3 \) people.

3. **Application Example**:
   - **Question**: Prove that in any group of 13 people, at least two were born in the same month.
   - **Solution**: There are only 12 months, so by the Pigeonhole Principle, placing 13 people into these months ensures that at least one month contains more than one person.

Here are detailed notes on **Mathematical Induction**, an essential proof technique in mathematics, especially in topics involving sequences and series.

### **Mathematical Induction**

#### 1. **Definition**
   - **Mathematical Induction** is a method of proof used to establish the truth of an infinite sequence of statements, often involving positive integers. It is commonly used to prove statements about natural numbers and is particularly useful in proving formulas for sequences, divisibility, inequalities, and other properties.

#### 2. **Principle of Mathematical Induction**
   - The principle states that if a statement \( P(n) \) is true for the first term \( n = k \) and the truth of \( P(n) \) implies the truth of \( P(n + 1) \) for all \( n \geq k \), then \( P(n) \) is true for all \( n \geq k \).
   - **Basic Steps of Mathematical Induction**:
     1. **Base Case**: Show that the statement holds for the initial value (usually \( n = 1 \) or \( n = 0 \)).
     2. **Inductive Hypothesis**: Assume the statement holds for some arbitrary positive integer \( n = k \).
     3. **Inductive Step**: Show that if the statement is true for \( n = k \), then it must also be true for \( n = k + 1 \).

#### 3. **Steps of a Proof by Induction**
   - **Step 1**: Identify the statement \( P(n) \) that you want to prove.
   - **Step 2**: **Prove the Base Case**: Verify that \( P(k) \) is true for the starting value (e.g., \( k = 1 \) or \( k = 0 \)).
   - **Step 3**: **Formulate the Inductive Hypothesis**: Assume \( P(k) \) is true for some arbitrary integer \( k \).
   - **Step 4**: **Inductive Step**: Show that if \( P(k) \) is true, then \( P(k + 1) \) is also true.
   - **Step 5**: **Conclusion**: By induction, \( P(n) \) is true for all integers \( n \geq k \).

#### 4. **Example Problems**

##### Example 1: Proving a Sum Formula
   - **Problem**: Prove that the sum of the first \( n \) natural numbers is given by \( S(n) = 1 + 2 + \cdots + n = \frac{n(n + 1)}{2} \).
   
   - **Solution**:
     1. **Base Case**: For \( n = 1 \),
        \[
        S(1) = 1 = \frac{1 \cdot (1 + 1)}{2} = 1
        \]
        So, the base case is true.
        
     2. **Inductive Hypothesis**: Assume that \( S(k) = \frac{k(k + 1)}{2} \) is true for some arbitrary positive integer \( k \).
        
     3. **Inductive Step**: Prove that \( S(k + 1) = \frac{(k + 1)(k + 2)}{2} \).
        
        - Using the assumption \( S(k) = \frac{k(k + 1)}{2} \),
          \[
          S(k + 1) = S(k) + (k + 1)
          \]
          Substitute the assumption:
          \[
          S(k + 1) = \frac{k(k + 1)}{2} + (k + 1)
          \]
          Combine terms:
          \[
          S(k + 1) = \frac{k(k + 1) + 2(k + 1)}{2} = \frac{(k + 1)(k + 2)}{2}
          \]
        - Thus, \( S(k + 1) = \frac{(k + 1)(k + 2)}{2} \), so the inductive step holds.

     4. **Conclusion**: By mathematical induction, the formula is true for all \( n \geq 1 \).

##### Example 2: Proving an Inequality
   - **Problem**: Prove that \( 2^n > n \) for all \( n \geq 1 \).
   
   - **Solution**:
     1. **Base Case**: For \( n = 1 \),
        \[
        2^1 = 2 > 1
        \]
        The base case is true.
        
     2. **Inductive Hypothesis**: Assume \( 2^k > k \) holds for some \( k \geq 1 \).
        
     3. **Inductive Step**: Prove that \( 2^{k + 1} > k + 1 \).
        
        - Using the assumption \( 2^k > k \),
          \[
          2^{k + 1} = 2 \cdot 2^k > 2 \cdot k
          \]
        - Since \( k \geq 1 \), \( 2k \geq k + 1 \), so \( 2^{k + 1} > k + 1 \).
        
     4. **Conclusion**: By induction, \( 2^n > n \) for all \( n \geq 1 \).

#### 5. **Why Mathematical Induction Works**
   - Induction works similarly to "dominoes falling": if the first statement is true, and each statement implies the next, then all statements are true.

#### 6. **Common Mistakes in Mathematical Induction**
   - **Incorrect Base Case**: Ensure that the initial value is proven.
   - **Wrong Inductive Hypothesis**: The assumption must match the statement exactly.
   - **Faulty Inductive Step**: Always start with the assumption \( P(k) \) and use it logically to prove \( P(k + 1) \).

---

