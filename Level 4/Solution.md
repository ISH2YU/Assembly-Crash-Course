






```sh

Welcome to ASMLevel4
==================================================

To interact with any level you will send raw bytes over stdin to this program.
To efficiently solve these problems, first run it to see the challenge instructions.
Then craft, assemble, and pipe your bytes to this program.

For instance, if you write your assembly code in the file asm.S, you can assemble that to an object file:
  as -o asm.o asm.S

Note that if you want to use Intel syntax for x86 (which, of course, you do), you'll need to add the following to the start of asm.S:
  .intel_syntax noprefix

Then, you can copy the .text section (your code) to the file asm.bin:
  objcopy -O binary --only-section=.text asm.o asm.bin

And finally, send that to the challenge:
  cat ./asm.bin | /challenge/run

You can even run this as one command:
  as -o asm.o asm.S && objcopy -O binary --only-section=.text ./asm.o ./asm.bin && cat ./asm.bin | /challenge/run

In this level you will be working with registers. You will be asked to modify
or read from registers.

We will now set some values in memory dynamically before each run. On each run
the values will change. This means you will need to do some type of formulaic
operation with registers. We will tell you which registers are set beforehand
and where you should put the result. In most cases, its rax.



Using your new knowledge, please compute the following:
  f(x) = mx + b, where:
    m = rdi
    x = rsi
    b = rdx

Place the result into rax.

Note: there is an important difference between mul (unsigned
multiply) and imul (signed multiply) in terms of which
registers are used. Look at the documentation on these
instructions to see the difference.

In this case, you will want to use imul.

We will now set the following in preparation for your code:
  rdi = 0xe87
  rsi = 0x25ee
  rdx = 0x1d7e

Please give me your assembly in bytes (up to 0x1000 bytes):

```

## Solution

```sh
import pwn
pwn.context.update(arch="amd64")
code = pwn.asm("""

imul rdi, rsi
add rdi, rdx
mov rax, rdi

""")
process = pwn.process("/challenge/run")
process.write(code)
print(process.readall())
```
