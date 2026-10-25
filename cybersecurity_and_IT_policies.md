# 6. Cybersecurity and IT Policies

## 6.1 Cybersecurity, Access Control, Threats / Vulnerabilities, Attacks, Authn / Authz, Passwords

### Q.1 What is cybersecurity? Explain CIA triad, relation between threat, vulnerability and risk, and classify security attacks.

**Def**
→ protecting systems, networks, programs and data from digital attacks aimed at accessing, changing or destroying sensitive information, extorting money or interrupting business.

```text
                    +-------------------+
                    |  Confidentiality  |
                    +-------------------+
                       /             \
                      /  INFORMATION  \
                     /    SECURITY     \
                    /                   \
        +-----------+                    +--------------+
        | Integrity |--------------------| Availability |
        +-----------+                    +--------------+
```

| Pillar | Meaning | Tools | Bank example |
| :--- | :--- | :--- | :--- |
| Confidentiality | Information not disclosed to unauthorized people | Encryption, access control | PIN and balance secret |
| Integrity | Data not modified by unauthorized parties | Hashing, digital signature, audit trail / tampering | Transfer amount not altered |
| Availability | Systems and data accessible when needed | Backup, DDoS protection, failover, redundancy, DR site | Internet banking and ATM |

*Fig: CIA triad with banking examples*

| Term | Definition | Example |
| :--- | :--- | :--- |
| Asset | Anything (value to protect) | Customer db |
| Vulnerability | Weakness in a system | Unpatched web server, weak password |
| Threat | Anything that can exploit a vulnerability to cause harm | Hacker, malware, insider |
| Attack | Deliberate action | SQL injection, phishing |
| Risk | Likelihood × impact | costly |
| Control | Measure that reduces risk | Patch, firewall, MFA |

```text
 [THREAT] --exploits--> [VULNERABILITY]
                              |
                              v
              damage on ASSET (customer data)

 [ RISK = likelihood × impact ]
```

**Classification of attacks**

```text
(a) Passive attack                        (b) Active attacks

 [Sender] ------------------> [Receiver]   [Sender]                  [Receiver]
      |                                        \  intercept            ^
      | copy only                               v                    | altered or
      v                                      [Attacker] -------------+ false message
  [Attacker]

 Eavesdropping, traffic:                   Masquerade, replay, modification,
 hard to detect                            DoS: detectable
```

---

### Q.N.2 Access control models (DAC, MAC, RBAC, ABAC)

**4 steps**
Identification (who are you? username) > Authentication (prove it) > Authorization (what may you do?) > Accounting / Auditing (log what you did).

| Model | Example |
| :--- | :--- |
| DAC (Discretionary) | sharing a folder on a PC |
| MAC (Mandatory) | Military, classified systems |
| RBAC (Role-based) | Teller, loan officer, branch manager (banks use mainly this) |
| ABAC (Attribute-based) | Loan system only from office network in office hours |

---

### Q.3 Authentication vs Authorization; MFA in banking.

```text
 factor 1:                       factor 2:
 something you know              something you have

 [Customer enters  ]   [Server checks ]   [OTP send to   ]   [Customer    ]   [Access granted;]
 [user ID + pass-  ] → [password hash ] → [registered     ] → [enters OTP ] → [rights by role ]
 [word             ]                      [phone          ]

   AUTHENTICATION        AUTHENTICATION        AUTHORIZATION
   KNOW                  HAVE                  ARE
   Password, PIN         phone, token, card    fingerprint, face
```
*Fig: Multifactor login to Internet Banking*

**Weak point**
→ OTP can be phished.

**NRB requirement**
→ second factor for online card payment.

---

### Q.4 Password Management and a good password policy

```text
 Registration                                          Login

 [password]  --\                  stored:              entered password +
                >--> [Slow hash ]--> userID,           stored salt
 [random salt]-/      [function  ]    salt,            --> hash again -->
                                      hash             compare with stored hash
                                                       equal = accept
```
the password itself is never stored; a hash cannot be reversed

*Fig: Storing and checking a password with a salt and a hash.*

---

### Q.4 Risk assessment. How risk is measured and treated?

**Steps**
1. list assets
2. Identify threats and vulnerabilities
3. Estimate likelihood & impact
4. Rank in a risk register
5. Choose treatment
6. Monitor and repeat

**Risk matrix (score = likelihood × impact)**

