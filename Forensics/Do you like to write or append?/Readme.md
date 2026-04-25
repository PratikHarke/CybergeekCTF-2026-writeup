# 🍓 Strawberry Ice Cream – Writeup

<p align="center">
  <img src="https://img.shields.io/badge/CATEGORY-FORensics-purple?style=for-the-badge">
  <img src="https://img.shields.io/badge/DIFFICULTY-EASY-black?style=for-the-badge">
  <img src="https://img.shields.io/badge/TECHNIQUE-POLYGLOT%20FILES-blue?style=for-the-badge">
  <img src="https://img.shields.io/badge/FOCUS-IMAGE%20DIFFING-green?style=for-the-badge">
</p>

---


## 📜 Challenge Description

You think it's special, but it's all reused.

Flag format: geek{...}

---

## 🔍 Initial Analysis

Command:
binwalk strawberry_ice_cream.jpg

Output shows multiple embedded structures:

- JPEG image data  
- TIFF image data  
- Multiple offsets indicating layered content  

➡️ Indicates a polyglot / concatenated file  

---

## 🧵 Step 1: Manual Extraction

Since auto extraction failed, images were carved manually:

Command:
dd if=strawberry_ice_cream.jpg of=img1.jpg bs=1 skip=0 count=182202  
dd if=strawberry_ice_cream.jpg of=img2.jpg bs=1 skip=182202  

➡️ Two separate images extracted  

---

## 🔎 Step 2: Metadata Analysis

Commands:
file img1.jpg img2.jpg  
exiftool img1.jpg img2.jpg  
strings img1.jpg | grep geek{  
strings img2.jpg | grep geek{  

Observations:

- Same resolution: 1080x1080  
- Same tool: Canva  
- Nearly identical metadata  

Key difference:

img1 → Title: geek{ - 1  
img2 → Title: geek{ - 2  

➡️ Indicates split or layered data  

---

## 🧠 Step 3: Understanding the Hint

"You think it's special, but it's all reused"

➡️ Interpretation:

- Images are reused copies  
- Differences between them contain data  
- Hidden content lies in pixel variations  

---

## ⚡ Step 4: Image Differencing

Python script:

from PIL import Image, ImageChops, ImageEnhance

img1 = Image.open("img1.jpg").convert("RGB")  
img2 = Image.open("img2.jpg").convert("RGB")  

diff = ImageChops.difference(img1, img2)  
diff = ImageEnhance.Contrast(diff).enhance(10)  

diff.save("final.png")  

---

## 👀 Step 5: Extracting the Flag

Opening final.png reveals hidden text embedded in pixel differences.

➡️ Flag becomes clearly visible after contrast enhancement  

---

## 🏁 Final Flag

geek{deja-vu!}

---

## 🧠 Key Takeaways

- Polyglot files can contain multiple embedded formats  
- Metadata can hint but rarely gives full answer  
- Reused images often hide differences  
- Image differencing is a powerful forensic technique  
- Small pixel changes can encode meaningful data  

---

## 🛠 Tools Used

- binwalk  
- dd  
- exiftool  
- strings  
- Python (PIL)  

---

## 🏁 Conclusion

This challenge combined file carving, metadata analysis, and image steganography. By identifying that the image was reused and analyzing the differences between extracted images, the hidden flag was revealed successfully.

---

<p align="center">
  ⭐ If you found this helpful, consider starring the repo!
</p>
