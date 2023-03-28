
- WEP employs a secret key of either a 40- or 104-bits, which are shared between access-points and mobile devices. 
- These secret keys are concatenated with 24-bit initialization vectors (IV) to form what is casually described as 64-bit or 128-bit encryption - marketed as _silver_ or _gold_ wireless Ethernet cards. 
- The 64- or 128-bit key provides input to a pseudo-random number generator (PRNG) - the RC4 encryption algorithm, known as a _stream cipher_, producing an infinite pseudo-random _keystream_.
- ![[Screenshot 2023-03-28 at 8.01.00 pm.png]]
- To prevent against modification in transit, the common CRC-32 checksum (ICV) is calculated over the original plaintext, and appended to produce the total payload.
- The sender XORs the keystream with the payload to produce ciphertext. This results in ciphertext that is the same length as the original payload.
- ![[Screenshot 2023-03-28 at 8.01.40 pm.png]]
- The receiver has a copy of the same key, and uses it to initialize and generate the identical keystream. XORing the keystream with the ciphertext yields the original plaintext and the integrity of the original data may be verified by recalculating the CRC-32.