# Security Framework & Password Evaluation Logic

A practical information security utility developed in Python to bridge the gap between theoretical cryptographic research and functional application. The tool evaluates password resilience by combining strict adherence to international security standards with information theory mathematics.

## 1. Core Methodology & Mathematical Framework

Unlike traditional tools that rely solely on string length, this framework evaluates the actual randomness and unpredictability of user inputs using the **Shannon Entropy Model**[cite: 2, 3]. 

### The Entropy Formula:
$$H = L \times \log_2(R)$$

Where[cite: 2, 3]:
*   **H**: Entropy value in bits[cite: 2, 3].
*   **L**: Total length of the password string[cite: 2, 3].
*   **R**: Character set pool size, dynamically computed based on the detected character types[cite: 2, 3]:
    *   *Lowercase letters [a-z]*: Pool Size = 26[cite: 2, 3]
    *   *Uppercase letters [A-Z]*: Pool Size = 26[cite: 2, 3]
    *   *Numbers [0-9]*: Pool Size = 10[cite: 2, 3]
    *   *Special Symbols/Characters*: Pool Size = 32[cite: 2, 3]

### NIST SP 800-63B Alignment:
The validation pipeline incorporates core recommendations from the **National Institute of Standards and Technology (NIST)** guidelines[cite: 2, 3]:
- Real-time comparison against a localized common-password blacklist (`123456`, `password`, `123456789`, `qwerty`, `admin`) to mitigate dictionary attacks[cite: 1, 2].
- Verifying character entropy boundaries rather than enforcing arbitrary character composition rules[cite: 2, 3].

---

## 2. Dynamic Classification Logic & Rating Scale

Based on the mathematical outputs of the entropy calculation engine, passwords are filtered and classified into three strict security tiers[cite: 2, 3]:

| Rating | Entropy Threshold | Length Criteria | Threat Implication & Resilience |
| :--- | :--- | :--- | :--- |
| **WEAK** | $< 40$ bits | $< 8$ characters | Vulnerable to instant brute-force and dictionary attacks[cite: 2, 3]. |
| **MODERATE**| $40 - 60$ bits | $8 - 12$ characters | Resists basic automated attacks; inadequate for sensitive data[cite: 2, 3]. |
| **STRONG** | $> 60$ bits | $\ge 12$ characters | Highly resistant to advanced brute-force attempts via GPU clusters[cite: 2, 3]. |

*Note: Any input matching the common-password blacklist is instantly dropped to a **WEAK** classification regardless of its length or calculated bits[cite: 2].*

---

## 3. Implemented Threat Model Mitigations

The validation logic was engineered to actively test and defend user credentials against specific vectors identified in the project threat assessment[cite: 2, 3]:
*   **Brute Force Attacks:** Defended by verifying high entropy pools ($>60$ bits) to exponentially increase the attacker's required work factor[cite: 2, 3].
*   **Dictionary Attacks:** Controlled via an automated blacklist validation check before processing structural logic[cite: 2, 3].
*   **Credential Stuffing & Rainbow Tables:** Addressed within the research framework by defining requirements for salted hashing (e.g., *bcrypt*, *Argon2*) and Multi-Factor Authentication (MFA) parameters[cite: 2, 3].

---

## 4. Verification & Testing Scenarios

The tool's detection accuracy was verified using rigorous, automated execution pipelines matching the empirical test logs[cite: 1, 2]:

1. **TC-01 (Blacklist Check):** Input `admin` $\rightarrow$ Result: **WEAK** (Criteria: Common password detected)[cite: 1, 2].
2. **TC-02 (Length & Complexity Failure):** Input `123456789` $\rightarrow$ Result: **WEAK** (Criteria: Entropy $< 40$ bits)[cite: 1, 2].
3. **TC-03 (Standard User Pattern):** Input `Jo123456` $\rightarrow$ Result: **MODERATE** (Criteria: Balanced character mix, Entropy ~38.99 bits)[cite: 1, 2].
4. **TC-04 (High Cryptographic Resilience):** Input `P@ssw0rd!2026` $\rightarrow$ Result: **STRONG** (Criteria: Full character set utilization, Entropy ~91.76 bits)[cite: 1, 2].

---

## Project Context
This system was developed as a core technical component for an academic Information Security curriculum[cite: 1, 2]. I maintained full ownership over the software engineering lifecycle, including building the mathematical entropy computation engine, database/list validation algorithms, and automated verification script testing[cite: 2].
