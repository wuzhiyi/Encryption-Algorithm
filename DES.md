#DES
###Description
DES is the archetypal block cipher--an algorithm that takes a fixed-length string of plaintext bits and transforms it through a series of complicated operations into another ciphertext bitstring of the same length. </br>
In the case of DES, the block size is 64 bits. DES also uses a key to customize the transformation, so that decryption can supposedly only be performed by those who know the particular key used to encrypt. The key ostensibly consists of 64 bits; however, only 56 of these are actually used by the algorithm. Eight bits are used solely for checking parity, and are thereafter discarded. Hence the effective key length is 56 bits.</br>
###Structure Overview
<div align="center"><img src="https://cloud.githubusercontent.com/assets/9131176/9484153/e11d75b0-4bda-11e5-844f-1f346e6c39c2.png"></div>

###Structure
The encryption process is made of two permutations (P-boxes) which we call initial and final permutations, and sixteen Feistel rounds.</br>

<div align="center">![img](https://cloud.githubusercontent.com/assets/9131176/9484149/dea08d0e-4bda-11e5-838f-37189a106e81.png)</br></div>

Before the main rounds, the block is divided into two 32-bit halves and processed alternately; this criss-crossing is known as the Feistel scheme. The Feistel structure ensures that decryption and encryption are very similar processes--the only difference is that the subkeys are applied in the reverse order when decrypting. The rest of the algorithm is identical. This greatly simplifies implementation, particularly in hardware, as there is no need for separate encryption and decryption algorithms.(from wikipedia)</br>

###Rounds
DES uses 16 rounds. Each round of DES is a Feistel cipher.</br>


<div align="center"><img src="https://cloud.githubusercontent.com/assets/9131176/9484150/deab572a-4bda-11e5-8d38-46f36f5b321f.png"></br></div>

###Feistel(F) function
The F-function, depicted in below, operates on half a block (32 bits) at a time and consists of four stages:

1. Expansion (P-Box)
2. Key mixing
3. Substitution (S-Boxes)
4. Permutation (Straight P-Box)

<div align="center">![img](https://cloud.githubusercontent.com/assets/9131176/9484147/de73f000-4bda-11e5-877e-cfefc2af7d39.png)</div>

###Expansion P-Box
The 32-bit half-block is expanded to 48 bits using the expansion permutation by duplicating half of the bits. The output consists of eight 6-bit (8 * 6 = 48 bits) pieces, each containing a copy of 4 corresponding input bits, plus a copy of the immediately adjacent bit from each of the input pieces to either side.</br>
###Key mixing
Key mixing--the result is combined with a subkey using an XOR operation. 16 48-bit subkeys--one for each round--are derived from the main key using the key schedule(described below).</br>
###S-Boxes
After mixing in the subkey, the block is divided into eight 6-bit pieces before processing by the S-boxes, or substitution boxes. Each of the eight S-boxes replaces its six input bits with four output bits according to a non-linear transformation, provided in the form of a lookup table. The S-boxes provide the core of the security of DES--without them, the cipher would be linear, and trivially breakable.</br>
###Straight P-Box
Finally, the 32 outputs from the S-boxes are rearranged according to a fixed permutation, the P-box. This is designed so that, after permutation, each S-box's output bits are spread across 4 different S boxes in the next round.</br>
</br>
</br>
back to [Encryption-Algorithm](https://github.com/wuzhiyi/Encryption-Algorithm)</br>
