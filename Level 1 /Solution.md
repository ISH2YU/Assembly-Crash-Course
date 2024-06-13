```sh
cd /challenge
```
```sh
run
```
Write your Assembly in ipython

```sh
ipython
```
Set Register :

```sh
Welcome to ASMLevel1
==================================================

To interact with any level you will send raw bytes over stdin to this program.
To efficiently solve these problems, first run it once to see what you need
then craft, assemble, and pipe your bytes to this program.

In this level you will be working with registers. You will be asked to modify
or read from registers_use.



In this level you will work with registers_use! Please set the following:
* rdi = 0x1337

Please give me your assembly in bytes (up to 0x1000 bytes):
```

### Solution 

```sh
import pwn
pwn.context.update(arch="amd64")
code = pwn.asm("""
mov rdi, 0x1337
""" )
process = pwn.process("/challenge/run")
process.write(code)
print(process.readall())
```
