# Level 1: Set a Register Value

In the General Tips, the way to execute ARM64 instructions in the dojo had been given 
```
#!/usr/bin/env python3
from pwn import *
context.arch = 'aarch64'

asm_bytes = asm("""
  PUT YOUR AARCH64 ASSEMBLY HERE
  """)

with process('/challenge/run') as p:
  p.send(asm_bytes)
  p.stdin.close()
  p.interactive()
```
I set the arbitrary general-purpose register of AArch64 `X1` to `12`, and upon execution, it displayed that I had to set the value to `1337` in hex. `MOV X1, #0x1337` and got the flag: pwn.college{02JJHQ12Aep2RksvGER9EL5T_Lj.dlTM2MDL3IjN0czW}

# Level 2: Set a Register to a Large Value

Now, by a large value it had to mean more than 16 bits, and since it is 64 bit arch, i can store 64 bits in a general purpose register. 
however, I cannot pass all the bits at once since it needs some bits for the OPCODE itself. For example: `MOV X1, #0x1337` is actually `0xd28026a1
` using objdump. So anyways, MOV allows only 16 bit values at once. 

```

asm_bytes = asm("""
    movz x1, #0xbeef
    movk x1, #0xdead, lsl #16

""")
```
I initially tried moving random values but it wanted me to set x1 to 0xdeadbeef. x1 is set to `0x000000000000beef` after the first MOV (MOV is just MOVZ, meaning it doesn't shift the value insertion position i.e. starts inserting values into register at 0th bit) and then lsl shifts the incoming 0xdead to start insertion at 16th bit. 
flag: pwn.college{wwsigwa5pvsF4Bk8Hyrik1Vqq0n.dBjM2MDL3IjN0czW}

