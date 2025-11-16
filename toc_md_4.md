Module 4: Pushdown Automata (PDA)** — a key topic that connects **finite automata** with **context-free grammars (CFGs)**.
Let’s break it down clearly and simply 👇

---

## 🧩 **What is a Pushdown Automaton (PDA)?**

A **Pushdown Automaton (PDA)** is like a **Finite Automaton (FA)** but with an extra memory structure — a **stack**.

👉 This makes PDA more powerful than FA and allows it to recognize **Context-Free Languages (CFLs)**.

---

### **Formal Definition**

A PDA is represented as a **7-tuple:**

```
M = (Q, Σ, Γ, δ, q₀, Z₀, F)
```

Where:

| Symbol | Meaning                                            |
| ------ | -------------------------------------------------- |
| **Q**  | Set of finite states                               |
| **Σ**  | Input alphabet                                     |
| **Γ**  | Stack alphabet (symbols that can be pushed/popped) |
| **δ**  | Transition function                                |
| **q₀** | Start state                                        |
| **Z₀** | Initial symbol on stack (bottom marker)            |
| **F**  | Set of final states                                |

---

### **Language Accepted by PDA**

Example from your notes:

```
L = { aⁿ bⁿ | n ≥ 0 }
```

✅ This is a **Context-Free Language** (CFL), recognized by PDA.

---

## 🧠 **Working of a PDA**

The PDA uses three things at any time:

1. **Current state**
2. **Current input symbol**
3. **Top of the stack**

It then decides:

* What new state to go to
* Whether to **push** or **pop** symbols on the stack.

---

### **Transition Function**

```
δ : Q × (Σ ∪ {ε}) × Γ → P(Q × Γ*)
```

This means:

* Current state ∈ Q
* Current input symbol ∈ Σ (or ε for empty input)
* Current stack top ∈ Γ
* Outputs: new state and new stack content (could be multiple possibilities)

---

## ⚙️ **Example Transition Explanation**

### Example 1:

```
δ(p, a, Z₀) = (q, aZ₀)
```

✅ Meaning:

* PDA is in **state p**.
* Input symbol **a** is being read.
* **Z₀** is on top of the stack.
* Then PDA goes to **state q**, and **pushes ‘a’** on top of the stack (so stack becomes `aZ₀`).

✅ Visually:

```
Before: [Z₀]
After:  [aZ₀]
```

So, it **pushes ‘a’** onto the stack.

---

### Example 2:

```
δ(p, a, Z₀) = (q, ε)
```

✅ Meaning:

* PDA is in **state p**, reads **a**, and **Z₀** is on top of the stack.
* It goes to **state q**, **removes Z₀** from the stack (because ε means nothing left).

✅ Visually:

```
Before: [Z₀]
After:  []
```

So, it **pops Z₀** (deletes it).

---

## 🧩 **Summary of Symbols**

| Symbol  | Represents                                |
| ------- | ----------------------------------------- |
| **p**   | Present state                             |
| **q**   | Next state                                |
| **a**   | Input symbol being read                   |
| **Z₀**  | Symbol at top of stack                    |
| **aZ₀** | New stack content (a pushed on top of Z₀) |
| **ε**   | Pop operation (remove top of stack)       |

---

## 🧠 **Key Idea**

* **Push** operation → adds symbol to the top of stack
* **Pop** operation → removes the top symbol
* PDA accepts input if:

  1. It reaches a **final state**, or
  2. The **stack becomes empty**

---

## ✅ **Takeaway**

| Concept       | Finite Automata | Pushdown Automata                      |         |          |
| ------------- | --------------- | -------------------------------------- | ------- | -------- |
| Memory        | No memory       | Has a stack (infinite memory in depth) |         |          |
| Language Type | Regular         | Context-Free                           |         |          |
| Example       | `{ aⁿbⁿ         | n≥0 }` ❌                               | `{ aⁿbⁿ | n≥0 }` ✅ |

---

## **1️⃣ Transition**

### δ(p, a, Z₀) = (q, γ)

👉 **Meaning:**
When PDA is in **state p**, and

