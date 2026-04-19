# Assessment — NVTech Internal Multi-App Host

---

## Question 1 — MCQ

**On which port is the real target application (Project Access Portal) running?**

- A) `8001`
- B) `8005`
- C) **`8009`** ✅
- D) `8010`

> **Answer:** C — Port `8009` hosts the Project Access Portal — the actual target. Ports `8001`–`8008` and `8010` serve decoy applications (Asset Management, Payroll Mirror, etc.) designed to waste the attacker's time during enumeration.

---

## Question 2 — MCQ

**The login form's WAF blocks `OR`, `UNION`, `SELECT`, `--`, and `#`. Which operator successfully bypasses it for the SQL injection?**

- A) `AND`
- B) `XOR`
- C) `&&`
- D) **`||`** ✅

> **Answer:** D — The `||` operator (logical OR in SQL) is not on the WAF's blocklist. The payload `' || '1'='1` appended to the password field makes the WHERE clause always evaluate to true, bypassing the login.

---

## Question 3 — MCQ

**The LFI endpoint at `/archive?doc=` sanitises `../` sequences. What traversal string bypasses this imperfect recursive sanitisation?**

- A) `..//`
- B) `%2e%2e%2f`
- C) `..%2f`
- D) **`....//`** ✅

> **Answer:** D — The sanitiser performs a non-recursive replacement of `../`. When `....//` is processed, the inner `../` is stripped, leaving `../` — successfully traversing one directory level. Multiple repetitions (`....//....//....//....//`) reach the target file.

---

## Question 4 — Fill in the Blank

**What logical operator, used in place of `OR`, bypasses the WAF and achieves SQL injection on the login form?**

**Answer:** `||`

> The WAF blocks `OR` as a keyword but does not block the SQL logical OR operator `||`. Using `' || '1'='1` as the password makes the backend query condition always true, bypassing authentication without triggering the WAF.

---

## Question 5 — Fill in the Blank

**What traversal sequence is used to bypass the non-recursive `../` sanitisation in the LFI endpoint?**

**Answer:** `....//`

> The application's sanitiser strips `../` in a single non-recursive pass. Supplying `....//` means after the `../` inside is removed, `../` remains — completing one level of directory traversal. The final working path uses four of these sequences to reach the target file.

---

*Lab target (real app):* `http://localhost:8009`
