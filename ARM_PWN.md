I followed this [video](https://youtu.be/gfmRrPjnEw4?si=G8noL4Ux3Dw3qRP6).

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

# Level 3: Basic Arithmetic

I had to perform some basic arithmetic, moved values into X1,X2 and added them into X0 but the program needed me to perform `mx+b` where m was X0, x was X1, b was X2 and had to place the value into X0
```
asm_bytes = asm("""
    MUL X0, X0, X1     // X0 = X0*X1 (mx)
    ADD X0, X0, X2     // X0 = X0 + X2 (mx+b)
""")
```
flag: pwn.college{MdKm-e5xUqXV-7QA9OfNY0Bl5i5.dFjM2MDL3IjN0czW}

# Level 4: Efficient Arithmetic

It wanted to perform the same function in one operation. Quick search: MADD allowed multiply and add in the same operation 
```
asm_bytes = asm("""
     MADD X0, X0, X1, X2 (destination, multiply1, multiply2, add)
""")
```
flag: pwn.college{szWawLzvPC7_tegnhauU_lX5c_4.dJjM2MDL3IjN0czW}

# Level 5: Modulo Operation

Modulo doesn't have a dedicated OPCODE and so it had to be performed by its definition which is to find the remainder: Dividend - Quotient*Divisor
```
asm_bytes = asm("""
    UDIV X2, X0, X1        // X2 = X0 / X1
    MSUB X0, X2, X1, X0    // X0 = X0 - (X2 * X1)
""")
```
UDIV is for unsigned division, in AMD64 it needs to explicitly know signed div from unsigned div, and MSUB is for Multiply-subtraction like MADD
flag: pwn.college{wbnV-4V-4D_UsOeSEaJDhR2jy8g.dNjM2MDL3IjN0czW}

# Level 6: Shifting

The program was about LSL and RSL shifting.  X1 = | B7 | B6 | B5 | B4 | B3 | B2 | B1 | B0 |
        Set X0 to the value of B3

`We will now set the following in preparation for your code:
        X0 = 0x7c8c1616626683bb`
```
asm_bytes = asm("""
    LSL X0, X0, #32
    LSR X0, X0, #56
""")
```
flag: pwn.college{8Oq1qabADqST3TaFcLTv2GwSIol.dRjM2MDL3IjN0czW}

# Level 7: Loading and storing values (Unsolved)

So it should've been simple, load and store values after adding. I tried multiple times, using literal pools (LDR X1, =0xADDR), by building addresses using 16 bit MOV immediates into registers, by traversing using [X1, #8], but nothing worked. It gave CPU error or no error and set the X0 register to the correct value that should've been and yet no flag. I will revisit at a later time.

# Level 8: Loading and storing pairs

The level needed to work with LDP and STP which is load pair and store pair. Now because it did not allow LDR, I had to build the base address using MOV and MOVK (allowed), and then use LDP to load the pair into X1, X2 and STP to store [X0, #0x10] to X1, X2 pair.
```
asm_bytes = asm("""
MOV    X0, #0x4000, LSL #0      
MOVK   X0, #0x40,    LSL #16    

LDP     X1, X2, [X0]              // load X1 = [0x404000], X2 = [0x404008]
STP     X1, X2, [X0, #0x10]       // store X1 to 0x404010, X2 to 0x404018

""")
```
flag: pwn.college{0RfBCCxD4o5G8XASZrBRMPjy_b3.dZjM2MDL3IjN0czW}

# Level 9: Working with Stack

Now here 8 QWORDS had to be popped and taken average of. However, the program gave a little note about maintaining 16 byte alignment when working with SP in AArch64. Since a QWORD is 64 bits, that meant popping two adjacent QWORDS in one go. Which meant popping them as a pair. Then computing the sum, and average using ADD and UDIV. Now lastly, pushing it onto stack while keeping the alignment meant also pushing some other value into the adjacent pair. I looked online and the way this is done as a standard is using the zero register. So stack grows downward with the X0 computed average and zero values. 

```
asm_bytes = asm("""
LDP X0, X1, [SP], #16     //16 byte alignment as per requirement
LDP X2, X3, [SP], #16
LDP X4, X5, [SP], #16
LDP X6, X7, [SP], #16

ADD X0, X0, X1
ADD X0, X0, X2
ADD X0, X0, X3
ADD X0, X0, X4
ADD X0, X0, X5
ADD X0, X0, X6
ADD X0, X0, X7

MOV X1, #8
UDIV X0, X0, X1

STP X0, XZR, [SP, #-16]!
""")
```
flag: pwn.college{4JBUtaVhqBauVoWVGT2hY3TeYoT.ddjM2MDL3IjN0czW}

# Level 10: 
