# 🧟 Zombie Generator – Writeup

<p align="center">
  <img src="https://img.shields.io/badge/CATEGORY-CRYPTO%20%2F%20MISC-purple?style=for-the-badge">
  <img src="https://img.shields.io/badge/DIFFICULTY-HARD-black?style=for-the-badge">
  <img src="https://img.shields.io/badge/TECHNIQUE-CYCLIC%20GROUPS-blue?style=for-the-badge">
  <img src="https://img.shields.io/badge/FOCUS-PERMUTATION%20CIPHER-green?style=for-the-badge">
</p>

---


## 📜 Challenge Description

In every circle of life, there's always that one spark that keeps everyone moving.  
Good Luck!

Given string:

0eRbrk{_ng}eoe3Z|aEm1g

Flag format: geek{...}

---

## 🔍 Initial Analysis

Observations:

- Contains `{`, `}`, `_` → likely already flag characters  
- Mixed casing + numbers → not simple substitution  
- Structure resembles shuffled flag  

➡️ Indicates **reordering (permutation)** rather than encoding  

---

## 🧠 Step 1: Understanding the Hint

Key phrases:

- "circle of life" → cyclic structure  
- "one spark" → generator  

➡️ Strong hint toward **cyclic groups and generators**

---

## 🔢 Step 2: Mathematical Insight

- Length of string = 22  
- 23 is prime  
- Multiplicative group mod 23 has size 22  

➡️ Perfect match  

So we consider:

Multiplicative group modulo 23 → cyclic group of order 22  

---

## ⚙️ Step 3: Generator-Based Permutation

Choose generator:

g = 7 (primitive root mod 23)

Generate sequence:

Start from 1  
Multiply by 7 mod 23 repeatedly  

Sequence covers all positions (1–22) exactly once  

➡️ Produces a full cyclic permutation  

---

## 🔁 Step 4: Reordering Characters

Use generated sequence as indices to reorder:

0eRbrk{_ng}eoe3Z|aEm1g

Apply permutation → reconstruct original ordering  

---

## 🎯 Decoded Output

geek{Z0mb1E_g3nera|oR}

---

## 🏁 Final Flag

geek{Z0mb1E_g3nera|oR}

---

## 🧠 Key Takeaways

- Not all ciphers modify characters — some **reorder them**  
- Cyclic groups are powerful for generating permutations  
- Prime modulus often indicates group theory usage  
- Generators can traverse entire sets without repetition  
- Challenge hints often directly point to mathematical concepts  

---

## 🛠 Tools Used

- Python (for permutation testing)  
- Manual mathematical reasoning  

---

## 🏁 Conclusion

This challenge used a permutation cipher based on cyclic group theory. By interpreting the hints correctly and recognizing the significance of the string length, we applied a generator modulo 23 to reconstruct the original ordering of characters and recover the flag.

---

<p align="center">
  ⭐ If you found this helpful, consider starring the repo!
</p>