* Reads the **input symbol ‘a’**
* **Top of stack = Z₀**

Then, PDA will:

* Move to **state q**
* Replace **Z₀** on the top of stack with **γ**

📘 Example:
If `γ = YZ₀`, that means PDA removes Z₀ and pushes Y, then Z₀ (so Y becomes top).

---

## **2️⃣ Transition**

### δ(p, ε, Z₀) = (q, γ)

👉 **Meaning:**
Here PDA reads **ε (empty input)** — that means it doesn’t consume any input symbol.

So:

* PDA is in **state p**,
* **Top of stack = Z₀**,
  Then it goes to **state q**,
  and **replaces Z₀ with γ**.

🧠 This is called an **ε-move (epsilon move)** — PDA changes its state or stack **without reading input**.

---

## **3️⃣ Two Ways PDA Can Accept a String**

Your notes show:

1. **PDA by empty stack** – Accepts when **stack becomes empty**.
2. **PDA by final state** – Accepts when it **reaches a final state**.

Both methods are valid; sometimes you’ll see both used in problems.

---

## **4️⃣ Transition**

### δ(p, ε, ε) = (q, Z₀)

👉 **Meaning:**
When PDA is in **state p**,
and **input is empty (ε)**,
and **stack is empty (ε)**,
then PDA goes to **state q**,
and **pushes Z₀** onto the stack.

🧠 Used when PDA starts working and needs to initialize stack.

---

## **5️⃣ Transition**

### δ(p, ε, Z₀) = (q, ε)

👉 **Meaning:**
When PDA is in **state p**,
reads **empty input (ε)**,
and **top of stack is Z₀**,
then it moves to **state q**
and **removes (pops) Z₀** from the stack.

So **Z₀ is deleted** from the stack.

📘 This happens when PDA is accepting by **empty stack** — when all input is processed and stack becomes empty.

---

## **💡 Summary Table (Easy Format)**

| Transition           | Reads Input  | Stack Action          | Description                     |
| -------------------- | ------------ | --------------------- | ------------------------------- |
| δ(p, a, Z₀) = (q, γ) | Reads `a`    | Replace `Z₀` with `γ` | Normal transition               |
| δ(p, ε, Z₀) = (q, γ) | No input (ε) | Replace `Z₀` with `γ` | Epsilon move                    |
| δ(p, ε, ε) = (q, Z₀) | No input     | Push `Z₀`             | Initialize stack                |
| δ(p, ε, Z₀) = (q, ε) | No input     | Pop `Z₀`              | Used for empty stack acceptance |

---

Perfect 👍
Let’s go over this page step-by-step in **simple and easy-to-understand words** — this page is about **constructing a PDA** for a specific language and understanding its transitions.

---

## 🧩 **1️⃣ Transition at the Top Left**

### δ(p, ε, Z₀) = (q, ε)

This means:

* PDA is in **state p**
* **Reads empty input (ε)**
* **Top of stack = Z₀**
* It moves to **state q**
* And **removes Z₀** from the stack

📘 **In diagram form** (drawn on the left):
An arrow from state **p → q** with label `ε, Z₀/ε` means:

> On reading ε (no input), and seeing Z₀ on the stack, pop Z₀ and move to q.

This usually represents **PDA acceptance by empty stack** — when the stack is empty, the PDA accepts the string.

---

## 🧩 **2️⃣ The Language Definition**

### L = { w c wʳ | w ∈ (a + b)* }

It means:

* The string starts with **some combination of a’s and b’s (that’s w)**
* Then there is a **single c** in the middle
* Then the **reverse of w (wʳ)** follows after c

✅ Examples:

* `aba c aba`
* `abb c bba`
* `a c a`
* `b c b`
* `c` (when w = ε)

So the language is **palindromic around the character ‘c’**.

---

## 🧠 **3️⃣ PDA Type**

Your notes say:
**“PDA by final state”**
That means the PDA **accepts when it reaches a final state**, not necessarily when the stack is empty.

---

## 🧩 **4️⃣ Symbols Used**

