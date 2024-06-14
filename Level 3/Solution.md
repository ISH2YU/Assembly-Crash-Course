```sh
/challenge/run
```

Write your Assembly in ipython

```sh
ipython
```
Addition

```sh
hacker@assembly-crash-course-level-2:~$ /challenge/run

Welcome to ASMLevel2
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


Many instructions exist in x86 that allow you to do all the normal
math operations on registers_use and memory. For shorthand, when we say
A += B, it really means, A = A + B. Here are some useful instructions:
add reg1, reg2       <=>     reg1 += reg2
sub reg1, reg2       <=>     reg1 -= reg2
imul reg1, reg2      <=>     reg1 *= reg2
div  is a littler harder, we will discuss it later.
Note: all 'regX' can be replaced by a constant or memory location

Do the following:
* add 0x331337 to rdi

We will now set the following in preparation for your code:
rdi = 0xc78

Please give me your assembly in bytes (up to 0x1000 bytes): 
```

## Solution 

```sh
import pwn
pwn.context.update(arch="amd64")
code = pwn.asm("""

""")
process = pwn.process(/challenge/run)
process.write(code)
print(process.readall())
```
