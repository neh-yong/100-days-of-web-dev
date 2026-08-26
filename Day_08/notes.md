# Cybersecurity & Cryptography

## Overview

Today I learned about **Cybersecurity** and how **Cryptography** is one of the fundamental technologies used to protect information.

I then studied IBM's article **"What is Cryptography?"**, which explains how cryptography protects digital information, the principles behind it, common use cases, different types of cryptography, cryptographic keys, hashing, digital signatures, and the future of cryptography.

---

# 1. What is Cybersecurity?

**Cybersecurity** is the practice of protecting systems, networks, applications, and data from unauthorized access, attacks, damage, or theft.

Cryptography is an important part of cybersecurity because it helps protect sensitive information from attackers.

### Relationship

```text
Cybersecurity
      │
      ├── Network Security
      ├── Application Security
      ├── Access Control
      ├── Threat Detection
      └── Cryptography
              │
              ├── Encryption
              ├── Hashing
              ├── Digital Signatures
              └── Key Management
```

**Key idea:**

> Cryptography is a tool used within the larger field of cybersecurity.

---

# 2. What is Cryptography?

Cryptography is the practice of using coded algorithms to protect information so that unauthorized people cannot read or access it.

The word comes from the Greek word **"kryptos"**, meaning **hidden**.

Cryptography can protect different types of digital information:

* Text
* Images
* Video
* Audio

---

# 3. Plaintext → Ciphertext

The basic idea of encryption is to transform readable information into an unreadable format.

```text
Plaintext
   │
   │ Encryption + Key
   ▼
Ciphertext
   │
   │ Decryption + Key
   ▼
Plaintext
```

### Plaintext

The original, readable information.

Example:

```text
"Hello"
```

### Ciphertext

The encrypted, unreadable version.

```text
x7@k91...
```

Only someone with the appropriate key should be able to decrypt the ciphertext.

---

# 4. Four Core Principles of Modern Cryptography

Modern cryptography is built around four important security principles.

## 1. Confidentiality

Only authorized people should be able to access the information.

```text
Sender ──🔒──> Receiver
             ❌ Attacker
```

---

## 2. Integrity

Data should not be modified without the modification being detected.

Example:

```text
Original:
Transfer $100

Modified:
Transfer $1000

       ↓

Integrity check detects the change
```

---

## 3. Non-repudiation

The sender cannot later deny that they created or sent the information.

Digital signatures are an important mechanism for achieving this.

---

## 4. Authentication

Cryptography can help verify:

* Who sent the information
* Who received it
* Where the information came from
* Where it is going

---

# 5. Why is Cryptography Important?

Cryptography is used extensively in modern digital systems to protect sensitive information such as:

* Credit card information
* E-commerce transactions
* Private messages
* Banking information
* Enterprise data

It is also important for protecting classified and sensitive information at a national-security level.

---

# 6. Common Uses of Cryptography

## Passwords

Cryptographic techniques can be used to protect stored passwords so that services don't need to keep passwords as readable plaintext.

> **Important:** Passwords are generally protected using **hashing**, rather than reversible encryption.

---

## Cryptocurrency

Cryptography is fundamental to cryptocurrencies such as:

* Bitcoin
* Ethereum

It helps protect wallets, verify transactions, and prevent fraud.

---

## Secure Web Browsing

Protocols such as **TLS** use cryptographic techniques to protect communication between a browser and a web server.

This helps defend against:

* Eavesdropping
* Man-in-the-middle (MitM) attacks

Example:

```text
Browser
   │
   │ 🔒 TLS
   ▼
Web Server
```

This is one reason websites use:

```text
https://
```

instead of:

```text
http://
```

---

## Electronic Signatures

Cryptographic digital signatures can help verify documents and prevent unauthorized modification or forgery.

---

## Authentication

Cryptography can help verify someone's identity when accessing systems such as:

* Online banking
* Secure networks
* Online accounts

---

## Secure Communication

End-to-end encryption can protect communications such as:

* Instant messages
* Video conversations
* Emails

Applications such as **WhatsApp** and **Signal** use end-to-end encryption to provide privacy and security.

---

# 7. Types of Cryptography

There are two major types of encryption:

1. **Symmetric Cryptography**
2. **Asymmetric Cryptography**

Hybrid systems can combine both approaches.

---

# 8. Symmetric Cryptography

Symmetric cryptography uses **one shared secret key** for both encryption and decryption.

```text
             Same Secret Key
                  🔑
                   │
Message ──> Encryption ──> Ciphertext
                              │
                              ▼
                         Decryption
                              │
                              ▼
                           Message
```

Both sender and receiver need access to the same secret key.

### Example

**AES (Advanced Encryption Standard)** is a symmetric encryption algorithm.

### Advantages

* Fast
* Efficient
* Good for large amounts of data

### Historical Example

The **Caesar Cipher** is an early example of symmetric encryption.

For example:

```text
CAT
 ↓
FDW
```

Each letter is shifted three positions forward.

The receiver reverses the shift using the same secret.

---

# 9. Asymmetric Cryptography

Asymmetric cryptography uses **two keys**:

* Public key
* Private key

```text
Public Key  🔓
Private Key 🔐
```

The public key can be shared, while the private key must remain secret.

### Basic Concept

```text
Sender
   │
   │ Uses Receiver's Public Key
   ▼
Encrypted Message
   │
   ▼
Receiver
   │
   │ Uses Private Key
   ▼
Original Message
```

