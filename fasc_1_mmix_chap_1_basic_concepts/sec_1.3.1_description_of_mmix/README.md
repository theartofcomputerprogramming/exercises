# 1.3.1' Description of MMIX

In *Chapter 1, Basic Concepts*, of *Fascicle 1, MMIX*

## Exercises

**1\.** *`[00]`* The binary form of 2009 is (11111011001)<sub>2</sub>; what is 2009 in hexadecimal?

**2\.** *`[05]`* Which of the letters {A, B, C, D, E, F, a, b, c, d, e, f} are odd when considered as (a) hexadecimal digits? (b) ASCII characters?

**3\.** *`[10]`* Four-bit quantities -- half-bytes, or hexadecimal digits -- are often called nybbles. Suggest a good name for two-bit quantities, so that we have a complete binary nomenclature ranging from bits to octabytes.

**4\.** *`[15]`* A kilobyte (kB or KB) is 1000 bytes, and a megabyte (MB) is 1000 kB. What are the official names and abbreviations for larger numbers of bytes?

**5\.** *`[M13]`* If 𝛼 is any string of 0s and 1s, let s(𝛼) and u(𝛼) be the integers that it represents when regarded as a signed or unsigned binary number. Prove that, if x is any integer, we have
<p align=center>
  x = s(𝛼) &nbsp; &nbsp; &nbsp; if and only if &nbsp; &nbsp; &nbsp; x ≡ u(𝛼) (modulo 2<sup>n</sup>) and -2<sup>n-1</sup> ≤ x < 2<sup>n-1</sup>,
</p>
where n is the length of 𝛼

▶ **6\.** *`[M20]`* Prove or disprove the following rule for negating an n-bit number in two's complement notation: "Complement all the bits, then add 1." (For example, **`#0...01`** becomes **`#f...fe`**, then **`#f...ff`**; also **`#f...ff`** becomes **`#0...00`**, then **`#0...01`**)

**7\.** *`[M15]`* Could the formal definitions of **`LDHT`** and **`STHT`** have been stated as
<p align=center>
  s($X) ← s(M<sub>4</sub>[A]) * 2<sup>32</sup> &nbsp; &nbsp; &nbsp; and &nbsp; &nbsp; &nbsp; s(M<sub>4</sub>[A]) ← ⌊s($X)/2<sup>32</sup>⌋,
</p>
thus treating the numbers as signed rather than unsigned

**8\.** *`[10]`* If registers $Y and $Z represent numbers between 0 and 1 in which the binary radix point is assumed to be at the left of each register, (7) illustrates the fact that `MULU` forms a product in which the assumed radix point appears at the left of register `rH`. Suppose, on the other hand, that $Z is an integer, with the radix point assumed at its right, while $Y is a fraction between 0 and 1 as before. Where does the radix point lie after `MULU` in such a case?

**9\.** *`[M10]`* Does the equation s($Y) = s($X) . s($Z) + s(rR) always hold after the instruction **`DIV $X,$Y,$Z`** has been performed?

**10\.** *`[M16]`* Give an example of **`DIV`** in which overflow occurs.

**11\.** *`[M16]`* True or false:

(a) Both **`MUL $X,$Y,$Z`** and **`MULU $X,$Y,$Z`** produce the same result in $X.\
(b) If register `rD` is zero, both **`DIV $X,$Y,$Z`** and **`DIVU $X,$Y,$Z`** produce the same result in $X.

▶ **12\.** *`[M20]`* Although **`ADDU $X,$Y,$Z`** never signals overflow, we might want to know if a carry occurs at the left when adding $Y to $Z. Show that the carry can be computed with two further instructions.

**13\.** *`[M21]`* Suppose MMIX had no **`ADD`** command, only its unsigned counterpart **`ADDU`**. How could a programmer tell whether overflow occurred when computing s($Y)+s($Z)?

**14\.** *`[M21]`* Suppose MMIX had no **`SUB`** command, only its unsigned counterpart **`SUBU`**. How could a programmer tell whether overflow occurred when computing s($Y)-s($Z)?

**15\.** *`[M25]`* The product of two signed octabytes always lies between -2<sup>126</sup> and 2<sup>126</sup>, so it can always be expressed as a signed 16-byte quantity. Explain how to calculate the upper half of such a signed product.

**16\.** *`[M23]`* Suppose MMIX had no **`MUL`** command, only its unsigned counterpart **`MULU`**. How could a programmer tell whether overflow occurred when computing s($Y) * s($Z)?

▶ **17\.** *`[M22]`* Prove that unsigned integer division by 3 can always be done by multiplication:

If register $Y contains any unsigned integer y, and if register $1 contains the constant `#aaaa aaaa aaaa aaab`, then the sequence
```
MULU $0,$Y,$1
GET  $0,rH
SRU  $X,$0,1
```
puts ⌊y/3⌋ into register $X

