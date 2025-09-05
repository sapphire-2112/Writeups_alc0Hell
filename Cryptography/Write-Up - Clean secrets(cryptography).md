# **Write-Up \- Clean secrets(cryptography)** 

## **Overview**

In this challenge, we were given RSA public parameters (`e`, `n`) along with a signature (`sign`). The task was to analyze the signature, recover the underlying message, and extract the hidden flag.

## **Step 1: Understanding the Provided Values**

The file contained:

* **e** \= 65537 (the standard public exponent)

* **n** \= a 2048-bit RSA modulus

* **sign** \= an integer representing the RSA signature

Since RSA signatures are computed as `s^e mod n` (where `s` is the signature integer), the goal was to recover the message block embedded within the signature.

## **Step 2: Recovering the Signature Block**

Using modular exponentiation, we computed:

`m = sign^e mod n`

This produced a 256-byte block (as expected for a 2048-bit modulus). Converting the result to bytes gave us the signature content.

## **Step 3: Inspecting the Block**

Typical RSA signatures (with PKCS\#1 v1.5 padding) start with `0x00 0x01 0xFF...0x00`, followed by an ASN.1 DigestInfo structure. However, in this case, the recovered block directly contained human-readable ASCII text at the beginning.

Hex preview of the recovered block showed:

`66 6c 61 67 7b 69 6d 5f 73 65 61 72 63 68 69 6e ...`

Which translates to:

`flag{im_searching_for_a_new_hashing_function}`

The rest of the block was filled with padding bytes.

## **Step 4: Extracting the Flag**

The ASCII sequence immediately revealed the hidden flag:

**Flag:**

`flag{im_searching_for_a_new_hashing_function}`

## **Conclusion**

By performing RSA signature recovery (`sign^e mod n`), we successfully extracted the flag embedded inside the signature block. This challenge tested understanding of RSA internals, padding schemes, and data extraction from raw cryptographic operations

