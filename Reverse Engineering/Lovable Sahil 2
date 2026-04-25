# 🧠 Funhouse VM Challenge Writeup

<p align="center">
  <img src="https://img.shields.io/badge/Category-Reverse%20Engineering-red?style=for-the-badge">
  <img src="https://img.shields.io/badge/Difficulty-Hard-black?style=for-the-badge">
  <img src="https://img.shields.io/badge/Technique-VM%20Obfuscation-blue?style=for-the-badge">
  <img src="https://img.shields.io/badge/Focus-Constraint%20Solving-green?style=for-the-badge">
</p>

---

## 📌 Challenge Overview

> “Welcome to the funhouse. The walls are shifting, the locks change every cycle, and your debuggers are going to lie to you. Brute force is a mathematical impossibility. You can't just read the code—you have to prove it.”

This challenge provides a statically linked, stripped ELF binary implementing heavy obfuscation using a custom VM-like logic.

🎯 Objective: Recover the correct input that satisfies the internal validation  
Flag format: geek{...}

---

## 🧩 Key Characteristics

- Statically linked binary  
- VM-based obfuscation  
- Anti-debugging behavior  
- Brute force infeasible  
- Requires mathematical reasoning  

---

## 🔍 Step 1: Initial Analysis

Command:
file chall

Output:
ELF 64-bit LSB executable, statically linked, stripped

Insights:
- No symbols → harder reverse engineering  
- Large binary → likely embedded VM  
- Static → all logic inside binary  

---

## 🔎 Step 2: String Recon

Command:
strings chall | grep -i correct

Output:
Correct! You survived the VM.

Insight:
- Confirms internal validation logic  
- No direct flag exposure  

---

## ⚙️ Step 3: Strategy

From challenge hints:

- “debuggers will lie” → avoid dynamic debugging  
- “brute force impossible” → constraints too large  
- “you have to prove it” → mathematical solution  

➡️ Approach: Extract constraints instead of executing the VM

---

## 🧠 Step 4: Reverse Engineering

Observed validation pattern:

(input[i] XOR input[i+1]) + 10 = constant

---

## 🔗 Step 5: Constraint Logic

Rewriting:

input[i] = (constant - 10) XOR input[i+1]

Using known prefix:

geek{...}

We validate:

- g ^ e = 2  
- e ^ e = 0  
- e ^ k = 14  
- k ^ { = 16  

This confirms correctness of extracted logic.

---

## 🔓 Step 6: Flag Reconstruction

By propagating the XOR constraints:

- Start from known prefix  
- Apply chained dependency  
- Recover full string  

Result:
geek{n0_m0r3_AI}

---

## 🎯 Final Flag

geek{n0_m0r3_AI}

---

## 📊 Constraint Visualization

c0 ⊕ c1 → k1  
c1 ⊕ c2 → k2  
c2 ⊕ c3 → k3  
...

Each character depends on the next, forming a chained system.

---

## 🧠 Key Takeaways

- VM obfuscation often hides simple mathematical logic  
- XOR chains create interdependent constraints  
- Known prefixes (geek{}) help anchor solutions  
- Static analysis is more reliable than debugging in anti-RE binaries  
- Many reverse engineering problems reduce to constraint solving  

---

## 🚀 Bonus: Automation

This solution can be automated using Python or Z3 by modeling XOR constraints.

---

## 🛠 Tools Used

- Ghidra / IDA Pro / radare2  
- strings  
- Linux CLI  
- Manual constraint solving  

---

## 🏁 Conclusion

This challenge demonstrates that complex VM-based obfuscation can be bypassed by identifying underlying mathematical relationships. Extracting constraints and solving them directly is far more efficient than emulating the VM.

---

<p align="center">
  ⭐ If you found this helpful, consider starring the repo!
</p>
