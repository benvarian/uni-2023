## 8.1 what is network security 
what you want from a network
	- Confidentiality 
	- Message integrity
	- End-to-end auth
	- Operational security

## 8.2 principles of cryptography 

### 8.2.1 symmetric key cryptography
- cipher text only 
	- only know the cipher message 
- known cipher 
	- know some of the algorithms corresponding characters 
- chosen
	- have access to og message before encryption so know everything

block cipher
- have a block of data, then divide it up into sections, and encrypt each singular block 
- usually k = 64 so its harder to decrypt 

cipher-block chaining 
- sends one random value with the first message 
- have the sender and receiver use the computed blocks in place of the subsequent random number

public private key stuff
- basically person a uses b public key to encrypt and person b uses private key to decrypt message 