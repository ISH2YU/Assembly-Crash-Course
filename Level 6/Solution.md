## Concept 
In the Earlier Level we Studied about the `Div` Instruction 

We have to Find Modulus of which means remainder when we divide rdi and rsi

- Quotient : rax
- Remainder : rdx 

Since in This Question we are only interested in Remainder , 

Just Move the value of rdx to rax which is getting checked you will get the flag




```sh
hacker@assembly-crash-course-level-5:~$ /challenge/run

Welcome to ASMLevel6
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



Modulo in assembly is another interesting concept! x86 allows you to get the
remainder after doing a division on something. For instance:
10 / 3  ->  remainder = 1
You can get the remainder of a division using the instructions introduced earlier
through the div instruction.
In most programming languages we refer to mod with the symbol '%'.

Please compute the following:
rdi % rsi
Place the value in rax.

We will now set the following in preparation for your code:
rdi = 0x11857d73
rsi = 0x3fff

Please give me your assembly in bytes (up to 0x1000 bytes):
```


## Solution

```python
import pwn
pwn.context.update(arch="amd64")
code = pwn.asm("""

mov rax, rdi
div rsi
mov rax, rdx

""")
process = pwn.process("/challenge/run")
process.write(code)
print(process.readall())
```
