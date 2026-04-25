# 🧅 Lovable Sahil Writeup

<p align="center">
  <img src="https://img.shields.io/badge/CATEGORY-REVERSE%20ENGINEERING%20%2F%20MISC-purple?style=for-the-badge">
  <img src="https://img.shields.io/badge/DIFFICULTY-MEDIUM-black?style=for-the-badge">
  <img src="https://img.shields.io/badge/TECHNIQUE-LAYERED%20OBFUSCATION-blue?style=for-the-badge">
  <img src="https://img.shields.io/badge/FOCUS-STATIC%20ANALYSIS-green?style=for-the-badge">
</p>

---

## 📜 Challenge Description

They handed us a black box with a single button that says "RUN".  
But if you press it, the evidence burns itself.

Your job isn't to play their game.  
Your job is to catch whatever falls out the back right before the machine tries to start.

Flag format: geek{...}

---

## 🔍 Initial Analysis

Observations from onion.py:

- Contains large encoded payload  
- Uses:
  - base64 decoding  
  - zlib decompression  
- Final execution via exec  

Pattern:

exec(zlib.decompress(base64.b64decode(payload)).decode())

➡️ Indicates **multi-layer packed script (onion style)**  

---

## 🧠 Step 1: Key Insight

Hint suggests:

"catch whatever falls out the back before the machine tries to start"

➡️ Do NOT execute the code  
➡️ Instead, print decoded layers  

---

## 🔧 Step 2: First Layer Extraction

Modified code:

print(zlib.decompress(base64.b64decode(payload)).decode())

➡️ Reveals next layer  

---

## ⚡ Step 3: XOR Obfuscation Layer

Next layer contains:

secret_key = 42  
payload = b'...'  
decrypted = "".join(chr(b ^ secret_key) for b in payload)  

➡️ Simple XOR encryption  

---

## 🔓 Step 4: Decryption

Script used:

secret_key = 42  
decrypted = "".join(chr(b ^ secret_key) for b in payload)  
print(decrypted)  

➡️ Reveals validation logic  

---

## 🧠 Step 5: Validation Logic

Condition observed:

(ord(user_input[i]) ^ i) == targets[i]

➡️ Input is validated character by character  

---

## 🔁 Step 6: Reverse Logic

Rearranging:

user_input[i] = chr(targets[i] ^ i)

➡️ Direct reconstruction possible  

---

## 🧪 Step 7: Final Solver

targets = [103, 100, 103, 104, 127, 112, 104, 119, 60, 106, 97, 110, 104, 112]  

flag = ''.join(chr(t ^ i) for i, t in enumerate(targets))  

print(flag)  

---

## 🎯 Output

geek{unp4cked}

---

## 🏁 Final Flag

geek{unp4cked}

---

## 🧠 Key Takeaways

- Never blindly execute unknown code  
- Layered obfuscation often uses:
  - base64  
  - compression  
  - XOR  
- Static analysis is safer and faster  
- Validation checks can be reversed mathematically  
- Onion-style challenges require step-by-step peeling  

---

## 🛠 Tools Used

- Python3  
- Manual code analysis  

---

## 🏁 Conclusion

This challenge demonstrates layered obfuscation techniques combined with simple cryptographic logic. By avoiding execution and instead decoding step-by-step, the hidden validation logic was reversed and the flag recovered.

---

<p align="center">
  ⭐ If you found this helpful, consider starring the repo!
</p>
