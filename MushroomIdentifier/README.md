# Mushroom Identifier

A Java console program that works out which mushroom the user is thinking of by asking **at most three** yes/no questions.

This version uses **decision control statements** (nested `if / else`) to identify the mushroom, and **loops** to check the answers and to let the user play again.

---

## Problem Description

The user secretly thinks of one of these six mushrooms:

- Agaric jaunissant
- Amanite tue-mouche
- Cepe de bordeaux
- Coprin chevelu
- Girolle
- Pied bleu

The program asks yes/no questions chosen from these four:

1. Does your mushroom have gills?
2. Does your mushroom grow in a forest?
3. Does your mushroom have a ring?
4. Does your mushroom have a convex cup?

The user answers truthfully, and the program must name the mushroom after asking **no more than three** of the four questions.

### What we know about each mushroom

| Mushroom | Gills | Grows in forest | Ring | Convex cup |
|---|---|---|---|---|
| Agaric jaunissant | yes | no (meadow) | yes | yes |
| Amanite tue-mouche | yes | yes | yes | yes |
| Cepe de bordeaux | no (pores) | yes | no | no |
| Coprin chevelu | yes | no (meadow) | yes | no |
| Girolle | yes | yes | no | no |
| Pied bleu | yes | yes | no | yes |

---

## Solution Design

### Why the first question is "ring"

If the program started with "gills?" and then "forest?", three mushrooms would still be left in the forest group, and a fourth question would be needed. Asking about the **ring** first splits the six mushrooms into two groups of three, and each group can then be separated with two more questions.

- **Ring = yes:** Agaric jaunissant, Amanite tue-mouche, Coprin chevelu
- **Ring = no:** Cepe de bordeaux, Girolle, Pied bleu

### Decision tree

```
Has a ring?
├── yes → Grows in a forest?
│         ├── yes → Amanite tue-mouche
│         └── no  → Convex cup?
│                   ├── yes → Agaric jaunissant
│                   └── no  → Coprin chevelu
└── no  → Has gills?
          ├── no  → Cepe de bordeaux
          └── yes → Convex cup?
                    ├── yes → Pied bleu
                    └── no  → Girolle
```

Every path through the tree uses 3 questions or fewer.

---

## How It Works

1. The program lists the six mushrooms and explains how to answer.
2. It asks the first question: "Does your mushroom have a ring?"
3. Depending on each answer, it follows the decision tree, asking the next question.
4. When only one mushroom is possible, it prints the name.
5. It asks whether the user wants to identify another mushroom, and repeats if the answer is yes.

### Where loops are used

- **Answer checking:** the `askYesNo` method uses a `while` loop that keeps asking until the user types exactly `yes` or `no`.
- **Playing again:** a `do-while` loop repeats the whole game while the user answers `yes`.

```java
static String askYesNo(Scanner input, String question) {
    while (true) {
        System.out.print(question + " (yes/no): ");
        String answer = input.next().toLowerCase();
        if (answer.equals("yes") || answer.equals("no")) {
            return answer;
        }
        System.out.println("Please answer with yes or no.");
    }
}
```

---

## Concepts Used

- **Variables and data types:** `String` for the answers
- **Operators:** comparison with `equals`, logical `||`
- **Decision control statements:** nested `if / else`
- **Repetition statements:** `while` and `do-while` loops
- **Methods:** a small helper method, `askYesNo`
- **Input and output:** `Scanner`, `System.out.println`

---

## Requirements

- Java Development Kit (JDK) 8 or later
- An IDE such as NetBeans, or a command line

---

## How to Run

### In NetBeans

1. Open `MushroomIdentifierLoop.java` in your project.
2. Make sure the first line matches your project package, for example `package com.mycompany.mushroom;`. Add it if it is missing.
3. Click **Run** and type your answers in the Output window.

### From the command line

```bash
javac MushroomIdentifierLoop.java
java MushroomIdentifierLoop
```

---

## Sample Runs

### Example 1: Girolle

```
Does your mushroom have a ring? (yes/no): no
Does your mushroom have gills? (yes/no): yes
Does your mushroom have a convex cup? (yes/no): no
Your mushroom is: Girolle
```

### Example 2: Amanite tue-mouche (only two questions needed)

```
Does your mushroom have a ring? (yes/no): yes
Does your mushroom grow in a forest? (yes/no): yes
Your mushroom is: Amanite tue-mouche
```

### Example 3: invalid answer

```
Does your mushroom have a ring? (yes/no): maybe
Please answer with yes or no.
Does your mushroom have a ring? (yes/no): no
```

---

## Test Cases

| Answers (in order asked) | Expected result |
|---|---|
| ring: yes, forest: yes | Amanite tue-mouche |
| ring: yes, forest: no, cup: yes | Agaric jaunissant |
| ring: yes, forest: no, cup: no | Coprin chevelu |
| ring: no, gills: no | Cepe de bordeaux |
| ring: no, gills: yes, cup: yes | Pied bleu |
| ring: no, gills: yes, cup: no | Girolle |

---

## Files

| File | Description |
|---|---|
| `MushroomIdentifierLoop.java` | Main program (decisions plus loops) |
| `MushroomIdentifier.java` | Simpler version using decisions only |
| `README_Mushroom.md` | This documentation |