A major advantage is that the private key does not need to be shared over the network.

### Example

**RSA** is a well-known public-key cryptographic algorithm.

---

# 10. Symmetric vs Asymmetric Cryptography

| Feature        | Symmetric        | Asymmetric                           |
| -------------- | ---------------- | ------------------------------------ |
| Keys           | One shared key   | Public + private key                 |
| Speed          | Faster           | Slower                               |
| Large data     | Very suitable    | Less suitable                        |
| Key sharing    | More challenging | Easier                               |
| Example        | AES              | RSA                                  |
| Main advantage | Performance      | Secure key exchange / authentication |

### Important

Asymmetric cryptography isn't automatically "more secure" in every situation. Security depends on factors such as the algorithm, key size, and implementation.

---

# 11. Cryptographic Keys

A **cryptographic key** is information used by a cryptographic algorithm to encrypt, decrypt, sign, or verify data.

Modern cryptographic keys can contain many bits, such as:

* 128 bits
* 256 bits
* 2048 bits

Key management includes:

* Generation
* Exchange
* Storage
* Usage
* Destruction
* Replacement

---

# 12. Brute-Force Attacks

A brute-force attack attempts to try possible keys until the correct one is found.

```text
Ciphertext
    │
    ▼
Try Key 1 ❌
Try Key 2 ❌
Try Key 3 ❌
...
Try Key N ✅
```

Larger key sizes dramatically increase the number of possible combinations, making brute-force attacks much more difficult.

### Key Idea

```text
Larger Key
    ↓
More Possible Combinations
    ↓
More Computational Work
    ↓
Harder Brute Force
```

---

# 13. Cryptographic Algorithms

An encryption algorithm transforms plaintext into ciphertext.

Two common categories include:

### Block Cipher

Encrypts data in fixed-size blocks.

Example:

```text
AES
```

### Stream Cipher

Encrypts data as a continuous stream, such as bit by bit.

---

# 14. Hash Functions

A **hash function** transforms input data into a fixed-length hash value.

```text
Input
  │
  ▼
Hash Function
  │
  ▼
Fixed-Length Hash
```

Hashing is useful for verifying **data integrity**.

### Important Difference

Encryption:

```text
Data → Encryption → Ciphertext
Ciphertext → Decryption → Data
```

Hashing:

```text
Data → Hash → Hash Value
```

A cryptographic hash is designed so that recovering the original input from the hash is computationally difficult.

---

# 15. Digital Signatures

Digital signatures use cryptographic techniques to:

* Verify the sender
* Verify that data has not been modified
* Provide non-repudiation

They are commonly used for digitally signing important documents and data.

---

# 16. The Future of Cryptography

As technology advances, cryptography continues to evolve in response to increasingly sophisticated attacks.

Two important areas discussed in the article are:

* **Elliptic Curve Cryptography (ECC)**
* **Quantum Cryptography**

---


## Quantum Cryptography

Quantum cryptography uses principles of **quantum mechanics** rather than relying only on traditional mathematical assumptions.

A key idea is that observing a quantum state changes it, meaning an attempt to intercept quantum information can potentially be detected.

However, quantum cryptography currently faces practical challenges, including specialized infrastructure, limited transmission range, and error-related issues.

---

# 17. The Big Picture

The concepts learned today connect together like this:

```text
                 CYBERSECURITY
                      │
                      ▼
                CRYPTOGRAPHY
                      │
        ┌─────────────┼─────────────┐
        ▼             ▼             ▼
    Encryption      Hashing     Digital Signatures
        │             │             │
        ▼             ▼             ▼
 Confidentiality   Integrity   Authentication
                              + Non-repudiation
```

And encryption itself can be divided into:

```text
             ENCRYPTION
                 │
        ┌────────┴────────┐
        ▼                 ▼
   Symmetric          Asymmetric
        │                 │
        ▼                 ▼
       AES               RSA
   One shared       Public + Private
       key                keys
```

---

# Key Takeaways

1. **Cybersecurity** is the broader field of protecting systems and information.
2. **Cryptography** is one of the major technologies used to achieve that protection.
3. Encryption transforms **plaintext → ciphertext**.
4. Decryption transforms **ciphertext → plaintext** using the appropriate key.
5. Modern cryptography focuses on **confidentiality, integrity, authentication, and non-repudiation**.
6. **Symmetric cryptography** uses one shared key and is fast.
7. **Asymmetric cryptography** uses public and private keys and is useful for secure key exchange and authentication.
8. **Hashing** is primarily used to verify data integrity and is not the same as encryption.
9. **Digital signatures** provide authentication, integrity, and non-repudiation.
10. **Key management** is a critical part of practical cryptography.
11. **ECC** provides strong public-key cryptography with smaller keys.
12. **Quantum cryptography** explores using quantum mechanics to secure communications.

---

# New Concepts Learned

* Cybersecurity
* Cryptography
* Cryptology
* Plaintext
* Cryptanalysis
* Ciphertext
* Encryption
* Decryption
* Cryptographic Key
* Symmetric Cryptography
* Asymmetric Cryptography
* AES
* RSA
* Hash Functions
* Digital Signatures
* Key Management
* Brute-Force Attack
* Block Cipher
* Stream Cipher
* TLS
* End-to-End Encryption
* Quantum Cryptography

---

# Article

**IBM — What is Cryptography?**
