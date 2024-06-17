```sh
hacker@assembly-crash-course-level-6:~$ /challenge/run

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



Another cool concept in x86 is the independent access to lower register bytes.
Each register in x86 is 64 bits in size, in the previous levels we have accessed
the full register using rax, rdi or rsi. We can also access the lower bytes of
each register using different register names. For example the lower
32 bits of rax can be accessed using eax, lower 16 bits using ax,
lower 8 bits using al, etc.
MSB                                    LSB
+----------------------------------------+
|                   rax                  |
+--------------------+-------------------+
                     |        eax        |
                     +---------+---------+
                               |   ax    |
                               +----+----+
                               | ah | al |
                               +----+----+
Lower register bytes access is applicable to all registers_use.

Using only the following instruction(s)
mov
Please compute the following:
rax = rdi modulo 256
rbx = rsi modulo 65536

We will now set the following in preparation for your code:
rdi = 0x42d8
rsi = 0x5d2dc86f

Please give me your assembly in bytes (up to 0x1000 bytes):
```

## Solution

```python
import pwn
pwn.context.update(arch="amd64")
code = pwn.asm("""

mov al, dil
mov bx, si

""" )
process = pwn.process("/challenge/run")
process.write(code)
print(process.readall())
```
