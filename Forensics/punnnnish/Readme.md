# 🕰️ The Timekeeper – Writeup

<p align="center">
  <img src="https://img.shields.io/badge/CATEGORY-FORensics-purple?style=for-the-badge">
  <img src="https://img.shields.io/badge/DIFFICULTY-MEDIUM-black?style=for-the-badge">
  <img src="https://img.shields.io/badge/TECHNIQUE-GIT%20METADATA-blue?style=for-the-badge">
  <img src="https://img.shields.io/badge/FOCUS-TEMPORAL%20CHANNEL-green?style=for-the-badge">
</p>

---

## 📁 Files Included

punish.zip 

---

## 📜 Challenge Description

Our investigators recovered a Git repository from a suspect known as **"The Timekeeper"**. The repository appeared to contain only repeated updates to a single text file.

Key hint:

The data just isn't in the code.

Flag format: geek{...}

---

## 🔍 Initial Analysis

Checked commit history:

Command:
git log --oneline

➡️ Multiple commits found, but nothing suspicious in messages.

Checked file contents across commits:

Command:
git show <commit>

➡️ Only normal text updates  
➡️ No hidden strings or anomalies  

---

## 🧠 Observation

Hints mention:

- Precision  
- Rhythm  
- Silence  

➡️ Suggests **time-based encoding**

---

## ⏱️ Step 1: Extract Commit Timestamps

Command:
git log --pretty=format:"%ct" --reverse

➡️ Extracts UNIX timestamps in chronological order  

---

## 📊 Step 2: Calculate Time Differences

Python logic:

times = [ ... ]  
diffs = [times[i] - times[i-1] for i in range(1, len(times))]

Sample output:

3703, 3701, 3701, 3707, 3723, ...

---

## 🔍 Step 3: Identify Pattern

Observed:

- Values ~3600 seconds  
- Slight variations  

➡️ Pattern:

decoded_character = time_difference - 3600

Example:

3703 - 3600 = 103 → g  
3701 - 3600 = 101 → e  
3701 - 3600 = 101 → e  
3707 - 3600 = 107 → k  
3723 - 3600 = 123 → {  

➡️ Forms:

geek{

---

## 🧪 Step 4: Full Decoding Script

Python script:

import subprocess

output = subprocess.check_output(
    ["git", "log", "--pretty=format:%ct", "--reverse"]
).decode().splitlines()

times = [int(x) for x in output]

diffs = [times[i] - times[i-1] for i in range(1, len(times))]

flag = ''.join(chr(d - 3600) for d in diffs)

print(flag)

---

## 🎯 Output

geek{t1m3_tr4v3l_c0mm1t5}

---

## 🏁 Final Flag

geek{t1m3_tr4v3l_c0mm1t5}

---

## 💡 Explanation

This challenge uses a **temporal covert channel**.

- Each commit occurs after ~3600 seconds  
- Extra delay encodes ASCII values  
- Subtracting 3600 reveals characters  

➡️ Data is hidden in **time differences**, not code  

---

## 🧠 Key Takeaways

- Always inspect metadata in forensic challenges  
- Git timestamps can act as covert channels  
- Timing-based encoding is common in:
  - Malware beaconing  
  - Network covert channels  
- Keywords like rhythm/precision often hint at time-based tricks  
- Hidden data is not always inside files  

---

## 🛠 Tools Used

- git  
- Python  

---

## 🏁 Conclusion

Instead of focusing on file contents, analyzing commit timestamps revealed a hidden pattern. The time differences between commits encoded ASCII characters, leading directly to the flag.

---

<p align="center">
  ⭐ If you found this helpful, consider starring the repo!
</p>
