# 1. CRYPTOGRAPHY

⭐ **Definition:** Cryptography is the technique of securing information and communication using codes, so only the intended person can read and use it. This stops unauthorized access.

**Used for:** protecting data privacy, secure web browsing (HTTPS), card and online transactions, and digital signing.

**Services it gives:** Confidentiality, Integrity, Authentication, Non-repudiation.

## Basic Concepts

| Term | Meaning |
|------|---------|
| **Plain text** | Original readable message (e.g., "Send Rs 500") |
| **Cipher text** | Scrambled unreadable message (e.g., A4$h*L@9) |
| **Encryption** | Plain text → Cipher text |
| **Decryption** | Cipher text → Plain text |
| **Key** | Secret value used to lock or unlock. Security depends on the key, not the algorithm. |

```text
Plain Text ──[Encryption + Key]──> Cipher Text ──[Decryption + Key]──> Plain Text
 (sender)                          (travels on network)                 (receiver)
```

---

# TYPES OF CRYPTOGRAPHY ⭐

```text
                 Cryptography
        ┌────────────┼─────────────┐
   Symmetric key  Asymmetric key  Hash function
```

## (a) Symmetric Key

- Same key encrypts and decrypts.
- Fast, good for large data.
- **Problem:** both sides must share the key secretly, which is hard.
- **Examples:** AES (modern, strong), DES (old, weak).

```text
Plain ─[Encrypt: Key K]─> Cipher ─[Decrypt: same Key K]─> Plain
```

## (b) Asymmetric Key

- Two keys: public key (shared with everyone) and private key (kept secret).
- Encrypt with the receiver's public key, and the receiver decrypts with their private key.
- Slower, but solves the key sharing problem.
- **Examples:** RSA, Elliptic Curve.

```text
Plain ─[Encrypt: Receiver's PUBLIC key]─> Cipher ─[Decrypt: Receiver's PRIVATE key]─> Plain
```

## (c) Hash Function

- No key. Turns any data into a fixed-length digest (e.g., `7ac67882...`).
- One-way: you cannot get the original back.
- A small change in data gives a totally different hash.
- Used for integrity check, password storage. **Examples:** SHA-256, MD5.

```text
abc / 123456 / file ──> [Hash Function] ──> 7ac67882...  (fixed length)
```

## ⭐ Comparison Table

| Point | Symmetric | Asymmetric | Hash |
|-------|-----------|------------|------|
| **Keys** | 1 shared key | 2 keys (public + private) | No key |
| **Speed** | Fast | Slow | Fast |
| **Key sharing** | Hard | Easy | Not needed |
| **Keys for n users** | n(n−1)/2 | 2n | none |
| **Reversible?** | Yes | Yes | No |
| **Used for** | Bulk data, files | Key exchange, signatures | Integrity, passwords |
| **Example** | AES | RSA | SHA-256 |

> **Memory line:** Symmetric gives speed. Asymmetric solves key sharing. Hash checks integrity.

## Banking use ⭐

Online banking combines both (this is TLS/HTTPS):

1. Server sends a CA-signed certificate.
2. Browser verifies it.
3. Asymmetric method agrees a session key.
4. Data is encrypted with AES (symmetric).
5. Extra protection: OTP, digital signature, integrity codes.

> **NRB rule line:** NRB IT Guidelines require strong cryptography, end-to-end encryption of PIN/password, and more than one authentication factor for internet-banking fund transfers.

---

# 2. CRYPTOGRAPHIC PROTOCOLS

**Definition:** A set of rules and steps that uses cryptography to achieve secure communication, authentication, key exchange, or message integrity.

| Protocol | Full form | One-line use |
|----------|-----------|--------------|
| **SSL** | Secure Sockets Layer | Old Internet security, replaced by TLS |
| **TLS** | Transport Layer Security | Secures web traffic (HTTPS) |
| **SSH** | Secure Shell | Secure remote login |
| **IPSec** | Internet Protocol Security | Secures IP traffic, used in VPN |
| **PGP** | Pretty Good Privacy | Encrypt and sign email or files |
| **S/MIME** | Secure/Multipurpose Internet Mail Extensions | Encrypt and sign email |
| **Kerberos** | (no common full form) | Ticket-based user authentication |

> **Quick memory:** Web = TLS. Remote login = SSH. VPN = IPSec. Email = PGP / S/MIME. Login tickets = Kerberos.

---

# 3. DIGITAL SIGNATURE ⭐⭐

**Definition:** A value created from a message using the sender's private key. Anyone with the sender's public key can check who signed it and that it is unchanged.

**Why needed:** Encryption hides data but does not prove who sent it. A signature = Hash + Public-key cryptography.

**Services:** Authentication, Integrity, Non-repudiation. ⚠️ It does not give confidentiality by itself.

## Figure

```text
SENDER (Signing)                          RECEIVER (Verification)

Message                                   Received Message
   ↓                                         ↓
Hash function                             Hash function
   ↓                                         ↓
Digest                                    Digest 1 ──────────┐
   ↓                                                         ↓
Sign with sender's PRIVATE key            Received Signature      Compare
   ↓                                         ↓                    Digest 1 = Digest 2 ?
Signature                                 Verify with sender's    YES → genuine & unaltered
   ↓                                      PUBLIC key              NO  → reject
Send: Message + Signature                    ↓
                                          Digest 2 ──────────┘
```

## How it works (steps)

1. **Signing:** Hash the message → encrypt digest with private key → send message + signature.
2. **Verification:** Hash the received message (Digest 1) → decrypt signature with public key (Digest 2) → if equal, valid. If not, reject.

## Applications ⭐

- Document integrity (contracts, legal papers, financial transactions)
- Sender authentication
- Non-repudiation (sender cannot deny)
- Software distribution (software not tampered)
- **Banking:** CA-signed server certificate, signed payment files, signed mobile apps and updates, signed e-statements

## Advantages ⭐

- Strong proof of identity and integrity
- Prevents forgery (needs private key)
- Non-repudiation (legally valuable)
- Saves time and paper
- Works for automated systems (thousands of transactions)

## Extra lines

- **Certificate Authority (CA)** links a public key to an identity and signs it. The whole trust system is called **PKI**.
- **Nepal:** Electronic Transactions Act, 2063 recognises digital signatures. Certifying authorities work under the Controller of Certification.

> **Conclusion:** Signing with the private key and verifying with the public key gives an electronic instruction the force of a signed document.
