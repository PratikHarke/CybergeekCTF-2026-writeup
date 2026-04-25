# 🧠 Archive Me In Your Heart – Writeup

<p align="center">
  <img src="https://img.shields.io/badge/Category-Forensics%20%2F%20Steganography-purple?style=for-the-badge">
  <img src="https://img.shields.io/badge/Difficulty-Medium-yellow?style=for-the-badge">
  <img src="https://img.shields.io/badge/CTF-CTF7-blue?style=for-the-badge">
  <img src="https://img.shields.io/badge/Technique-PDF%20Forensics-green?style=for-the-badge">
</p>

---

## 📁 Files Included

- Archive_me_in_your_Heart.pdf → Challenge PDF file

---

## 📌 Challenge Overview

Challenge description:
pee dee ef

We are given a PDF containing a story. The objective is to find the hidden flag.

Flag format: geek{...}

---

## 🔍 Step 1: Initial Observation

Opening the PDF shows a multi-part story:

- Part One: The Shelf
- Part Two: The Rain
- Part Three: Eight Months
- Part Four: The Ledger

At first glance, the PDF looks like normal narrative text, but several anomalies are visible:

- Broken and truncated words
- Irregular spacing
- Strange formatting issues
- Inconsistent sentence structures

Examples include words like summHe, thh, and agaih.

These anomalies suggest that the visible story is likely a decoy and the real flag is hidden inside the PDF structure.

---

## 🧠 Step 2: Analysis Strategy

The clue “pee dee ef” points directly toward PDF internals.

Instead of trusting the visible text, the approach was:

- Inspect raw strings
- Check metadata
- Look for embedded files
- Extract compressed objects
- Analyze PDF object streams
- Verify all discovered flags carefully

---

## 🔧 Step 3: Extracting Strings

Command:
strings Archive_me_in_your_Heart.pdf | grep geek

Output:
geek{n0t_th3_r34l_0n3}
geek{d3c0y_f14g}

These flags were found very easily, which made them suspicious.

Conclusion:
Both are decoy flags.

---

## 🔧 Step 4: Metadata Check

Command:
exiftool Archive_me_in_your_Heart.pdf

Result:
No useful flag-related information was found in the metadata.

---

## 🔧 Step 5: Embedded Data Scan

Command:
binwalk Archive_me_in_your_Heart.pdf

The scan revealed hidden structures and embedded data inside the PDF.

This confirmed that the file contained more than just normal visible PDF content.

---

## 🔧 Step 6: Extracting Embedded Content

Command:
binwalk -e Archive_me_in_your_Heart.pdf

This extracted hidden files and compressed objects from the PDF for further inspection.

---

## 🔧 Step 7: Checking PDF Attachments

Command:
pdfdetach -list Archive_me_in_your_Heart.pdf

Attachments were detected inside the PDF.

Extraction command:
pdfdetach -saveall Archive_me_in_your_Heart.pdf

This revealed an embedded PNG file.

---

## 🔍 Step 8: Analyzing the Embedded PNG

The extracted PNG was inspected using tools like strings, exiftool, and image viewing.

The PNG revealed an additional hint/key, confirming that the challenge used multiple layers and that simple string extraction was not enough.

---

## 🔧 Step 9: Inspecting PDF Object Streams

Command:
qpdf --qdf --object-streams=disable Archive_me_in_your_Heart.pdf out.pdf

This decompressed the PDF object streams and made hidden content readable.

Inside the decompressed output, another flag was found:

geek{wr0ng_l4y3r_wr0ng_4nsw3r}

This was also a decoy flag.

---

## 🧩 Step 10: Final Extraction

At this point, multiple fake flags had been discovered:

- geek{n0t_th3_r34l_0n3}
- geek{d3c0y_f14g}
- geek{wr0ng_l4y3r_wr0ng_4nsw3r}

By correlating:

- Decoy flags from strings
- Hidden PDF object streams
- Embedded PNG hint
- Extracted PDF attachments

The correct flag was identified.

---

## 🎯 Final Flag

geek{I_l0ve_PDF}

---

## 🧠 Key Takeaways

- PDF challenges often contain multiple hidden layers
- Easy flags found using strings are often decoys
- Always inspect PDF internals, not just visible content
- Useful PDF hiding locations include:
  - Object streams
  - Embedded attachments
  - Metadata
  - Compressed objects
  - Hidden images
- Systematic enumeration helps avoid falling for decoys

---

## 🛠 Tools Used

- strings
- binwalk
- pdfdetach
- exiftool
- qpdf

---

## 🏁 Conclusion

This challenge demonstrates a classic multi-layer PDF forensics and steganography workflow. The visible story and easily extracted flags were designed to mislead the solver. By analyzing embedded files, compressed streams, and PDF internals, the real flag was recovered successfully.

---

<p align="center">
  ⭐ If you found this helpful, consider starring the repo!
</p>