* **Σ (input symbols)** = {a, b, c}
* **Γ (stack symbols)** = {Z₀, a, b}

---

## 🧱 **5️⃣ Stack Working**

On the right side of the page, you drew the stack working idea:

For example:
When reading the first half `ababa`, PDA keeps **pushing each letter** (`a` or `b`) onto the stack.

Then, when it sees the middle `c`, it **switches to popping mode**, where it starts popping the stack as it reads the reverse half.

---

## 🧩 **6️⃣ Transitions**

Now, let’s go through the transitions written in your notes one by one 👇

| Transition               | Meaning in Simple Words                                        |
| ------------------------ | -------------------------------------------------------------- |
| δ(q₀, a, Z₀) = (q₀, aZ₀) | If input is `a` and top is Z₀, push `a` → stack becomes `aZ₀`. |
| δ(q₀, b, Z₀) = (q₀, bZ₀) | If input is `b` and top is Z₀, push `b`.                       |
| δ(q₀, a, a) = (q₀, aa)   | If reading `a` and top is `a`, push another `a`.               |
| δ(q₀, a, b) = (q₀, ab)   | If reading `a` and top is `b`, push `a`.                       |
| δ(q₀, b, a) = (q₀, ba)   | If reading `b` and top is `a`, push `b`.                       |
| δ(q₀, b, b) = (q₀, bb)   | If reading `b` and top is `b`, push `b`.                       |

📘 These transitions **keep pushing input letters (a or b)** onto the stack until the PDA reads **‘c’**.

After that, there will be another set of transitions (on next page probably) where PDA will **start popping** to match the reverse part of w.

---

## 💡 **7️⃣ Easy Understanding of PDA for L = {w c wʳ}**

1️⃣ **Before c:**
Push every symbol (`a` or `b`) onto stack.

2️⃣ **On reading c:**
Change to a new state (say `q1`) to start popping.

3️⃣ **After c:**
For every symbol read, pop the matching one from stack (a with a, b with b).

4️⃣ **Accept:**
When input is finished and either

* the stack is empty (**by empty stack**), or
* PDA reaches a final state (**by final state**, as in your notes).

---
Perfect 👍
Let’s explain this last part of your notes in **simple and clear words** — this page continues the **PDA construction for the language**

