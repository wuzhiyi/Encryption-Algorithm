#DES
###Structure
The encryption process is made of two permutations (P-boxes) which we call initial and final permutations, and sixteen Feistel rounds.
![img](https://cloud.githubusercontent.com/assets/9131176/9483704/8ed983de-4bd5-11e5-9a52-c10c1db62404.png)
Before the main rounds, the block is divided into two 32-bit halves and processed alternately; this criss-crossing is known as the Feistel scheme. The Feistel structure ensures that decryption and encryption are very similar processes--the only difference is that the subkeys are applied in the reverse order when decrypting. The rest of the algorithm is identical. This greatly simplifies implementation, particularly in hardware, as there is no need for separate encryption and decryption algorithms.(from wikipedia)
###Rounds
DES uses 16 rounds. Each round of DES is a Feistel cipher.
![img](https://cloud.githubusercontent.com/assets/9131176/9483708/9281a71e-4bd5-11e5-8357-05fa70b4ce6c.png)
###Feistel(F) function
The F-function, depicted in below, operates on half a block (32 bits) at a time and consists of four stages:
1. Expansion (P-Box)
2. Key mixing
3. Substitution (S-Boxes)
4. Permutation (Straight P-Box)
![img](https://cloud.githubusercontent.com/assets/9131176/9483697/8b63dda8-4bd5-11e5-91ef-b52c34c81bc4.png)