**18\.** *`[M23]`* Continuing the previous exercise, prove or disprove that the instructions
```
MULU $0,$Y,$1
GET  $0,rH
SRU  $X,$0,2
```
put ⌊y/5⌋ in $X if $1 is an appropriate constant

▶ **19\.** *`[M26]`* Continuing exercises 17 and 18, prove or disprove the following statement: Unsigned integer division by a constant can always be done using "high multiplication" followed by a right shift. More precisely, if 2<sup>𝑒</sup> < z < 2<sup>𝑒+1</sup> we can compute ⌊y/z⌋ by computing ⌊a*y/2<sup>64+𝑒</sup>⌋, where a = ⌈2<sup>64+𝑒</sup>/z⌉, for 0  y < 2<sup>64</sup>

**20\.** *`[16]`* Show that two cleverly chosen MMIX instructions will multiply by 25 faster than the single instruction **`MUL $X,$Y,25`**, if we assume that overflow will not occur

**21\.** *`[15]`* Describe the effects of **`SL`**, **`SLU`**, **`SR`**, and **`SRU`** when the unsigned value in register $Z is 64 or more

▶ **22\.** *`[15]`* Mr. B. C. Dull wrote a program in which he wanted to branch to location `Case1` if the signed number in register $1 was less than the signed number in register $2. His solution was to write
```
SUB $0,$1,$2
BN  $0,Case1
```
What terrible mistake did he make? What should he have written instead?

▶ **23\.** *`[10]`* Continuing the previous exercise, what should Dull have written if his problem had been to branch if s($1) was less than or equal to s($2)?

**24\.** *`[M10]`* If we represent a subset S of {0, 1, ..., 63} by the bit vector
<p align:center>
  ([0 ∈ S], [1 ∈ S], ..., [63 ∈ S]),
</p>
the bitwise operations ∩ and ∪ correspond respectively to set intersection (S ∩ T) and set union (S ∪ T). Which bitwise operation corresponds to set difference (S ∖ T)?

**25\.** *`[10]`* The Hamming distance between two bit vectors is the number of positions in which they differ. Show that two MMIX instructions suffice to set register $X equal to the Hamming distance between v($Y) and v($Z)

**26\.** *`[10]`* What's a good way to compute 64 bit differences, v($X) ← v($Y) ∸ v($Z)?

▶ **27\.** *`[20]`* Show how to use **`BDIF`** to compute the maximum and minimum of eight bytes at a time:
```
b($X) ← max(b($Y), b($Z))
b($W) ← min(b($Y), b($Z))
```

**28\.** *`[16]`* How would you calculate eight absolute pixel differences |b($Y) - b($Z)| simultaneously?

**29\.** *`[21]`* The operation of saturating addition on n-bit pixels is defined by the formula
<p align=center>
  y ∔ z = min(2<sup>n-1</sup>, y + z).
</p>
Show that a sequence of three MMIX instructions will set b($X) ← b($Y) ∔ b($Z)

▶ **30\.** *`[25]`* Suppose register $0 contains eight ASCII characters. Find a sequence of three MMIX instructions that counts the number of blank spaces among those characters. (You may assume that auxiliary constants have been preloaded into other registers. A blank space is ASCII code **`#20`**)

**31\.** *`[22]`* Continuing the previous exercise, show how to count the number of characters in $0 that have odd parity (an odd number of 1 bits)

**32\.** *`[M20]`* True or false: If C = A ⦿ B then C<sup>T</sup> = B<sup>T</sup> ⦿ A<sup>T</sup>. (See (11).)

**33\.** *`[20]`* What is the shortest sequence of MMIX instructions that will cyclically shift a register eight bits to the right? For example, **`#9e 37 79 b9 7f 4a 7c 16`** would become **`#16 9e 37 79 b9 7f 4a 7c`**.

▶ **34\.** *`[21]`* Given eight bytes of ASCII characters in $Z, explain how to convert them to the corresponding eight wyde characters of Unicode, using only two MMIX instructions to place the results in $X and $Y. How would you go the other way (back to ASCII)?

▶ **35\.** *`[22]`* Show that two cleverly chosen **`MOR`** instructions will reverse the left-to-right order of all 64 bits in a given register $Y.

▶ **36\.** *`[20]`* Using only two instructions, create a mask that has **`#ff`** in all byte positions where $Y differs from $Z, **`#00`** in all byte positions where $Y equals $Z.

▶ **37\.** *`[HM30]`* (Finite fields.) Explain how to use **`MXOR`** for arithmetic in a field of 256 elements; each element of the field should be represented by a suitable octabyte.

**38\.** *`[20]`* What does the following little program do?
```
SETL $1,0
SR   $2,$0,56
ADD  $1,$1,$2
SLU  $0,$0,8
PBNZ $0,@-4*3
```

▶ **39\.** *`[20]`* Which of the following equivalent sequences of code is faster, based on the
timing information of Table 1?\
a)
```
BN   $0,@+4*2
ADDU $1,$2,$3
```
versus
```
ADDU $4,$2,$3
CSNN $1,$0,$4
```

