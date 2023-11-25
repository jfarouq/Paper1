---
title: Paper 1 Lesson 2.9 - Boolean statements and logic
---

# Boolean Statements and Logic

As we have seen in earlier notes, a **boolean statement** is a statement that evaluates to either "True" or "False". 

For each of the following boolean statements, decide if it evaluates to true or false.

1. 2 + 2 = 7
2. √49=7 
3. It is raining outside right now.
4. It is not raining outside right now.
5. Mr. Farouq is a teacher and Mr. Farouq is American.
6. Mr. Farouq is a teacher or Mr. Farouq is an American.
7. Either Mr. Farouq is a teacher or Mr. Farouq is an American.

## Boolean operators

There are 6 boolean operators we need to know. Below they are explained.

### NOT

The NOT operator changes a true boolean statement to a false one, and vice versa. So if `A` is true, then `NOT A` is false. The programming equivalent in Typescript and Java is the `!` operator, as in `! isBlue`.

You can represent the behavior of boolean operators with a *truth table* - the one for NOT is simple:

| A   | NOT A |
| --- | ----- |
| 0   | 1     |
| 1   | 0     |

### OR

The OR operator combines two boolean statements. If EITHER of the statements are true, the entire OR statement is true. So `2 = 2 OR 2 = 3` is a true statement. The Typescript / Java equivalent is the `||` operator, as in `x < 0 || y < 0` (which will be true if either value is negative, or both)

For operators like OR that combine two statements, we need a larger truth table.

| A   | B   | A OR B |
| --- | --- | ------ |
| 0   | 0   | 0      |
| 0   | 1   | 1      |
| 1   | 0   | 1      |
| 1   | 1   | 1     |

### AND

The AND operator combines two boolean statements and is only true if BOTH of the statements are true, otherwise it is false. So `2 = 2 AND 2 = 3` is a false statement, but `2 = 2 AND 2 > 1` is true. The Typescript/Java equivalent is the `&&` operator, as in `x < 0 && y < 0` (only true if both are less than 0)

| A   | B   | A AND B |
| --- | --- | ------- |
| 0   | 0   | 0       |
| 0   | 1   | 0       |
| 1   | 0   | 0       |
| 1   | 1   | 1       |

### XOR

The XOR operator stands for *exclusive or* and it is used in situations we might use the English phrase "either...or" - meaning it is NOT okay for both. We might say "You can have either a cookie OR a brownie", which is an exclusive or. There is no single XOR operator in java / Typescript, but if you're sure that `a` and `b` are both boolean values, you can "cheat" by realizing that this simply means they are not equal to each other and use `a != b` to work like XOR.

| A   | B   | A XOR B |
| --- | --- | ------- |
| 0   | 0   | 0       |
| 0   | 1   | 1       |
| 1   | 0   | 1       |
| 1   | 1   | 0       |

### NOR

The NOR operator means "NOT OR" and returns the exact opposite of the OR operator. It is only true if BOTH of the operands are FALSE. So "2 = 2 NOR 2 = 3" is false because one of the statements is true. There is no single NOR operator in java/Typescript, but you can build one combining `!` and `||` like `! (x < 0  || y < 0)`. (a little thinking will realize this is the same as saying `x >= 0 && y >= 0` , which is true - there are usually multiple ways to build complex logical expressions.)


| A   | B   | A NOR B |
| --- | --- | ------- |
| 0   | 0   | 1       |
| 0   | 1   | 0       |
| 1   | 0   | 0       |
| 1   | 1   | 0       |

### NAND

The NAND operator means "NOT AND" and returns the opposite of the AND operator. `A NAND B` is logically equivalen to `NOT A OR NOT B` and that is usually more common, but we still have to know the NAND operator!

| A   | B   | A NAND B |
| --- | --- | -------- |
| 0   | 0   | 1        |
| 0   | 1   | 1        |
| 1   | 0   | 1        |
| 1   | 1   | 0        |

## Building Complex Truth Tables

One required skill for the IB exam is to build truth tables (like the ones above) based on these operators. I will work through an example.

> Build a truth table for the statement `(A OR B) OR (B NAND A)`

