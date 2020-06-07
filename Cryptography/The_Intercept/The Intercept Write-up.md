# The Intercept Write-up


-----
### Category: Steganography

### Challenge Brief:

The raid at location seven has given us the encrypted as well as decrypted message.  Can you use this information to find the cipher key? It will help us decrypt all other messages we have intercepted so far.


-----


### Solution:

- The user is given a .txt file with the plaintext and ciphertext recovered. 

- The user has to recover the key using this information so that all previous intercepted communications can be decrypted.


-----



The logic is like this:

- While encrypting, the key is added to the plaintext to get encrypted text.

- So subtracting the plaintext form the encryption text will give the key.

  - Plaintext: MEET UNDER THE BRIDGE AT NINE

  - Ciphertext: OMTA YEGMJ VJM QYMUJM SV PQCL


- You can use an online tool to decrypt the cyphertext with the plaintext.

- Using **MEET UNDER THE BRIDGE AT NINE** to decrypt **OMTA YEGMJ VJM QYMUJM SV PQCL** you will find the key **CIPH ERDIS CCI PHERDI SC CIPH**

This is the key **CIPHERDISC** repeated.


The flag here is `HilltopCTF{CIPHERDISC}`

