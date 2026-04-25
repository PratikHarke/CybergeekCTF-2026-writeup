# 🧠 Peeedeeeffffff Writeup

<p align="center">
  <img src="https://img.shields.io/badge/CATEGORY-FORensics-purple?style=for-the-badge">
  <img src="https://img.shields.io/badge/DIFFICULTY-HARD-black?style=for-the-badge">
  <img src="https://img.shields.io/badge/TECHNIQUE-PDF%20Steganography-blue?style=for-the-badge">
  <img src="https://img.shields.io/badge/FOCUS-MULTI%20LAYER%20ANALYSIS-green?style=for-the-badge">
</p>

---

## 📁 Files Included

- Archive_me_in_your_Heart.pdf → Challenge PDF  

---

## 📜 Challenge Description

pee dee ef  

Flag format: geek{...}

---

## 🔍 Initial Observation

The PDF contains a multi-part story:

- Part One: The Shelf  
- Part Two: The Rain  
- Part Three: Eight Months  
- Part Four: The Ledger  

However, several anomalies stand out:

- Broken words (summHe, thh, agaih)  
- Irregular spacing  
- Formatting inconsistencies  

➡️ Indicates visible text is a **decoy**

---

## 🧠 Approach

The hint “pee dee ef” suggests focusing on:

- PDF internals  
- Embedded objects  
- Hidden layers  

➡️ Not the visible content

---

## 🔧 Step 1: Strings Extraction

Command:
strings Archive_me_in_your_Heart.pdf | grep geek

Output:
geek{n0t_th3_r34l_0n3}  
geek{d3c0y_f14g}  

➡️ Decoy flags

---

## 🔧 Step 2: Metadata Check

Command:
exiftool Archive_me_in_your_Heart.pdf

➡️ No useful data

---

## 🔧 Step 3: Embedded Data Scan

Command:
binwalk Archive_me_in_your_Heart.pdf

➡️ Reveals hidden structures

---

## 🔧 Step 4: Extract Embedded Content

Command:
binwalk -e Archive_me_in_your_Heart.pdf

➡️ Extracts hidden files

---

## 🔧 Step 5: Extract Attachments

Command:
pdfdetach -list Archive_me_in_your_Heart.pdf

Extraction:
pdfdetach -saveall Archive_me_in_your_Heart.pdf

➡️ Embedded PNG found

---

## 🔍 Step 6: PNG Analysis

- PNG contains additional hints  
- Confirms multi-layer hiding  

---

## 🔧 Step 7: Inspect Object Streams

Command:
qpdf --qdf --object-streams=disable Archive_me_in_your_Heart.pdf out.pdf

Found:
geek{wr0ng_l4y3r_wr0ng_4nsw3r}

➡️ Another decoy

---

## 🧩 Final Extraction

After correlating:

- Decoy flags  
- Embedded PNG  
- PDF object streams  

➡️ Real flag identified

---

## 🎯 Final Flag

geek{I_l0ve_PDF}

---

## 🧠 Key Takeaways

- PDFs can hide multiple layers  
- Strings output often contains decoys  
- Always inspect:
  - Object streams  
  - Embedded files  
  - Attachments  
- Systematic enumeration is key  

---

## 🛠 Tools Used

- strings  
- binwalk  
- pdfdetach  
- exiftool  
- qpdf  

---

## 🏁 Conclusion

This challenge demonstrates multi-layer PDF steganography with intentional decoys. Careful inspection of internal structures leads to the correct flag.

---

<p align="center">
  ⭐ If you found this helpful, consider starring the repo!
</p>
