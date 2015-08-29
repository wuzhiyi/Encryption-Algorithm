#AES
###Description
AES is based on a design principle known as a substitution-permutation network, combination of both substitution and permutation, and is fast in both software and hardware.</br>
AES is a variant of Rijndael which has a fixed block size of 128 bits, and a key size of 128, 192 or 256 bits. By contrast, the Rijndael specification _per se_ is specified with block and key sizes that may be any multiple of 32 bits, both with a minimum of 128 and a maximum of 256 bits.</br>
AES operates on a 4×4 column-major order matrix of bytes, termed the _state_.</br>
The key size used for an AES cipher specifies the number of repetitions of transformation rounds that convert the input, called the plaintext, into the final output, called the ciphertext. The number of cycles of repetition are as follows:

* 10 cycles of repetition for 128-bit keys.
* 12 cycles of repetition for 192-bit keys.
* 14 cycles of repetition for 256-bit keys.

Each round consists of several processing steps, each containing four similar but different stages, including one that depends on the encryption key itself. A set of reverse rounds are applied to transform ciphertext back into the original plaintext using the same encryption key.</br>
###Structure
1. Key Expansions--round keys are derived from the cipher key using Rijindael's key schedule. AES requires a separate 128-bit round key block for each round plus one more.
2. Initial Round
	1. AddRoundKey--each byte of the state is combined with a block of the round key using bitwise xor.
3. Rounds
	1. SubBytes--a non-linear substitution step where each byte is replaced with another according to a lookup table.
	2. ShiftRows--a transposition step where the last three rows of the state are shifted cyclically a certain number of steps.
	3. MixColumns--a mixing operation which operates on the columns of the state, combining the four bytes in each column.
	4. AddRoundKey
4. Final Round (no MixColumns)
	1. SubBytes
	2. ShiftRows
	3. AddRoundKey

![img](https://cloud.githubusercontent.com/assets/9131176/9522667/733b56e6-4d08-11e5-9f15-227f89e3d8d9.png)</br>

###The SubBytes step
In the **SubBytes** step, aech byte a(i,j) in the state matrix is replaced with a **SubByte** S(a(i,j)) using an 8-bit substitution box, the Rijndael S-box.</br>
This operation provides the non-linearity in the cipher. The S-box used is derived from the multiplicative inverse over GF(2^8), known to have good non-linearity properties. To avoid attacks based on simple algebraic properties, the S-box is constructed by combining the inverse function with an invertible affine transformation. The S-box is also chosen to avoid any fixed points (and so is a derangement) and also any opposite fixed points.</br>
While performing the decryption, Inverse SubBytes step is used, which requires first taking the affine transformation and then finding the multiplicative inverse (just reversing the steps used in SubBytes step).</br>

###The ShiftRows step
The **ShiftRows** step operates on the rows of the state; it cyclically shifts the bytes in each row by a certain offset. For AES, the first row is left unchanged. Each byte of the second row is shifted one to the left. Similarly, the third and fourth rows are shifted by offsets of two and three respectively.</br>
For blocks of sizes 128 bits and 192 bits, the shiting pattern is the same. Row n is shifted left circular by n-1 bytes. In this way, each colun of the output state of  the **ShiftRows** step is composed of bytes from each column of the input state. (Rijndael variants with a larger block size have slightly different offsets).</br>
For a 256-bit block, the first row is unchanged and the shifting for the seconde, third and fourth row is 1 byte, 3 bytes and 4 bytes respectivley--this change only applies for the Rijndael cipher when used with a 256-bit block, as AES does not use 256-bit blocks. The importance of this step is to avoid the columns being linearly independent, in which case, AES degenerates into four independent block ciphers.</br>
![img](https://cloud.githubusercontent.com/assets/9131176/9522666/72f29a82-4d08-11e5-9819-4ce53501ee4e.png)</br>

###The MixColumns step
In the **MixColumns** step step, the four bytes of each column of the state are combined using an invertible linear transformation. The **MixColumns** function takes four bytes as innput and outputs four bytes, where each input byte affects all four output bytes. Together with **ShiftRows**, **MixColumns** provides diffusion in the cipher.</br>
During this operation, each column is transformed using a fixed matrix.</br>
Matrix multiplication is composed of multiplication and addition of the entries. Entries are 8 bit bytes treated as coefficients of polynomial of order x^7. Addition is simply XOR. Mulitiplication is modulo irreducible polynomial x^8+x^4+x^3+x+1. If processed bit by bit then after shifting a conditional XOR with 0x1B should be performed if the shifted value is larger than 0xFF(overflow must be corrected by subtraction of generating polynomial). These are special cases of the usual multiplication in GF(2^8).</br>
###The AddRoundKey step
In the **AddRoundKey** step, the subkey is combined with the state. For each round, a subkey is derived from the main key using Rijndael's key schedule; each subkey is the same size as the state. The subkey is added by combining each byte of the state with the corresponding byte of the subkey using bitwise XOR.</br>
</br>
</br>
back to [Encryption-Algorithm](https://github.com/wuzhiyi/Encryption-Algorithm)</br>
