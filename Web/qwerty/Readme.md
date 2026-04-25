# 🕹️ qwerty Writeup

<p align="center">
  <img src="https://img.shields.io/badge/CATEGORY-WEB-purple?style=for-the-badge">
  <img src="https://img.shields.io/badge/DIFFICULTY-EASY-black?style=for-the-badge">
  <img src="https://img.shields.io/badge/TECHNIQUE-KEY%20SEQUENCE-blue?style=for-the-badge">
  <img src="https://img.shields.io/badge/FOCUS-JAVASCRIPT%20EVENTS-green?style=for-the-badge">
</p>

---

## 📜 Challenge Description

Some old machines only respond to the right rhythm.

Flag format: geek{...}

---

## 🔍 Initial Analysis

Observations:

- Webpage titled "Arcade Relic"  
- Robot present in center  
- Pressing any key triggers animation (hands/head movement)  
- Displays "System idle."  
- No visible input fields  

➡️ Indicates **keyboard-driven interaction**

---

## 🧠 Step 1: Understanding the Hint

Key phrase:

"right rhythm"

➡️ Suggests a **specific key sequence**

"old machines"

➡️ Points to **classic arcade references**

---

## 🎮 Step 2: Hypothesis

Most common hidden arcade input:

Konami Code

Sequence:

↑ ↑ ↓ ↓ ← → ← → B A

---

## ⌨️ Step 3: Testing Input

Entered sequence:

ArrowUp ArrowUp ArrowDown ArrowDown ArrowLeft ArrowRight ArrowLeft ArrowRight b a

➡️ Application responds  
➡️ Hidden function triggered  

---

## ⚙️ Step 4: Internal Behavior

From observation / DevTools:

- Page listens to keydown events  
- Maintains input buffer  
- Compares buffer with predefined sequence  
- On match → triggers hidden output  

➡️ Classic **sequence-matching logic**

---

## 🎯 Result

Correct sequence reveals the flag.

---

## 🏁 Final Flag

geek{k0h_nah_m3}

---

## 🧠 Key Takeaways

- Challenge hints often directly point to solution  
- "Old machines" → arcade references  
- "Rhythm" → input sequence  
- Web challenges may hide logic in:
  - Keyboard event listeners  
  - Input buffers  
  - JavaScript conditions  
- Konami Code is a common CTF pattern  

---

## 🛠 Tools Used

- Web browser (Chrome)  
- DevTools (optional)  

---

## 🏁 Conclusion

This challenge demonstrates how simple client-side logic can hide interactive secrets. Recognizing the reference to the Konami Code allowed quick identification of the correct sequence and retrieval of the flag.

---

<p align="center">
  ⭐ If you found this helpful, consider starring the repo!
</p>