| Likelihood \ Impact | Low | Medium | High |
| :--- | :---: | :---: | :---: |
| **High** | 3 | 6 | 9 |
| **Medium** | 2 | 4 | 6 |
| **Low** | 1 | 2 | 3 |

- 6-9: treat at once
- 3-4: plan controls
- 1-2: accept, monitor

*Fig: From threat to risk, and a simple risk matrix*

**Ex:** The bank's database / server is worth Rs 10,000,000 (the asset). A cyber attack would damage 20% of it. Attacks happen about once in 2 years.

→ Given,
- Asset Value (AV) = Rs 10,000,000
- Exposure Factor (EF) = 20% = 0.2
- Single Loss Expectancy (SLE) = AV × EF = Rs 2,000,000
- Annual Rate of Occurrence (ARO) = 1/2 = 0.5 (Once in 2 years)
- Annual Loss Expectancy (ALE) = SLE × ARO = Rs 1,000,000 per year

∴ so without any protection, the bank expects to lose Rs 1,000,000 every year.

**Again, Is a security control worth buying?**
then, suppose
- cost of control = Rs 3,00,000 per year
- new ARO = 1/10 = 0.1 (Once in 10 years)
- ALE after = SLE × new ARO = 2,000,000 × 0.1 = Rs 200,000
- Saved = ALE before − ALE after = 1,000,000 − 200,000 = 800,000
- Net benefit = Saved − Cost of control = Rs 5,00,000

∴ so the control is worth buying.

---

## 6.2 Common Security Threats: Social Engineering, Malware, DoS / DDoS, Phishing

### ① Malware

```text
                              Malware
                  +----------------+----------------+
          By how it spreads                By what it does (payload)

 [Virus]  attaches to a host file;    [Ransomware: encrypts data for payment]
          runs when the file is opened[Spyware, keylogger: steal information]
 [Worm]   copies itself over the      [Bot: joins a remotely controlled botnet]
          network without help        [Rootkit, backdoor: hides and keeps access]
 [Trojan  disguised as useful         [Adware: unwanted advertisements]
  horse]  software; installed by      [Logic bomb: acts on a set condition]
          the user
```
*Fig: Classification of malware*

### ② Customers receive calls / messages asking for passwords and OTPs. Explain social engineering, types of phishing and bank measures.

→ urgency, authority, fear, reward

→ **stop here:** verify, do not click, report

```text
 [1. Research ] → [2. Fake message ] → [3. Victim clicks ] → [4. Fake site    ] → [5. Attacker logs in,]
 [   target   ]   [(email, SMS,    ]   [link, password,  ]   [collects        ]   [transfers money     ]
                  [ call)          ]   [OTP              ]   [password, OTP    ]
                                       |<----------- the victim acts here ----------->|
```
a phishing attack succeeds only if the victim acts at step 3 or 4

*Fig: Stages of a phishing attack*

### ③ DoS vs DDoS; how a bank defends?

```text
(a) DoS: one source                   (b) DDoS: many sources (botnet)

 [Attacker] ==flood==> [Bank server]   [Attacker] → [Command server] → [Bot] ┐
                            ^ refused                                  [Bot] ┼→ [Bank server]
                        [Customer]                                     [Bot] ┤
                                                                       [Bot] ┘
                                       thousand of hijacked devices send traffic together
```
*Fig: DoS and DDoS attacks*

**Defense**

| Before | During | After |
| :--- | :--- | :--- |
| redundant links, rate limiting, firewall and IPS rules. | divert traffic for filtering, inform customers, watch for fraud | Analyze logs, DDoS steals nothing but stops internet / mobile banking |

---

## 6.3 ICT Policy of Nepal, 2072 (2015)

### ① Explain the vision, objectives, goals and major provisions of the ICT Policy of Nepal, 2072.

```text
 Vision
   ↓
 Mission
   ↓
 6 Objectives
   ↓
 Goals (to 2020)
   ↓
 21 Policy areas
   ↓
 Institutions
   ↓
 Implementation
   ↓
 Security provisions
   ↓
 Assumption
   ↓
 Risks
```

