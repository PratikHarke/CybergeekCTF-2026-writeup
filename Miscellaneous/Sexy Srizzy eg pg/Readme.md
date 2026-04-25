# 💔 Sexy Srizzy eg pg Writeup

<p align="center">
  <img src="https://img.shields.io/badge/CATEGORY-MISC%20%2F%20STEGO-purple?style=for-the-badge">
  <img src="https://img.shields.io/badge/DIFFICULTY-EASY-black?style=for-the-badge">
  <img src="https://img.shields.io/badge/TECHNIQUE-IMAGE%20RECONSTRUCTION-blue?style=for-the-badge">
  <img src="https://img.shields.io/badge/FOCUS-DATA%20ORDERING-green?style=for-the-badge">
</p>

---

## 📁 Files Included

lol.zip

---

## 📜 Challenge Description

Broke my heart now keep arranging shards

Flag format: geek{...}

---

## 🔍 Initial Analysis

Observations after extraction:

- Large number of small BMP tiles  
- Filenames contain emoji sequences  
- Each tile appears to be part of a bigger image  

➡️ Indicates **fragmented image reconstruction challenge**

---

## 🧠 Step 1: Key Insight

Filenames are not random — they encode numbers using emojis  

➡️ Emoji-based numeric encoding  

---

## 🔢 Step 2: Emoji Mapping

🥹 → 0  
😀 → 1  
😁 → 2  
😂 → 3  
🤣 → 4  
😃 → 5  
😄 → 6  
😅 → 7  
😆 → 8  
😉 → 9  

---

## 🧩 Step 3: Reconstruction Logic

Process:

- Convert emoji filename → digits  
- Form integer index (0–255)  
- Map into 16 × 16 grid  

Position formula:

row = index // 16  
col = index % 16  

---

## ⚙️ Step 4: Image Reconstruction

Steps:

- Create blank canvas  
- Place each tile at calculated position  
- Ignore empty tiles  
- Merge all tiles  

---

## 🖼️ Step 5: Final Output

After reconstruction:

- Image becomes readable  
- Hidden flag appears clearly  

---

## 🎯 Result

geek{🍰💜}

---

## 🏁 Final Flag

geek{🍰💜}

---

## 🧠 Key Takeaways

- Filenames can carry encoded information  
- Emoji encoding is a creative obfuscation method  
- Image reconstruction often relies on correct ordering  
- Grid-based puzzles (16×16) are common in CTFs  
- Always analyze both metadata and structure  

---

## 🛠 Tools Used

- Python (PIL)  
- Manual mapping logic  

---

## 🏁 Conclusion

This challenge combines encoding and image reconstruction. By decoding emoji-based indices and correctly arranging the shards, the hidden image and flag were successfully recovered.

---

<p align="center">
  ⭐ If you found this helpful, consider starring the repo!
</p>