> **L = { w c wʳ | w ∈ (a + b)***

---

## 🧠 1️⃣ Recap of What PDA Does

This PDA works in **two phases**:

1. **Before ‘c’ (pushing phase)** – it **pushes** all symbols (`a` or `b`) of `w` onto the stack.
2. **After ‘c’ (popping phase)** – it **pops** the stack to check whether the second half of the input matches the reverse of the first half.

---

## 📘 2️⃣ Transition When PDA Reads ‘c’

### δ(q₀, c, Z₀) = (q₁, Z₀)

This means:

* PDA is in **state q₀**,
* Reads the middle symbol `c`,
* Stack top is `Z₀`,
* It moves to **state q₁** and keeps `Z₀` as it is.

🧩 This marks the **switch from pushing phase (q₀)** → **popping phase (q₁)**.

---

## 💡 3️⃣ If w = ε (empty string)

That means the string is just `c`.
Then the transition still works:

* PDA reads `c` in q₀,
* Goes to q₁ with stack unchanged (`Z₀`),
* So it will accept by final state.

---

## 📘 4️⃣ Transition While Popping

Once PDA is in **state q₁**, it will start matching each input symbol after `c` with the top of the stack:

| Transition            | Meaning                                     |
| --------------------- | ------------------------------------------- |
| δ(q₁, a, a) = (q₁, ε) | If the input is `a` and top is `a`, pop it. |
| δ(q₁, b, b) = (q₁, ε) | If the input is `b` and top is `b`, pop it. |

🧠 Each of these transitions **removes (pops)** one matching symbol from the stack.

---

## ⚙️ 5️⃣ Example Explained (on the right page diagram)

For example,
String = `abbc bba`
→ Here `w = abb`, `c` in middle, and `wʳ = bba`.

Steps:

1. Start in `q₀`

   * Read `a` → push `a`
   * Read `b` → push `b`
   * Read `b` → push `b`
2. Read `c` → move to `q₁` (no change in stack)
3. In `q₁`:

   * Read `b` → pop `b`
   * Read `b` → pop `b`
   * Read `a` → pop `a`

Stack returns to `Z₀` → **string accepted** ✅

---

## 📘 6️⃣ Final Transition (Acceptance)

### δ(q₁, ε, Z₀) = (q₂, Z₀)

→ When no input is left (ε) and stack has only Z₀ left, PDA moves to **final state q₂**.

That means PDA **accepts by final state** (since your notes mention *“PDA by final state”*).

---

## 💡 7️⃣ Summary of All Transitions

| Step | Transition               | Meaning                        |
| ---- | ------------------------ | ------------------------------ |
| 1    | δ(q₀, a, Z₀) = (q₀, aZ₀) | Push `a`                       |
| 2    | δ(q₀, b, Z₀) = (q₀, bZ₀) | Push `b`                       |
| 3    | δ(q₀, a, a) = (q₀, aa)   | Push `a` on top of `a`         |
| 4    | δ(q₀, a, b) = (q₀, ab)   | Push `a` on top of `b`         |
| 5    | δ(q₀, b, a) = (q₀, ba)   | Push `b` on top of `a`         |
| 6    | δ(q₀, b, b) = (q₀, bb)   | Push `b` on top of `b`         |
| 7    | δ(q₀, c, Z₀) = (q₁, Z₀)  | On `c`, switch to popping mode |
| 8    | δ(q₁, a, a) = (q₁, ε)    | Pop matching `a`               |
| 9    | δ(q₁, b, b) = (q₁, ε)    | Pop matching `b`               |
| 10   | δ(q₁, ε, Z₀) = (q₂, Z₀)  | Accept by final state          |

---

## ✅ **Final Concept**

This PDA **checks for symmetry around the middle ‘c’**:

* Everything before `c` is pushed,
* Everything after `c` must match and pop,
* If stack and input both end correctly → **string accepted**.

---
Perfect 👍
This page combines **two different PDAs** — one for a *new language* and another for explaining **Instantaneous Description (ID)**.
Let’s go through each part in **simple and clear words** 👇

---

## 🧠 **1️⃣ PDA for the Language**

### ( L = { a^n b^n ;|; n \ge 1 } )

That means:

* Equal number of `a`’s and `b`’s
* All `a`’s come first, then all `b`’s
  ✅ Examples: `ab`, `aabb`, `aaabbb`

---

### **Input and Stack Alphabets**

* Input symbols: **Σ = {a, b}**
* Stack symbols: **Γ = {a, b, Z₀}**

  * `Z₀` → Initial symbol in stack (bottom marker)

---

### **Language Pattern**

String **starts with a**
String **ends with b**

🧩 Example shown in notes:

```
aabb
aaabbb
```

---

### **Transitions Explained**

| Transition               | Meaning                                                           |
| ------------------------ | ----------------------------------------------------------------- |
| δ(q₀, a, Z₀) = (q₀, aZ₀) | If reading `a` and stack top is `Z₀`, push `a`                    |
| δ(q₀, a, a) = (q₀, aa)   | If reading another `a`, push one more `a` on top                  |
| δ(q₀, b, a) = (q₁, ε)    | On seeing first `b`, pop one `a` (switch to popping mode, q₁)     |
| δ(q₁, b, a) = (q₁, ε)    | For each `b`, pop a matching `a`                                  |
| δ(q₁, ε, Z₀) = (q₂, Z₀)  | When input is finished and only Z₀ remains, accept by final state |

---

### **📘 Step-by-Step Example**

Let’s take **aabb**:

1️⃣ Start:
`q₀` — Read `a`, push onto stack → Stack: `aZ₀`
`q₀` — Read next `a`, push again → Stack: `aaZ₀`

2️⃣ Then comes `b`:
`q₀ → q₁` (switch to popping mode)
Pop one `a` for each `b`

After second `b`, stack becomes only `Z₀`.

3️⃣ No input left → move to `q₂` → ✅ **Accepted**

---

### **Visual Diagram Summary**

```
(q₀) --a, Z₀/aZ₀--> (q₀)
(q₀) --a, a/aa--> (q₀)
(q₀) --b, a/ε--> (q₁)
(q₁) --b, a/ε--> (q₁)
(q₁) --ε, Z₀/Z₀--> (q₂)
```

---

## 🧩 **2️⃣ ID – Instantaneous Description**

### **Definition**

If
( M = (Q, Σ, Γ, δ, q₀, Z₀, F) )
is a PDA, then an **Instantaneous Description (ID)** is represented as:

```
(q, w, α)
```

Where:

* **q** → current state
* **w** → input string still to be read
* **α** → current contents of the stack

---

### **Explanation in Simple Words**

It shows **the current situation** of the PDA:

* What **state** it is in
* What **input remains** to be processed
* What’s currently **inside the stack**

---

### **Example**

Suppose PDA is in:

```
(q₀, abb, aZ₀)
```

That means:

* PDA is in state **q₀**
* Input **abb** is yet to be read
* Stack has **a** on top and **Z₀** at the bottom

---

### **Stack Rule Note in Your Page**

> “The leftmost symbol in α is the top of the stack, and the rightmost symbol is the bottom.”

So if stack = `aZ₀`
→ `a` is **top**,
→ `Z₀` is **bottom**.

---

✅ **In short:**

* PDA reads input left to right.
* Stack top is leftmost in α.
* IDs help describe every **step** PDA takes while reading a string.

---
Perfect 👍
This page combines **two different PDAs** — one for a *new language* and another for explaining **Instantaneous Description (ID)**.
Let’s go through each part in **simple and clear words** 👇

---

## 🧠 **1️⃣ PDA for the Language**

### ( L = { a^n b^n ;|; n \ge 1 } )

That means:

* Equal number of `a`’s and `b`’s
* All `a`’s come first, then all `b`’s
  ✅ Examples: `ab`, `aabb`, `aaabbb`

---

### **Input and Stack Alphabets**

* Input symbols: **Σ = {a, b}**
* Stack symbols: **Γ = {a, b, Z₀}**

  * `Z₀` → Initial symbol in stack (bottom marker)

---

### **Language Pattern**

String **starts with a**
String **ends with b**

🧩 Example shown in notes:

```
aabb
aaabbb
```

---

### **Transitions Explained**

| Transition               | Meaning                                                           |
| ------------------------ | ----------------------------------------------------------------- |
| δ(q₀, a, Z₀) = (q₀, aZ₀) | If reading `a` and stack top is `Z₀`, push `a`                    |
| δ(q₀, a, a) = (q₀, aa)   | If reading another `a`, push one more `a` on top                  |
| δ(q₀, b, a) = (q₁, ε)    | On seeing first `b`, pop one `a` (switch to popping mode, q₁)     |
| δ(q₁, b, a) = (q₁, ε)    | For each `b`, pop a matching `a`                                  |
| δ(q₁, ε, Z₀) = (q₂, Z₀)  | When input is finished and only Z₀ remains, accept by final state |

---

### **📘 Step-by-Step Example**

Let’s take **aabb**:

1️⃣ Start:
`q₀` — Read `a`, push onto stack → Stack: `aZ₀`
`q₀` — Read next `a`, push again → Stack: `aaZ₀`

2️⃣ Then comes `b`:
`q₀ → q₁` (switch to popping mode)
Pop one `a` for each `b`

After second `b`, stack becomes only `Z₀`.

3️⃣ No input left → move to `q₂` → ✅ **Accepted**

---

### **Visual Diagram Summary**

```
(q₀) --a, Z₀/aZ₀--> (q₀)
(q₀) --a, a/aa--> (q₀)
(q₀) --b, a/ε--> (q₁)
(q₁) --b, a/ε--> (q₁)
(q₁) --ε, Z₀/Z₀--> (q₂)
```

---

## 🧩 **2️⃣ ID – Instantaneous Description**

### **Definition**

If
( M = (Q, Σ, Γ, δ, q₀, Z₀, F) )
is a PDA, then an **Instantaneous Description (ID)** is represented as:

```
(q, w, α)
```

Where:

* **q** → current state
* **w** → input string still to be read
* **α** → current contents of the stack

---

### **Explanation in Simple Words**

It shows **the current situation** of the PDA:

* What **state** it is in
* What **input remains** to be processed
* What’s currently **inside the stack**

---

### **Example**

Suppose PDA is in:

```
(q₀, abb, aZ₀)
```

That means:

* PDA is in state **q₀**
* Input **abb** is yet to be read
* Stack has **a** on top and **Z₀** at the bottom

---

### **Stack Rule Note in Your Page**

> “The leftmost symbol in α is the top of the stack, and the rightmost symbol is the bottom.”

So if stack = `aZ₀`
→ `a` is **top**,
→ `Z₀` is **bottom**.

---

✅ **In short:**

* PDA reads input left to right.
* Stack top is leftmost in α.
* IDs help describe every **step** PDA takes while reading a string.

---
Excellent 👍
This page explains **how PDA configurations (Instantaneous Descriptions)** work and shows an **example step-by-step simulation** of a valid string (`aaabbb`) for the language **L = { aⁿbⁿ | n ≥ 1 }**.
Let’s go through it in **very simple and clear words** 👇

---

## 🧠 1️⃣ **Understanding PDA Configuration**

The **current configuration** of a PDA is written as:

```
(q, aw, Zα)
```

Where:

* **q** → current state
* **aw** → remaining input string to be processed
* **Zα** → current stack contents (Z = top of the stack)

📘 Example:
`(q0, aabb, Z0)` means:

* PDA is in state `q0`
* Input string left to read = `aabb`
* Stack currently has `Z0` (initial symbol) at the bottom

---

## ⚙️ 2️⃣ **Transition Rule**

If there is a transition

```
δ(q, a, Z) = (p, β)
```

then the PDA moves from:

```
(q, aω, Zα)
```

to

```
(p, ω, βα)
```

✅ Meaning:

* PDA reads `a` from input (so it is removed from the input part)
* Replaces the top stack symbol `Z` with `β`
* Goes to new state `p`

---

### **Notation Used**

The movement between configurations is shown as:

```
⊢
```

which means **“yields in one move.”**

If there are **zero or more moves**, it is written as:

```
⊢*
```

---

## 🧩 3️⃣ **Example: Valid String – `aaabbb`**

Language: L = { aⁿbⁿ | n ≥ 1 }

---

### **Initial Configuration**

```
(q0, aaabbb, Z0)
⊢ (q0, aabbb, aZ0)
```

→ PDA reads the first `a` and pushes `a` onto the stack.

---

### **Next Moves**

| Step         | Action               | Configuration    |
| ------------ | -------------------- | ---------------- |
| δ(q0, a, Z0) | Push a               | (q0, aabbb, aZ0) |
| δ(q0, a, a)  | Push a               | (q0, abbb, aaZ0) |
| δ(q0, a, a)  | Push a               | (q0, bbb, aaaZ0) |
| δ(q0, b, a)  | Pop a (switch to q1) | (q1, bb, aaZ0)   |
| δ(q1, b, a)  | Pop a                | (q1, b, aZ0)     |
| δ(q1, b, a)  | Pop a                | (q1, ε, Z0)      |
| δ(q1, ε, Z0) | Accept               | (q2, ε, Z0)      |

✅ **Final Configuration:**

```
(q2, ε, Z0)
```

No input left + in final state → **String Accepted!**

---

## 💡 4️⃣ **Meaning in Words**

1️⃣ PDA starts in state `q0` with empty stack (just Z0).
2️⃣ It reads `a`s and pushes each onto the stack.
3️⃣ When it starts reading `b`s, it switches to popping mode (state `q1`).
4️⃣ For each `b`, one `a` is popped.
5️⃣ If stack returns to Z0 and no input remains, PDA accepts the string.

---

## ✅ **Summary**

| Symbol                | Meaning                  |
| --------------------- | ------------------------ |
| `⊢`                   | One move (derives)       |
| `⊢*`                  | Zero or more moves       |
| `(q, aw, Zα)`         | PDA configuration        |
| `δ(q, a, Z) = (p, β)` | Transition rule          |
| Final configuration   | `(qf, ε, Z0)` → Accepted |

---
Perfect 👍
This page continues your **PDA working example** for the language:

> **L = { w c wʳ | w ∈ (a + b)* }**

and shows the **Instantaneous Description (ID) sequence** for the string **bababc babab**, i.e.,
`w = babab`, `c` is the middle symbol, and `wʳ = babab`.

Let’s explain everything in very **simple and clear words 👇**

---

## 🧠 1️⃣ Language Recap

**L = { w c wʳ | w ∈ (a + b)* }**

This means:

* String is split into three parts:
  **w**, **c**, **reverse of w**
* Example valid strings:

  * `aca`
  * `abbc bba`
  * `babc bab`
  * `babab c babab`

So your example `babab c babab` ✅ **belongs to this language.**

---

## ⚙️ 2️⃣ PDA Concept Recap

### PDA works in 3 phases:

1️⃣ **State q₀ (push mode)**
Push all letters of `w` (before `c`) into stack.

2️⃣ **On reading ‘c’**
Switch to state **q₁** (pop mode).

3️⃣ **State q₁ (pop mode)**
For every symbol after `c`, PDA pops and matches it with the stack top.

If all symbols are matched and only Z₀ remains → **accepted**.

---

## 🧩 3️⃣ PDA Example Execution

### Input string:

```
babab c babab
```

### Initial configuration:

```
(q₀, bababc babab, Z₀)
```

---

### Step-by-step ID sequence:

| Step | Action             | Configuration          |
| ---- | ------------------ | ---------------------- |
| 1    | Read `b`, push `b` | (q₀, ababc babab, bZ₀) |
| 2    | Read `a`, push `a` | (q₀, babc babab, abZ₀) |
| 3    | Read `b`, push `b` | (q₀, abc babab, babZ₀) |
| 4    | Read `a`, push `a` | (q₀, bc babab, ababZ₀) |
| 5    | Read `b`, push `b` | (q₀, c babab, bababZ₀) |

At this point, the **first half (w)** is done, and **stack = w**.

---

### Now reading middle `c`:

```
(q₀, c babab, bababZ₀)
⊢ (q₁, babab, bababZ₀)
```

→ PDA moves to **q₁** (pop mode). Stack unchanged.

---

### Matching phase (after c):

| Step | Input | Stack top | Action |
| ---- | ----- | --------- | ------ |
| 1    | `b`   | `b`       | pop    |
| 2    | `a`   | `a`       | pop    |
| 3    | `b`   | `b`       | pop    |
| 4    | `a`   | `a`       | pop    |
| 5    | `b`   | `b`       | pop    |

After popping all → stack = `Z₀`.

---

### Final configuration:

```
(q₁, ε, Z₀)
⊢ (q₂, ε, Z₀)
```

✅ **String accepted by final state (or empty stack).**

---

## 💡 4️⃣ Summary of What Happens

1️⃣ PDA starts in `q₀`, pushes every symbol of `w` into stack.
2️⃣ When it reads `c`, it switches to `q₁`.
3️⃣ Then for each symbol after `c`, it pops and matches the stack top.
4️⃣ When both input and stack are empty (except Z₀), PDA accepts.

---

### ✅ Final Note

Your notebook’s right page is showing these **transitions and IDs** exactly:

* `(q₀, bababc babab, Z₀)`
* `(q₀, ababc babab, bZ₀)`
* `(q₀, babc babab, abZ₀)`
* `(q₀, c babab, bababZ₀)`
* `(q₁, babab, bababZ₀)`
* `(q₁, ababab, ababZ₀)`
* … until → `(q₂, ε, Z₀)` ✅ Accepted.

---
