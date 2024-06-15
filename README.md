
# Some Basics of Assembbly Language Labs Writeups

I am Using `Pwntools` for this entire challenge 

Its strictly for those who are doing this via SSH 

This is the Format to be used to solve all levels 

```python
import pwn
pwn.context.update(arch="amd64")
code = pwn.asm("""

// Enter Your Assembly Here

""")
process = pwn.process("/challenge/embryoasm")
process.write(code)
print(process.readall())
```

## Under Construction
  All Levels Yet to be Completed
