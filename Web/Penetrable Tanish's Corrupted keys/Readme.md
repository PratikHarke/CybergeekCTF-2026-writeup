# 🧬 Localized Density Anomaly – Writeup

<p align="center">
  <img src="https://img.shields.io/badge/CATEGORY-FORensics%20%2F%20MISC-purple?style=for-the-badge">
  <img src="https://img.shields.io/badge/DIFFICULTY-EASY-black?style=for-the-badge">
  <img src="https://img.shields.io/badge/TECHNIQUE-ZERO%20WIDTH%20UNICODE-blue?style=for-the-badge">
  <img src="https://img.shields.io/badge/FOCUS-DATA%20ANOMALY%20DETECTION-green?style=for-the-badge">
</p>

---

## 📁 Files Included

- corrupted_keys.txt → Provided dataset  

---

## 📜 Challenge Description

reporting a localized density anomaly

Flag format: geek{...}

---

## 🔍 Initial Analysis

Dataset format:

geek{12_hex_characters}

Examples:

geek{a90b54b245f4}  
geek{7cf6a94ff15b}  

Observations:

- All entries follow identical structure  
- Hex values appear random  
- No visible anomalies at first glance  

➡️ Indicates hidden data within structure, not values  

---

## 🧠 Step 1: Understanding the Hint

"localized density anomaly"

➡️ Suggests:

- A specific region is different  
- Higher concentration of hidden data  
- Not visible through normal inspection  

---

## 🔎 Step 2: Investigation Strategy

Instead of analyzing values:

Focus on:

- Line length differences  
- Hidden/non-printable characters  
- Encoding inconsistencies  

Tools used:

wc -L  
cat -A  
xxd / hexdump  

---

## 🔧 Step 3: Finding the Anomaly

One line stands out:

- Longer than others  
- Contains strange sequences like:

â€‹  
â€Œ  

➡️ Indicates encoding issue (mojibake)

---

## 🧬 Step 4: Identifying Hidden Data

These sequences represent:

- U+200B → ZERO WIDTH SPACE  
- U+200C → ZERO WIDTH NON-JOINER  

➡️ Invisible characters carrying information  

---

## ⚡ Step 5: Extraction & Decoding

Process:

1. Extract zero-width characters  
2. Map to binary:
   - U+200B → 0  
   - U+200C → 1  
3. Convert binary → ASCII  

---

## 🎯 Decoded Output

sup3rman_is_just_a_guy  

---

## 🏁 Final Flag

geek{sup3rman_is_just_a_guy}

---

## 🧠 Key Takeaways

- Invisible Unicode characters can hide data  
- Always inspect raw file structure  
- Encoding artifacts (mojibake) are valuable clues  
- Large datasets often hide small anomalies  
- Forensics challenges require pattern deviation detection  

---

## 🛠 Tools Used

- wc  
- cat  
- xxd / hexdump  
- Python (optional for decoding)  

---

## 🏁 Conclusion

This challenge demonstrates how hidden Unicode characters can act as a covert channel. By identifying anomalies in data structure and decoding zero-width characters, the hidden flag was successfully extracted.

---

<p align="center">
  ⭐ If you found this helpful, consider starring the repo!
</p>
