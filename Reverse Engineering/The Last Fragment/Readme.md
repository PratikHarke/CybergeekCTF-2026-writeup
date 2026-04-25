# 🧠 The Last Fragment Writeup 

<p align="center">
  <img src="https://img.shields.io/badge/Category-Reverse%20Engineering-red?style=for-the-badge">
  <img src="https://img.shields.io/badge/Difficulty-Hard-black?style=for-the-badge">
  <img src="https://img.shields.io/badge/Technique-Custom%20VM-blue?style=for-the-badge">
  <img src="https://img.shields.io/badge/Focus-Bitwise%20Reversal-green?style=for-the-badge">
</p>

---

## 📁 Files Included

- executor → Main binary  
- fragment.bin → VM instruction fragment  

---

## 📌 Challenge Overview

> Node B4 left this behind. We don't know how it works, but it requires both the executor and the fragment to run. Recover the original access key.

🎯 Goal: Find input that results in  
ACCESS GRANTED. Access key accepted.

Flag format: geek{...}

---

## ⚙️ Setup & Execution

Make executable:
chmod +x executor

Run:
./executor fragment.bin

---

## 🧩 Key Characteristics

- Dynamically linked binary  
- Not stripped → symbols available  
- Uses external file (fragment.bin)  
- Custom VM / bytecode interpreter  
- Input validation via transformation pipeline  

---

## 🔍 Step 1: Initial Analysis

Command:
file executor

Output:
ELF 64-bit LSB executable, dynamically linked, not stripped

Command:
file fragment.bin

Output:
data

Insights:
- Binary is easier to analyze due to symbols  
- fragment.bin is required → external execution logic  
- Strong indicator of VM-based design  

---

## 🔎 Step 2: Dynamic Behavior

Running:
./executor fragment.bin

Behavior:
- Prompts for input  
- Outputs either:
  - ACCESS DENIED  
  - ACCESS GRANTED  

---

## 🧠 Step 3: Reverse Engineering Strategy

Instead of guessing input:

- Analyze how fragment.bin is processed  
- Identify instruction execution loop  
- Reconstruct VM instruction set  
- Reverse transformation logic  

➡️ Goal: Recover transformation and invert it

---

## 🔬 Step 4: VM Analysis

Using Ghidra / IDA:

- fragment.bin is read into memory  
- Loop processes bytes sequentially  
- Each byte acts as an opcode  

---

## ⚙️ Step 5: Instruction Set Reconstruction

Recovered VM instructions:

0x71 → Read next input byte  
0x1A → Rotate left by 3 bits (ROL3)  
0x82 0x42 → XOR with 0x42  
0xFF → End execution  

---

## 🔁 Step 6: Transformation Logic

Each input byte x becomes:

ROL3(x) ^ 0x42

---

## 🎯 Step 7: Target Extraction

Binary compares transformed bytes with a fixed array.

Extracted via:
- strings executor  
- Disassembler memory inspection  

This array represents the expected transformed flag.

---

## 🔓 Step 8: Reverse Transformation

We invert the logic:

Step 1:
ROL3(x) = target ^ 0x42

Step 2:
x = ROR3(target ^ 0x42)

---

## 🧪 Step 9: Solver Logic

Python approach:

- Iterate over target bytes  
- Apply XOR inverse  
- Apply rotate-right  
- Convert to characters  

---

## 🎯 Final Flag

geek{vvirtual_m4ch1n3_m4st3r}

---

## 📊 Transformation Flow

Input → ROL3 → XOR 0x42 → Compare with target  

Reverse:

Target → XOR 0x42 → ROR3 → Original Input  

---

## 🧠 Key Takeaways

- Binary + external file → strong VM indicator  
- Opcode reconstruction is critical  
- Bitwise ops (ROL/ROR/XOR) are common obfuscation  
- Reversing transformations is often easier than emulating  
- Always inspect:
  - Interpreter loops  
  - Byte arrays  
  - Transformation chains  

---

## 🚀 Tools Used

- Ghidra / IDA Pro  
- strings  
- Python  

---

## 🏁 Conclusion

This challenge highlights how a simple byte transformation pipeline can be hidden behind a custom VM. By identifying opcode behavior and reversing the logic, we bypass execution entirely and recover the valid access key.

---

<p align="center">
  ⭐ If you found this helpful, consider starring the repo!
</p>
