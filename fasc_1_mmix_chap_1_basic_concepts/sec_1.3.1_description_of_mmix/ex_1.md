# Exercise 1
From *1.3.1' Description of MMIX*, in *Chapter 1, Basic Concepts*, of *Fascicle 1, MMIX*

## Problem

**1\.** *`[00]`* The binary form of 2009 is (11111011001)<sub>2</sub>; what is 2009 in hexadecimal?

## Submissions

### Submission 1

By Zartaj, 2020-10-01

#### Answer
`0x7d9`

#### Work
(11111011001)<sub>2</sub>

Separate bits into chunks of 4 from the right since four bits represent the values 0-15 (0000-1111) - and that's exactly what one hex digit represents

Why from the right instead of the left?

Because that's the meaning of the decimal or binary place system - each position or place is for a power of the base of the number system - 10 for decimal, 2 for binary - and the position thus the power is counted from the rightmost place beginning from 0.

```
0111    1101    1001
7       d       9
```
