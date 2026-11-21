# Password Cracking of a Protected PDF — Hash Extraction & Dictionary Attack

![Type](https://img.shields.io/badge/type-password%20auditing-blue)
![Category](https://img.shields.io/badge/category-offensive%20security-orange)
![Scope](https://img.shields.io/badge/scope-authorized%20lab-green)
![Status](https://img.shields.io/badge/status-complete-brightgreen)

A hands-on lab demonstrating the full workflow of password recovery against a protected file: extracting a crackable hash from an encrypted PDF, running a dictionary attack against that hash, and verifying the recovered password against the original file.

> **Scope:** This lab was performed against a training file provided by Networkwalks Academy (`My Locked PDF1.pdf`), using browser-based lab tools built for this exercise. It mirrors real-world password-auditing practice (the kind performed with tools like **John the Ripper** or **Hashcat**) without requiring anything beyond a browser.

The full write-up, with step-by-step screenshots, is in [`Password_Cracking_Project_Report.docx`](./Password_Cracking_Project_Report.docx).

---

## Table of Contents

- [Objective](#objective)
- [Background: Hashing vs. Encryption](#background-hashing-vs-encryption)
- [Tools and Environment](#tools-and-environment)
- [Methodology](#methodology)
- [Result](#result)
- [Key Takeaways](#key-takeaways)
- [Conclusion](#conclusion)
- [Skills Demonstrated](#skills-demonstrated)
- Pictures
- [Disclaimer](#disclaimer)
- [Author](#author)
- [References](#references)

---

## Objective

Understand, hands-on, how password-protected files can be attacked and recovered using hash extraction and a dictionary attack, and use that understanding to explain why weak passwords are a serious security risk.

**Task:** Crack the password of a locked file, `My Locked PDF1.pdf`, using two browser-based tools — a **Hash Calculator** and a **Password Cracker**.

## Background: Hashing vs. Encryption

These two concepts are easy to confuse:

| | Encryption | Hashing |
|---|---|---|
| Direction | Two-way (reversible with the correct key) | One-way (not reversible) |
| Recovery method | Decrypt with the key | Guess candidates and compare hashes |

A password-protected PDF does not store the password itself — it stores a **hash** derived from it. To recover the password, the hash must be extracted from the file, then tested against a wordlist: each candidate word is hashed and compared to the target hash until a match is found.

## Tools and Environment

| Item | Detail |
|---|---|
| Target file | `My Locked PDF1.pdf` (password-protected PDF) |
| Hash extraction | Networkwalks Hash Calculator — extracts a `pdf2john`/hashcat-compatible `$pdf$` hash, entirely client-side in the browser |
| Cracking tool | Networkwalks Password Cracker — dictionary attack using a built-in 100-password wordlist (or a custom uploaded wordlist) |
| Verification | Adobe Acrobat Reader DC, used to confirm the recovered password opens the real file |
| Platform | Windows laptop (works unchanged on Kali Linux — both tools run entirely in-browser) |

## Methodology

1. **Obtain the target file** — downloaded `My Locked PDF1.pdf` from the lab page.
2. **Open the Hash Calculator** — supports Text, File, and PDF input modes; hashing runs locally, nothing is uploaded to a server.
3. **Extract the hash** — uploaded the PDF via the PDF tab; the tool identified it as encrypted and extracted a crackable hash beginning with `$pdf$`, along with revision, version, and key-length metadata.
4. **Copy the complete hash** — copied in full, since a truncated hash would cause every cracking attempt to fail.
5. **Open the Password Cracker** — simulates a dictionary attack: hashes every wordlist entry and compares it to the target hash, the same principle used by John the Ripper.
6. **Paste the hash and select a wordlist** — used the built-in 100 common-password list.
7. **Run the attack** — clicked "Start Cracking"; the tool tested candidates in real time (e.g. `service`, `canada`, `hockey`, `killer`, `qwertyuiop`, `111222`) until a match was found.
8. **Verify against the real file** — opened the original PDF in Adobe Acrobat Reader DC and entered the recovered password.
9. **Confirm recovery** — the PDF unlocked immediately, confirming the dictionary attack had found the correct password.

## Result

| Field | Value |
|---|---|
| Target file | `My Locked PDF1.pdf` |
| Extracted hash format | `$pdf$` (pdf2john / hashcat-compatible, Revision 4, Version 4, 128-bit key) |
| Attack method | Dictionary attack, built-in 100-password wordlist |
| Attempts required | 91 of 100 candidates (91% of the list) |
| Recovered password | `password1` |
| Time to crack | A few seconds, at ~9 passwords/second |

## Key Takeaways

- **Weak, predictable passwords fail almost instantly.** `password1` is a dictionary word plus a single digit — a pattern common enough to sit near the top of most breach-derived wordlists.
- **Hashing ≠ encryption.** Since the password is stored as a one-way hash, there is no key to recover — the only way in is to guess candidates and compare hashes, which is exactly what both tools automated here.
- **Dictionary attacks scale with password strength.** An 8-character, lowercase-only password can be cracked in minutes; a 12-character password mixing case, numbers, and symbols can take years to brute-force. This gap is the core lesson of the lab.
- **Real-world relevance.** Over 24 billion username/password pairs are already circulating from past breaches, and leaked credential sets keep resurfacing for years. Attackers reuse these lists rather than guessing blindly — which is why unique, complex passwords and MFA matter.
- **Defensive implication.** This lab is a compact illustration of why organizations enforce password complexity policies, salted/strong hashing algorithms (bcrypt/Argon2 rather than fast hashes), and account lockout or rate-limiting controls.

## Conclusion

This lab demonstrated the end-to-end workflow of password cracking against a protected file: extracting a crackable hash, running a dictionary attack against it, and verifying the recovered password against the original file. The password (`password1`) was recovered in seconds because it was short and predictable — reinforcing that password strength is the single biggest factor in resistance to offline cracking attacks. The skills practiced — hash extraction, dictionary/wordlist attacks, and interpreting cracking-tool output — are foundational to password auditing, penetration testing, and security-awareness work.

## Skills Demonstrated

- Hash extraction from a protected document (`pdf2john`/hashcat-compatible format)
- Dictionary attack methodology and wordlist-based password recovery
- Interpreting cracking-tool output and attack progress/rate metrics
- Distinguishing hashing from encryption, and explaining the security implications
- Verifying recovered credentials against the original protected artifact
- Translating a technical exercise into defensive recommendations (salting, strong hashing, MFA, lockout policies)

## PICTURES

<img width="1333" height="749" alt="image" src="https://github.com/user-attachments/assets/9a8946ad-5fd8-4577-8636-493878bd1062" />

<img width="1333" height="749" alt="image" src="https://github.com/user-attachments/assets/4941b5b4-aa73-4325-8a6d-453a9c3add92" />

<img width="1333" height="749" alt="image" src="https://github.com/user-attachments/assets/de6a2dd9-d1bf-409e-9e5b-136e2a59150e" />

<img width="1333" height="749" alt="image" src="https://github.com/user-attachments/assets/8c22089a-0919-4107-87d5-b091f7787781" />

<img width="1333" height="749" alt="image" src="https://github.com/user-attachments/assets/f8c4b09b-8fbe-4fd3-a03d-ed17539a1883" />

<img width="1601" height="898" alt="image" src="https://github.com/user-attachments/assets/8d143df9-6d1f-44d9-87cd-c91eb99e80fa" />

<img width="1395" height="785" alt="image" src="https://github.com/user-attachments/assets/495d0b4d-6542-49e6-9cb6-b44ed55836f4" />











## Disclaimer

This exercise was performed in a controlled training environment against a file provided for that purpose. Password cracking must only be performed on systems, accounts, or files you own or have explicit written authorization to test. Unauthorized password cracking is illegal in most jurisdictions.

## Author

** K BHAVANI**, Cybersecurity & Ethical Hacking Trainee

- LinkedIn: www.linkedin.com/in/bhavani-k-692a463a0
- Email: bhavani08021947@gmail.com

## References

- Networkwalks Academy — Cybersecurity & Ethical Hacking training, Week 3, Project Module 2
- John the Ripper: https://www.openwall.com/john/
- Hashcat: https://hashcat.net/hashcat/
- OWASP Password Storage Cheat Sheet