To build these, we start by figuring out our headings, working from the inside out. This always starts with our individual letters that represent individual statements (in this case A and B) and then we work our way outward to the complete statement, doing little middle statements as need be following the order or operations. (These operators all have the same power, so if parenthese don't make it clear move form left to right).

The first two columns always go "0011" and "0101" to make all four combinations.

| A   | B   | B NAND A | A OR B | (A OR B) OR (B NAND A) |
| --- | --- | -------- | ------ | ---------------------- |
| 0   | 0   |          |        |                        |
| 0   | 1   |          |        |                        |
| 1   | 0   |          |        |                        |
| 1   | 1   |          |        |                        |

We then build from left to right, following the rules for each operator. NAND the opposite of AND so it is False only when both are True. OR is true whenever either is true.

| A   | B   | B NAND A | A OR B | (A OR B) OR (B NAND A) |
| --- | --- | -------- | ------ | ---------------------- |
| 0   | 0   | 1        | 0      |                        |
| 0   | 1   | 1        | 1      |                        |
| 1   | 0   | 1        | 1      |                        |
| 1   | 1   | 0        | 1      |                        |

Then for the final column, we are applying the OR operator to the two columns I just made! OR is true whenever either of the inputs are true, so the output is...

| A   | B   | B NAND A | A OR B | (A OR B) OR (B NAND A) |
| --- | --- | -------- | ------ | ---------------------- |
| 0   | 0   | 1        | 0      | 1                      |
| 0   | 1   | 1        | 1      | 1                      |
| 1   | 0   | 1        | 1      | 1                      |
| 1   | 1   | 0        | 1      | 1                      |

This statement is always true! Oops, that was a lot of work for a rather simple output!

### Order of Operations

Sometimes, the IB will provide you with a logic statement that doesn't include parentheses, so you have to figure out which order to apply your operations. The rules are:

1. NOT goes first, so NOT A OR B is the same as (NOT A) OR B
2. AND and NAND go next (left-to right) so A OR B AND C is the same as A OR (B AND C)
3. OR, XOR, and NOR go last (left to right) so A OR B XOR C is (A OR B) XOR C but A XOR B OR C is (A XOR B) OR C

### Practice problems 

Try these examples (bonus: for each one try to come up with a DIFFERENT statement that would have the same result)

1.  Create a truth table for the statement `(A NOR B) OR A`
  
    <details markdown="1"><summary>Click to expand answer</summary>

    | A   | B   | A NOR B | (A NOR B) OR A |
    | --- | --- | ------- | -------------- |
    | 0   | 0   | 1       | 1              |
    | 0   | 1   | 0       | 0              |
    | 1   | 0   | 0       | 1              |
    | 1   | 1   | 0       | 1              |

    </details>

2.  Create a truth table for the statement `(A XOR B) AND A`
   
     <details markdown="1"><summary>Click to expand answer</summary>

    | A   | B   | A XOR B | (A XOR B) AND A |
    | --- | --- | ------- | --------------- |
    | 0   | 0   | 0       | 0               |
    | 0   | 1   | 1       | 0               |
    | 1   | 0   | 1       | 1               |
    | 1   | 1   | 0       | 0               |

    </details>
    
3.  Create a truth table for the statement `NOT (A XOR B)`

    <details markdown="1"><summary>Click to expand answer</summary>

    | A   | B   | A XOR B | NOT (A XOR B) |
    | --- | --- | ------- | ------------- |
    | 0   | 0   | 0       | 1             |
    | 0   | 1   | 1       | 0             |
    | 1   | 0   | 1       | 0             |
    | 1   | 1   | 0       | 1             |

    </details>

4.  Create a truth table for the statement `NOT (A OR B)`
   
    <details markdown="1"><summary>Click to expand answer</summary>

    | A   | B   | A OR B | NOT (A OR B) |
    | --- | --- | ------ | ------------ |
    | 0   | 0   | 0      | 1            |
    | 0   | 1   | 1      | 0            |
    | 1   | 0   | 1      | 0            |
    | 1   | 1   | 1      | 0            |

    </details>
    
5.  Create a truth table for the statement `NOT A AND NOT B`

    <details markdown="1"><summary>Click to expand answer</summary>

    | A   | B   | NOT A | NOT B | NOT A AND NOT B |
    | --- | --- | ----- | ----- | --------------- |
    | 0   | 0   | 1     | 1     | 1               |
    | 0   | 1   | 1     | 0     | 0               |
    | 1   | 0   | 0     | 1     | 0               |
    | 1   | 1   | 0     | 0     | 0               |
    
    </details>

6.  Create a truth table for the statement `A AND (B NOR C)` - note, with three inputs the table will need 8 rows!

    <details markdown="1"><summary>Click to expand answer</summary>

  | A   | B   | C   | B NOR C | A AND (B NOR C) |
  | --- | --- | --- | ------- | --------------- |
  | 0   | 0   | 0   | 1       | 0               |
  | 0   | 0   | 1   | 0       | 0               |
  | 0   | 1   | 0   | 0       | 0               |
  | 0   | 1   | 1   | 0       | 0               |
  | 1   | 0   | 0   | 1       | 1               |
  | 1   | 0   | 1   | 0       | 0               |
  | 1   | 1   | 0   | 0       | 0               |
  | 1   | 1   | 1   | 0       | 0               |
    </details>

7.  Create a truth table for the statement `(A XOR C) OR B` - note, with three inputs the table will need 8 rows!

    <details markdown="1"><summary>Click to expand answer</summary>

  | A   | B   | C   | A XOR C | (A  XOR C) OR B |
  | --- | --- | --- | ------- | --------------- |
  | 0   | 0   | 0   | 0       | 0               |
  | 0   | 0   | 1   | 1       | 1               |
  | 0   | 1   | 0   | 0       | 1               |
  | 0   | 1   | 1   | 1       | 1               |
  | 1   | 0   | 0   | 1       | 1               |
  | 1   | 0   | 1   | 0       | 0               |
  | 1   | 1   | 0   | 1       | 1               |
  | 1   | 1   | 1   | 0       | 1               |
    </details>

8.  Create a truth table for the statement `(A NAND B) XOR NOT C` - note, with three inputs the table will need 8 rows!

    <details markdown="1"><summary>Click to expand answer</summary>

  | A   | B   | C   | A NAND B | NOT C | (A  NAND B) XOR NOT B |
  | --- | --- | --- | -------- | ----- | --------------------- |
  | 0   | 0   | 0   | 1        | 1     | 0                     |
  | 0   | 0   | 1   | 1        | 0     | 1                     |
  | 0   | 1   | 0   | 1        | 1     | 0                     |
  | 0   | 1   | 1   | 1        | 0     | 1                     |
  | 1   | 0   | 0   | 1        | 1     | 0                     |
  | 1   | 0   | 1   | 1        | 0     | 1                     |
  | 1   | 1   | 0   | 0        | 1     | 1                     |
  | 1   | 1   | 1   | 0        | 0     | 0                     |
    </details>