| Item | Detail |
| :--- | :--- |
| Vision | Transform Nepal into an information and knowledge-based society |
| Mission | good governance, sustainable development and poverty reduction through ICT. |
| 6 Objectives | Access and Affordability, inclusive development, infrastructure, innovation and research, human resources, good governance |
| Goals (to 2020) | 75% digitally literate, 90% broadband access, Internet for all, 80% of citizen services online, ICT industry 7.5% of GDP |
| 21 Policy areas | access, education, ICT industry, e-commerce, health, agriculture, tourism, telecom infrastructure, cloud computing, security and trust and others |
| Institutions | Ministry of Information and Communications leads; steering committee chaired by the Minister |
| Implementation | National ICT Master Plan / e-strategies and regulatory arrangements, monitoring and evaluation. |
| Security provisions | Electronic Transactions Act 2063, Cyber security cell, mobile banking for financial inclusion, Government Integrated Data Center / cloud. |
| Assumption | High level of political commitment |
| Risks | lower ICT demand, weak monitoring |

---

## 6.4 IT Guidelines issued by NRB

### ① Discuss the major provisions of NRB IT Guideline, 2012 (2068 BS) in August 2012.

| Area | Major provisions |
| :--- | :--- |
| 1. IT governance | Board-approved IT strategy and policy, reviewed at least annually, Information Security Officer (ISO). |
| 2. Information security | risk assessment at least annually. PINs, passwords, firewalls. |
| 3. Information security education | Awareness programs for employees |
| 4. Information disclosure and grievance handling | clear information on services, costs, risks, privacy and security |
| 5. Outsourcing management | accountability stays with the bank. |
| 6. IT operations | master passwords, cryptographic keys, firewall changes. |
| 7. Acquisition development and implementation | required documented and approved before development (every stage of SDLC) |
| 8. Business continuity and DR (Disaster) | BCP, RPO, RTO |
| 9. IS audit | Information-systems audit annually. |
| 10. Fraud management | Identify, document and report all electronic attacks to NRB monthly; customers made aware of frauds. |

∴ Action plan 6 months, full compliance 2 years.

### ② Security provision for electronic banking channels
- ATM → PIN, CCTV
- Online card payment → instant alert (email / SMS)
- Mobile Banking → transaction limits

### ③

| Basis | IT Guidelines (2012) | Cyber Resilience Guidelines (2023) |
| :--- | :--- | :--- |
| Issued | Aug 2012, Bank Supervision Dept. | Aug 2023, Payment Systems Dept. |
| Applies to | Commercial banks (+ BFIs licensed by NRB) | A, B, C, D class BFIs, PSOs, PSPs |
| Key officer | ISO | CISO |

---

## 6.5 Cyber Resilience Guidelines, 2023 (NRB)

### ① Explain the framework of the Cyber Resilience Guidelines, 2023 issued by NRB.

```text
+----------------------------------------------------------------------------+
|                    Three overarching components:                           |
|   [TESTING]      [SITUATIONAL AWARENESS]      [LEARNING AND EVOLVING]      |
|                                                                            |
|                    Five risk management categories:                        |
|          +------------------------------------------------+                |
|          | GOVERNANCE: board, strategy, framework, CISO   |                |
|          +------------------------------------------------+                |
|  [IDENTIFICATION]   [PROTECTION]   [DETECTION]   [RESPONSE AND RECOVERY]   |
|   critical          controls,       monitoring,    resume in 2 hours;       |
|   functions,    →   access,     →   SIEM, SOC, →   settle by end of day     |
|   assets,           network,        logs                                    |
|   dependencies      people                                                  |
+----------------------------------------------------------------------------+
```
*Fig: Structure of Cyber Resilience Guidelines, 2023*

| Part | What the licensed institution is expected to do |
| :--- | :--- |
| 1. Governance | |
| 2. Identification | |
| 3. Protection | |
| 4. Detection | |
| 5. Response & recovery | |
| 6. Testing | |
| 7. Situational awareness | |
| 8. Learning & evolving | |

---

### ② Explain the incident response process with reference to bank.

→ NIST 2025 cycle

```text
                    new finding during containment
              +- - - - - - - - - - - - - - - - - - - - - - +
              v                                              |
 [1. Preparation       ]   [2. Detection        ]   [3. Containment, eradication,]
 [(policy, team,       ] → [& analysis          ] → [recovery                    ]
 [ tools, backup)      ]   [(confirm, clarify,  ]   [(isolate, block accounts,   ]
        ^                  [ restore)           ]   [ restore)                   ]
        |                                                          |
        |                                                          v
        |                                          [4. Post-incident activity    ]
        +--------------------------------------------[(root cause, lessons,       ]
              lessons learned improve preparation     [ report)                   ]
```
*Fig: Incident response life cycle*
