# ⛏️ Blockchain Mining – Writeup

<p align="center">
  <img src="https://img.shields.io/badge/CATEGORY-CRYPTO%20%2F%20MISC-purple?style=for-the-badge">
  <img src="https://img.shields.io/badge/DIFFICULTY-EASY-black?style=for-the-badge">
  <img src="https://img.shields.io/badge/TECHNIQUE-PROOF%20OF%20WORK-blue?style=for-the-badge">
  <img src="https://img.shields.io/badge/FOCUS-NONCE%20BRUTEFORCE-green?style=for-the-badge">
</p>

---

## 📜 Challenge Description

"You think you can mine? Everyone loves blockchain until they have to do the work."

We are given:

- Block Number: 1  
- Nonce (incorrect): 49051  
- Data: you think you can mine?  
- Hash: b4dd1133c58dd0cf8acd0445f1935d610d7e81df16b8082acb596d7f95674f01  

Goal:

Find a nonce such that the SHA-256 hash starts with:

0000b19ca...

Flag format: geek{...}

---

## 🔍 Initial Analysis

Observations:

- Given nonce does not produce valid hash  
- Hash must start with 0000  
- Classic Proof-of-Work condition  

➡️ Indicates **blockchain mining simulation**

---

## 🧠 Step 1: Understanding PoW

- Nonce is adjusted until hash meets difficulty  
- Difficulty = prefix condition (0000)  
- Similar to real blockchain mining  

---

## 🔧 Step 2: Reconstruct Hash Function

Hash format:

SHA256(BlockNumber + Nonce + Data)

Constructed input:

"1" + str(nonce) + "you think you can mine?"

Verification:

SHA256("149051you think you can mine?")  
→ b4dd1133c58dd0cf8acd0445f1935d610d7e81df16b8082acb596d7f95674f01  

➡️ Matches given hash  

---

## ⚡ Step 3: Brute Force Nonce

Approach:

- Start nonce from 0  
- Compute SHA256  
- Check prefix  
- Stop when condition satisfied  

---

## 🧪 Step 4: Python Script

import hashlib

block_number = "1"  
data = "you think you can mine?"  

nonce = 0  

while True:  
    text = block_number + str(nonce) + data  
    hash_result = hashlib.sha256(text.encode()).hexdigest()  

    if hash_result.startswith("0000"):  
        print("Nonce:", nonce)  
        print("Hash:", hash_result)  
        break  

    nonce += 1  

---

## 🎯 Solution

Result:

Nonce: 6342  
Hash: 0000291b503d18b1b226acfa207d04eebcebabf00d85fca6b72a4c39244f51f3  

➡️ Satisfies condition  

---

## 🏁 Final Flag

geek{6342}

---

## 🧠 Key Takeaways

- Proof-of-Work relies on brute-force nonce search  
- Small difficulty (0000) still requires many attempts  
- Hash input structure must be correct  
- Even simple PoW teaches real blockchain concepts  

---

## 🛠 Tools Used

- Python  
- hashlib  

---

## 🏁 Conclusion

This challenge simulates blockchain mining by requiring a valid nonce that satisfies a hash difficulty condition. By reconstructing the hash format and brute-forcing the nonce, we successfully found the correct value.

---

<p align="center">
  ⭐ If you found this helpful, consider starring the repo!
</p>