b)
```
BN  $0,@+4*3
SET $1,$2
JMP @+4*2
SET $1,$3
```
versus
```
CSNN $1,$0,$2
CSN  $1,$0,$3
```
c)
```
BN   $0,@+4*3
ADDU $1,$2,$3
JMP  @+4*2
ADDU $1,$4,$5
```
versus
```
ADDU $1,$2,$3
ADDU $6,$4,$5
CSN  $1,$0,$6
```
d, e, f) Same as (a), (b), and (c), but with **`PBN`** in place of **`BN`**.

**40\.** *`[10]`* What happens if you **`GO`** to an address that is not a multiple of 4?

**41\.** *`[20]`* True or false:\
a) The instructions `CSOD $X,$Y,0` and `ZSEV $X,$Y,$X` have exactly the same effect.\
b) The instructions `CMPU $X,$Y,0` and `ZSNZ $X,$Y,1` have exactly the same effect.\
c) The instructions `MOR $X,$Y,1` and `AND $X,$Y,#ff` have exactly the same effect.\
d) The instructions `MXOR $X,$Y,#80` and `SR $X,$Y,56` have exactly the same effect.

**42\.** *`[20]`* What is the best way to set register $1 to the *absolute value* of the number in register $0, if $0 holds (a) a signed integer? (b) a floating point number?

▶ **43\.** *`[28]`* Given a nonzero octabyte in $Z, what is the fastest way to count how many leading and trailing zero bits it has? (For example, **`#13fd8124f32434a2`** has three leading zeros and one trailing zero.)

▶ **44\.** *`[M25]`* Suppose you want to emulate 32-bit arithmetic with MMIX. Show that it is easy to add, subtract, multiply, and divide signed tetrabytes, with overflow occurring whenever the result does not lie in the interval [-2<sup>31</sup> .. 2<sup>31</sup>).

**45\.** *`[10]`* Think of a way to remember the sequence DVWIOUZX.

**46\.** *`[05]`* The all-zeros tetrabyte **`#00000000`** halts a program when it occurs as an MMIX instruction. What does the all-ones tetrabyte **`#ffffffff`** do?

**47\.** *`[05]`* What are the symbolic names of opcodes **`#DF`** and **`#55`**?

**48\.** *`[11]`* The text points out that opcodes **`LDO`** and **`LDOU`** perform exactly the same operation, with the same efficiency, regardless of the operand bytes X, Y, and Z. What other pairs of opcodes are equivalent in this sense?

▶ **49\.** *`[22]`* After the following "number one" program has been executed, what changes to registers and memory have taken place? (For example, what is the final setting of $1? of rA? of rB?)
```
NEG     $1,1
STCO    1,$1,1
CMPU    $1,$1,1
STB     $1,$1,$1
LDOU    $1,$1,$1
INCH    $1,1
16ADDU  $1,$1,$1
MULU    $1,$1,$1
PUT     rA,1
STW     $1,$1,1
SADD    $1,$1,1
FLOT    $1,$1
PUT     rB,$1
XOR     $1,$1,1
PBOD    $1,@-4*1
NOR     $1,$1,$1
SR      $1,$1,1
SRU     $1,$1,1
```

▶ **50\.** *`[14]`* What is the execution time of the program in the preceding exercise?

**51\.** *`[14]`* Convert the "number one" program of exercise 49 to a sequence of tetrabytes in hexadecimal notation.

**52\.** *`[22]`* For each MMIX opcode, consider whether there is a way to set the X, Y, and Z bytes so that the result of the instruction is precisely equivalent to **`SWYM`** (except that the execution time may be longer). Assume that nothing is known about the contents of any registers or any memory locations. Whenever it is possible to produce a no-op, state how it can be done. Examples: **`INCL`** is a no-op if X = 255 and Y = Z = 0. BZ is a no-op if Y = 0 and Z = 1. **`MULU`** can never be a no-op, since it affects rH.

**53\.** *`[15]`* List all MMIX opcodes that can possibly change the value of rH.

**54\.** *`[20]`* List all MMIX opcodes that can possibly change the value of rA.

**55\.** *`[21]`* List all MMIX opcodes that can possibly change the value of rL.

▶ **56\.** *`[28]`* Location **`#2000000000000000`** contains a signed integer number, *x*. Write two programs that compute *x*<sup>13</sup> in register $0. One program should use the minimum number of MMIX memory locations; the other should use the minimum possible execution time. Assume that *x*<sup>13</sup> fits into a single octabyte, and that all necessary constants have been preloaded into global registers.

▶ **57\.** *`[20]`* When a program changes one or more of its own instructions in memory, it is said to have *self-modifying code*. MMIX insists that a **`SYNCID`** command be issued before such modified commands are executed. Explain why self-modifying code is usually undesirable in a modern computer.

**58\.** *`[50]`* Write a book about operating systems, which includes the complete design of an NNIX kernel for the MMIX architecture.
