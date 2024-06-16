```sh
hacker@assembly-crash-course-level-8:~$ /challenge/run

Welcome to ASMLevel8
==================================================

To interact with any level you will send raw bytes over stdin to this program.
To efficiently solve these problems, first run it once to see what you need
then craft, assemble, and pipe your bytes to this program.

In this level you will be working with registers. You will be asked to modify
or read from registers_use.

We will now set some values in memory dynamically before each run. On each run
the values will change. This means you will need to do some type of formulaic
operation with registers_use. We will tell you which registers_use are set beforehand
and where you should put the result. In most cases, its rax.

In this level you will be working with bit logic and operations. This will involve heavy use of
directly interacting with bits stored in a register or memory location. You will also likely
need to make use of the logic instructions in x86: and, or, not, xor.



Bitwise logic in assembly is yet another interesting concept!
x86 allows you to perform logic operation bit by bit on registers.
For the sake of this example say registers only store 8 bits.
The values in rax and rbx are:
rax = 10101010
rbx = 00110011
'If we were to perform a bitwise AND of rax and rbx using the and rax, rbx instruction'
the result would be calculated by ANDing each pair bits 1 by 1 hence why
it's called a bitwise logic. So from left to right:
1 AND 0 = 0, 0 AND 0 = 0, 1 AND 1 = 1, 0 AND 1 = 0 ...
Finally we combine the results together to get:
rax = 00100010
Here are some truth tables for reference:
    AND          OR           XOR
 A | B | X    A | B | X    A | B | X
---+---+---  ---+---+---  ---+---+---
 0 | 0 | 0    0 | 0 | 0    0 | 0 | 0
 0 | 1 | 0    0 | 1 | 1    0 | 1 | 1
 1 | 0 | 0    1 | 0 | 1    1 | 0 | 1
 1 | 1 | 1    1 | 1 | 1    1 | 1 | 0

Without using the following instructions:
mov, xchg
Please perform the following:
rax = rdi AND rsi
i.e. Set rax to the value of (rdi AND rsi)

We will now set the following in preparation for your code:
rdi = 0x6d62b24e248376c4
rsi = 0x71d0046113d7c199

Please give me your assembly in bytes (up to 0x1000 bytes):
```

## Solution

```python
import pwn
pwn.context.update(arch="amd64")
code = pwn.asm("""

and rax, rdi
and rax, rsi

""" )
process = pwn.process("/challenge/run")
process.write(code)
print(process.readall())

```
