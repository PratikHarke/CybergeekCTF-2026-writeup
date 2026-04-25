# 🔐 Weak RSA – Writeup

<p align="center">
  <img src="https://img.shields.io/badge/CATEGORY-CRYPTO-purple?style=for-the-badge">
  <img src="https://img.shields.io/badge/DIFFICULTY-EASY-black?style=for-the-badge">
  <img src="https://img.shields.io/badge/TECHNIQUE-RSA%20FACTORISATION-blue?style=for-the-badge">
  <img src="https://img.shields.io/badge/FOCUS-MODULAR%20ARITHMETIC-green?style=for-the-badge">
</p>

---

## 📁 Files Included

- challenge.txt → RSA parameters  

---

## 📜 Challenge Description

hope you know how to factorize numbers  

Some people use 2048-bit RSA.  

Others use:

n = 15  

Needless to say, their encryption didn't last very long.  

c = 0b1100  
(e, n) = (5, 15)  

Flag format: geek{...}

---

## 🔍 Initial Analysis

Observations:

- Extremely small modulus (n = 15)  
- Easy to factor  
- Classic weak RSA scenario  

➡️ Indicates **direct factorization attack**

---

## 🧠 Step 1: Factorization

n = 15  

15 = 3 × 5  

So:

p = 3  
q = 5  

---

## 🔢 Step 2: Compute Totient

φ(n) = (p - 1)(q - 1)  

φ(15) = (3 - 1)(5 - 1)  
φ(15) = 2 × 4 = 8  

---

## 🔑 Step 3: Find Private Key

We need:

e × d ≡ 1 (mod φ(n))  

5 × d ≡ 1 (mod 8)  

Testing:

5 × 5 = 25 ≡ 1 (mod 8)  

➡️ d = 5  

---

## 🔄 Step 4: Convert Ciphertext

c = 0b1100  

Binary → Decimal:

0b1100 = 12  

---

## ⚡ Step 5: Decryption

m = c^d mod n  

m = 12^5 mod 15  

Compute:

12² = 144 ≡ 9 (mod 15)  
12⁴ = 9² = 81 ≡ 6 (mod 15)  
12⁵ = 6 × 12 = 72 ≡ 12 (mod 15)  

➡️ m = 12  

---

## 🎯 Step 6: Output Format

- Plaintext = 12  
- Given ciphertext format = binary  

➡️ Final answer in binary  

---

## 🏁 Final Flag

geek{0b1100}

---

## 🧠 Key Takeaways

- Small RSA moduli are trivially breakable  
- Factorization completely breaks RSA security  
- Modular inverse is key to private key recovery  
- Always match output format (binary vs decimal)  
- Real RSA uses very large primes (2048-bit+)  

---

## 🛠 Tools Used

- Manual calculation  
- Basic number theory  

---

## 🏁 Conclusion

This challenge demonstrates how weak RSA parameters completely compromise security. By factoring the modulus and computing the private key, we successfully decrypted the ciphertext and recovered the flag.

---

<p align="center">
  ⭐ If you found this helpful, consider starring the repo!
</p>
