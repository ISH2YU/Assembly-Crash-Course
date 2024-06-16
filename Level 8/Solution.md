```sh
hacker@assembly-crash-course-level-7:~$ /challenge/run

Welcome to ASMLevel7
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



Shifting in assembly is another interesting concept! x86 allows you to 'shift'
bits around in a register. Take for instance, rax. For the sake of this example
say rax only can store 8 bits (it normally stores 64). The value in rax is:
rax = 10001010
If we shift the value once to the left:
shl rax, 1
The new value is:
rax = 00010100
As you can see, everything shifted to the left and the highest bit fell off and
a new 0 was added to the right side. You can use this to do special things to
the bits you care about. It also has the nice side affect of doing quick multiplication,
division, and possibly modulo.
Here are the important instructions:
shl reg1, reg2       <=>     Shift reg1 left by the amount in reg2
shr reg1, reg2       <=>     Shift reg1 right by the amount in reg2
Note: all 'regX' can be replaced by a constant or memory location

Using only the following instructions:
mov, shr, shl
Please perform the following:
Set rax to the 5th least significant byte of rdi
i.e.
rdi = | B7 | B6 | B5 | B4 | B3 | B2 | B1 | B0 |
Set rax to the value of B4

We will now set the following in preparation for your code:
rdi = 0x62de7e71bc6a889e

Please give me your assembly in bytes (up to 0x1000 bytes):
```

## Solution

```python
import pwn
pwn.context.update(arch="amd64")
code = pwn.asm("""
mov rax, rdi
shl rax, 24
shr rax, 56
""" )
process = pwn.process("/challenge/run")
process.write(code)
print(process.readall())
```
