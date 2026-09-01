# ExpNo 8: Solve Cryptarithmetic Problem, a CSP (Constraint Satisfaction Problem) Using Python

| **Name**                       | Surya Prakash B  |
| ------------------------------ | - |
| **Register Number** | 212224230281  |

## Aim

To solve a **Cryptarithmetic Problem** as a **Constraint Satisfaction Problem (CSP)** using Python.

---

# Theory

## Cryptarithmetic Problem

A **Cryptarithmetic puzzle** is a mathematical puzzle in which letters represent digits from `0` to `9`.

The objective is to assign a unique digit to each letter so that the given arithmetic equation becomes correct.

For example:

```text
    S E N D
  + M O R E
  ----------
  M O N E Y
```

Each letter represents exactly one digit.

### Rules

1. Each letter must represent a unique digit.
2. A digit cannot be assigned to two different letters.
3. The same letter must always have the same digit.
4. A leading letter cannot be assigned `0`.
5. The resulting arithmetic equation must be correct.

For the `SEND + MORE = MONEY` problem:

```text
SEND = 9567
MORE = 1085
MONEY = 10652
```

Therefore:

```text
9567 + 1085 = 10652
```

Hence, the solution is valid.

---

# Constraint Satisfaction Problem (CSP)

A **Constraint Satisfaction Problem** consists of:

* **Variables**
* **Domains**
* **Constraints**

For this problem:

### Variables

The variables are the letters:

```text
S, E, N, D, M, O, R, Y
```

### Domains

Each letter can take a digit from:

```text
0, 1, 2, 3, 4, 5, 6, 7, 8, 9
```

### Constraints

The important constraints are:

```text
S, E, N, D, M, O, R, Y must all be different
```

and:

```text
S ≠ 0
M ≠ 0
```

because `S` and `M` are the leading digits of `SEND` and `MORE`.

The main arithmetic constraint is:

```text
SEND + MORE = MONEY
```

---

# Problem Representation

The puzzle is:

```text
      S E N D
    + M O R E
    ---------
    M O N E Y
```

The corresponding numerical values are:

```text
SEND  = 1000S + 100E + 10N + D

MORE  = 1000M + 100O + 10R + E

MONEY = 10000M + 1000O + 100N + 10E + Y
```

The program searches for values that satisfy:

```text
SEND + MORE = MONEY
```

---

# Approach Used

The program uses Python's `permutations()` function to generate possible assignments of digits.

There are 8 different letters:

```text
S, E, N, D, M, O, R, Y
```

Therefore, we select 8 different digits from the digits `0` to `9`.

```python
permutations(range(10), 8)
```

Each permutation represents one possible assignment.

For example:

```text
(9, 5, 6, 7, 1, 0, 8, 2)
```

means:

```text
S = 9
E = 5
N = 6
D = 7
M = 1
O = 0
R = 8
Y = 2
```

which gives:

```text
SEND  = 9567
MORE  = 1085
MONEY = 10652
```

---

# Algorithm

1. Define the letters:

```text
S, E, N, D, M, O, R, Y
```

2. Generate permutations of 8 unique digits from `0` to `9`.
3. Assign the digits to the letters.
4. Check the leading-zero constraint:

   * `S` must not be `0`.
   * `M` must not be `0`.
5. Construct the numerical values of `SEND`, `MORE`, and `MONEY`.
6. Check whether:

```text
SEND + MORE = MONEY
```

7. If the equation is satisfied:

   * Return the solution.
8. If no permutation satisfies the equation:

   * Return `None`.
9. Display the solution.

---

# Python 3 Program

```python
from itertools import permutations


def solve_cryptarithmetic():

    # Generate permutations of 8 unique digits
    # from 0 to 9
    for perm in permutations(range(10), 8):

        # Assign digits to letters
        S, E, N, D, M, O, R, Y = perm

        # Leading letters cannot be zero
        if S == 0 or M == 0:
            continue

        # Construct the numbers
        SEND = 1000 * S + 100 * E + 10 * N + D

        MORE = 1000 * M + 100 * O + 10 * R + E

        MONEY = 10000 * M + 1000 * O + 100 * N + 10 * E + Y

        # Check the equation
        if SEND + MORE == MONEY:
            return SEND, MORE, MONEY

    # No solution found
    return None


# Call the function
solution = solve_cryptarithmetic()


# Display the solution
if solution:

    SEND, MORE, MONEY = solution

    print(f'SEND = {SEND}')
    print(f'MORE = {MORE}')
    print(f'MONEY = {MONEY}')

else:

    print("No solution found.")
```

---

# Missing Code in the Original Program

The first missing part is:

```python
if S == 0 or M == 0:
    continue
```

### Why?

`S` is the first letter of `SEND`, and `M` is the first letter of `MORE` and `MONEY`.

A number cannot start with zero.

For example:

```text
0567
```

is not considered a valid four-digit number.

Therefore:

```text
S ≠ 0
M ≠ 0
```

---

The second missing part is:

```python
solution = solve_cryptarithmetic()
```

This calls the function and stores the returned solution.

---

# Sample Input

The cryptarithmetic problem is:

```text
SEND + MORE = MONEY
```

No keyboard input is required because the words are already defined in the program.

---

# Sample Output

```text
SEND = 9567
MORE = 1085
MONEY = 10652
```

The equation can be verified as:

```text
  9567
+ 1085
------
 10652
```

Therefore:

```text
9567 + 1085 = 10652
```

---

# Letter-to-Digit Mapping

The solution gives the following mapping:

| Letter | Digit |
| ------ | ----: |
| `S`    |   `9` |
| `E`    |   `5` |
| `N`    |   `6` |
| `D`    |   `7` |
| `M`    |   `1` |
| `O`    |   `0` |
| `R`    |   `8` |
| `Y`    |   `2` |

Therefore:

```text
S E N D
9 5 6 7
```

```text
M O R E
1 0 8 5
```

```text
M O N E Y
1 0 6 5 2
```

---

# Verification

Substituting the digits:

```text
SEND = 9567
MORE = 1085
MONEY = 10652
```

Now verify:

```text
9567 + 1085
```

```text
= 10652
```

Therefore:

```text
SEND + MORE = MONEY
```

The solution is correct.

---

# Understanding `permutations()`

The program imports:

```python
from itertools import permutations
```

and uses:

```python
permutations(range(10), 8)
```

`range(10)` generates:

```text
0 1 2 3 4 5 6 7 8 9
```

`permutations(..., 8)` selects 8 different digits at a time.

For example:

```text
(9, 5, 6, 7, 1, 0, 8, 2)
```

Because permutations do not repeat elements, the letters automatically receive unique digits.

---

# Why Are There 8 Variables?

The equation contains these unique letters:

```text
S E N D M O R Y
```

Counting them:

```text
S → 1
E → 2
N → 3
D → 4
M → 5
O → 6
R → 7
Y → 8
```

Therefore, the program needs to assign **8 different digits**.

---

# Search Space

There are 10 possible digits:

```text
0 to 9
```

and 8 different letters.

The number of possible assignments is:

```text
10P8
```

which is:

```text
10! / (10 - 8)!
```

```text
= 10! / 2!
```

```text
= 1,814,400
```

The program may therefore examine up to **1,814,400 possible assignments** before finding a solution in the worst case.

The leading-zero condition eliminates many invalid assignments early.

---

# Constraint Checking

The program checks two types of constraints.

### 1. Uniqueness Constraint

`permutations()` ensures that:

```text
S ≠ E ≠ N ≠ D ≠ M ≠ O ≠ R ≠ Y
```

More precisely, all eight assigned digits are pairwise different.

### 2. Arithmetic Constraint

The program checks:

```python
if SEND + MORE == MONEY:
```

Only assignments satisfying this equation are accepted.

---

# Why `continue` Is Used

Consider:

```python
if S == 0 or M == 0:
    continue
```

If either leading letter is zero, the current permutation is invalid.

`continue` immediately skips that permutation and moves to the next one.

For example:

```text
S = 0
M = 1
```

is rejected.

Instead of calculating:

```text
SEND + MORE
```

the program immediately tries another assignment.

This improves efficiency.

---

# CSP Components

| CSP Component               | Cryptarithmetic Problem                  |
| --------------------------- | ---------------------------------------- |
| **Variables**               | `S, E, N, D, M, O, R, Y`                 |
| **Domain**                  | Digits `0–9`                             |
| **Uniqueness Constraint**   | Every letter has a different digit       |
| **Leading Zero Constraint** | `S ≠ 0`, `M ≠ 0`                         |
| **Arithmetic Constraint**   | `SEND + MORE = MONEY`                    |
| **Solution**                | `S=9, E=5, N=6, D=7, M=1, O=0, R=8, Y=2` |

---

# Advantages

* Simple to implement.
* Easy to understand.
* Uses permutations to guarantee unique digit assignments.
* Automatically checks all possible assignments.
* Suitable for small cryptarithmetic problems.

---

# Limitations

* Brute-force search can become expensive as the number of unique letters increases.
* Large cryptarithmetic problems may have a very large search space.
* The program does not use advanced constraint propagation.
* It may evaluate many invalid possibilities before finding a solution.

More advanced CSP techniques include:

* Backtracking
* Forward Checking
* Constraint Propagation
* Arc Consistency
* MRV (Minimum Remaining Values)
* Least Constraining Value

---

# Complexity Analysis

For `N` unique letters selected from 10 digits, the number of possible assignments is:

```text
10PN = 10! / (10 - N)!
```

For this problem:

```text
N = 8
```

Therefore:

```text
10P8 = 1,814,400
```

For each assignment, constructing and checking the three numbers takes constant time because the number of digits is fixed.

Thus, the brute-force search is approximately:

```text
O(10P8)
```

---

# Key Concepts

| Concept                        | Meaning                                                     |
| ------------------------------ | ----------------------------------------------------------- |
| **Cryptarithmetic**            | Puzzle where letters represent digits                       |
| **CSP**                        | Problem involving variables, domains, and constraints       |
| **Variable**                   | Letter whose value must be determined                       |
| **Domain**                     | Set of possible values for a variable                       |
| **Constraint**                 | Rule restricting possible assignments                       |
| **Permutation**                | Arrangement of unique elements                              |
| **Leading Zero**               | Zero cannot appear at the beginning of a multi-digit number |
| **Backtracking**               | Returning to an earlier choice when a constraint fails      |
| **Brute Force**                | Trying possible assignments until a valid solution is found |
| **`itertools.permutations()`** | Generates arrangements without repetition                   |

---

# Result

Thus, the **Cryptarithmetic Problem `SEND + MORE = MONEY`** was successfully solved as a **Constraint Satisfaction Problem (CSP)** using Python. The valid digit assignment was obtained as:

```text
SEND  = 9567
MORE  = 1085
MONEY = 10652
```

Hence:

```text
9567 + 1085 = 10652
```

and the cryptarithmetic puzzle was solved successfully.
