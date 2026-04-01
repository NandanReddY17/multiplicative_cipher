# Multiplicative Cipher & Custom Hashing Implementation

This repository contains the implementation of a classical **Multiplicative Cipher** and a custom **Polynomial Rolling Hash function**, written entirely from scratch in Python without the use of external cryptographic libraries.

## Theory

### 1. Multiplicative Cipher
The Multiplicative Cipher is a type of substitution cipher where each letter in the plaintext is multiplied by a key $k$ modulo 26 (the number of letters in the English alphabet).
- **Encryption Equation:** $E(x) = (x \cdot k) \mod 26$
- **Decryption Equation:** $D(x) = (x \cdot k^{-1}) \mod 26$

**Constraint:** The key $k$ must be coprime to 26 (i.e., $\text{gcd}(k, 26) = 1$) to ensure that a modular inverse $k^{-1}$ exists. If it isn't coprime, multiple plaintext letters would map to the same ciphertext letter, making decryption impossible. Valid keys include: 1, 3, 5, 7, 9, 11, 15, 17, 19, 21, 23, 25.

### 2. Custom Polynomial Rolling Hash
To fulfill the hashing requirement, I implemented a custom Polynomial Rolling Hash. This hash function iterates through the string, treating the string's characters as coefficients of a polynomial. 
- **Equation:** $H(s) = \sum_{i=0}^{n-1} s[i] \cdot p^i \mod m$
- **Parameters chosen:** $p = 31$ (a small prime close to the alphabet size) and $m = 10^9 + 9$ (a large prime to minimize collisions). 

This function was chosen because it provides excellent distribution and avalanche properties without relying on standard algorithms like MD5 or SHA, making it a unique, from-scratch solution.

## Instructions to Run

1. Ensure you have Python 3.x installed on your system.
2. Clone this repository to your local machine.
3. Navigate to the project directory.
4. Run the test script via the terminal:
   ```bash
   python test_script.py
Worked ExamplesExample
1Plaintext: HELLO
Key: 7
Ciphertext: XCZZU
Hash of Ciphertext: 0x4d8174a
Decryption Check: XCZZU multiplied by modular inverse 15 $\mod 26$ correctly returns HELLO.

Example 2
Plaintext: WORLD
Key: 5
Ciphertext: GSHDP
Hash of Ciphertext: 0x4875328
Decryption Check: GSHDP multiplied by modular inverse 21 $\mod 26$ correctly returns WORLD.
