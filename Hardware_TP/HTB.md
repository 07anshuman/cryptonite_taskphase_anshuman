

# Transistor and MOSFET Logic Gates:

[This](https://youtu.be/OWlD7gL9gS0?si=LKe85J5l2eLnGVyW) video perfectly explains the construction of AND, NAND, OR, NOR gates using transistors. However, let's see how they work mathematically.

## NAND Gate
![image](https://github.com/user-attachments/assets/e6c881c6-6660-499d-89f5-0d8c7f1dc626)


Here:

Input A goes to base of top transistor
Input B goes to base of bottom transistor
Emitter of bottom transistor is grounded
Collector of top transistor goes to output through a resistor

For A = 1, B = 1

    Both bases get voltage, both transistors conduct
    Current flows from V_CC to resistor to both transistors and then finally GND
    Output gets pulled low (i.e., logic 0)

For A = 1, B = 0

    Top transistor conducts, but bottom is off
    No current path so no pull-down
    Output stays high (logic 1)

For A = 0, B = 1

    Bottom transistor can conduct, but top one doesn’t conduct
    Output stays high

For A = 0, B = 0

    Both OFF; output stays high

## AND Gate
![image](https://github.com/user-attachments/assets/37cad595-da23-4919-8bf0-e88cb8bc0b66)

Here:
 Top transistor:

        Base : Input A
        Collector : +5V
        Emitter : connects to collector of bottom transistor

  Bottom transistor:

        Base : Input B
        Emitter : goes through a resistor to GND, and output is taken from here

Output: Between resistor and emitter of the bottom transistor

There's no pull-up resistor, so output only goes low when the transistor path is active.

For A = 0, B = 0

    Top transistor OFF so no current can flow
    Bottom transistor OFF too, also no conduction
    Output is connected to GND via pull-down resistor, but no current flow from +5V
    OUT = 0

For A = 0, B = 1

    Top transistor OFF, breaks the path
    Bottom transistor ON but no current from top
    OUT = 0

For A = 1, B = 0

    Top transistor ON
    Bottom transistor OFF, open circuit at the bottom
    OUT = 0

For A = 1, B = 1

    Top transistor ON
    Bottom transistor ON
    +5V to top transistor to bottom transistor to resistor to GND
    Current flows to voltage drop across resistor
    OUT = 1 
## OR Gate
![image](https://github.com/user-attachments/assets/72a82454-35af-4c51-a802-ea3ed6d69bfc)

Here:
  Two NPN transistors connected in parallel
  +5V supply
  Input A connected to the base of the left transistor 
  Input B connected to the base of the right transistor 
  Pull-down resistor connected between the output node and ground
  Output taken from the junction between the two transistor collectors

  ```
For A = 0V, B = 0V (Both inputs LOW)

  Q1: Base = 0V : OFF (no base current)
  Q2: Base = 0V : OFF (no base current)

Current Path: No current flows through either transistor. Output is pulled to ground through the pull-down resistor

For A = 0V, B = 5V (A LOW, B HIGH)

  Q1: Base = 0V : OFF
  Q2: Base = 5V : ON (conducting)

Current Path: +5V → Q2 (emitter to collector) → Output → Pull-down resistor → Ground
  Output: HIGH 

For A = 5V, B = 0V (A HIGH, B LOW)

  Q1: Base = 5V : ON (conducting)
  Q2: Base = 0V : OFF

Current Path: +5V to Q1 (emitter to collector) to Output to Pull-down resistor to GND
Output: HIGH 
```

## NOR Gate
![image](https://github.com/user-attachments/assets/60006c7b-ef43-4f89-9c7a-6be6c6a4a4c7)

Here:
  Two NPN transistors connected in parallel
  +5V supply at the top
  Pull-up resistor connected between +5V and the output node
  Input A connected to the base of the left transistor 
  Input B connected to the base of the right transistor 
  Output taken from the junction between the resistor and transistor collectors
  Ground connection at the bottom (transistor emitters)

```
For A = 0V, B = 0V (Both inputs LOW)

  Q1: Base = 0V : OFF 
  Q2: Base = 0V : OFF 

  Current Path: No current flows through either transistor to ground. Output is pulled HIGH through the pull-up resistor.
  Output: HIGH 
  
For A = 0V, B = 5V (A LOW, B HIGH)

  Q1: Base = 0V : OFF
  Q2: Base = 5V : ON (conducting)

  Current Path: +5V to Pull-up resistor to Output to Q2 (collector to emitter) to Ground. Q2 provides a path to ground, pulling output LOW.
  Output: LOW 

For A = 5V, B = 0V (A HIGH, B LOW)

  Q1: Base = 5V : ON (conducting)
  Q2: Base = 0V : OFF
  
  Current Path: +5V to Pull-up resistor to Output to Q1 (collector to emitter) to Ground. Q1 provides a path to ground, pulling output LOW.
  Output: LOW 

For A = 5V, B = 5V (Both inputs HIGH)

  Q1: Base = 5V : ON (conducting)
  Q2: Base = 5V : ON (conducting)

  Current Path: +5V to Pull-up resistor to Output to Both Q1 and Q2 (parallel paths to ground). Both transistors provide paths to ground, pulling output LOW.
  Output: LOW 
```

## Challenge 1: 
![img](https://github.com/user-attachments/assets/48166180-6d6d-4aac-95d6-066008705508)

### Flag: HTB{Unl0ck_7he_L0gic_Puzz1e}

Equation based on the gates shown in the picture: ```((A_ and B_)) or (not((C or D) and (E and F)))``` 
However, this equation is incorrect and doesn't give a valid flag. ```((A_ and B_)) or (not((C or D) or (E and F)))```
The NAND gate in the circuit is actually supposed to be a NOR gate. Then by running a script taking all inputs given in the CSV into the equation and taking the other output of the NOR gate to be a 1, we get the flag. 

## Challenge 2: 
![img2](https://github.com/user-attachments/assets/3726a3d5-d26a-4f88-8d49-e4e707db07a3)

Very simple. Just two AND gates ORd together. Produces a flag. 

### Flag: HTB{4_G00d_Cm05_3x4mpl3}

## Logic Gates using MOSFETS (CMOS LOGIC)
![NAND-Gate-and-NOR-Gate](https://github.com/user-attachments/assets/0e91c6c0-7a01-42cd-878e-910c9c2ed218)

PMOS (P-Channel MOSFETs) - Top mosfets (receiving the inverted inputs)
```
ON when gate = LOW (0V) - creates path from VDD to output
OFF when gate = HIGH (VDD) - blocks current flow
Acts as pull-up network (connects output to VDD)
```

NMOS (N-Channel MOSFETs) - Bottom mosfets
```
ON when gate = HIGH (VDD) - creates path from output to ground
OFF when gate = LOW (0V) - blocks current flow
Acts as pull-down network (connects output to ground)
```

Construction

2 PMOS in parallel (pull-up network)
2 NMOS in series (pull-down network)
When pull-up is ON, pull-down is OFF

For: A = 0, B = 0
PMOS Network:
```
PMOS_A: Gate = 0 : ON (VDD to output)
PMOS_B: Gate = 0 : ON (VDD to output)
Both PMOS ON in parallel : Strong pull-up to VDD
```
NMOS Network:
```
NMOS_A: Gate = 0 : OFF
NMOS_B: Gate = 0 : OFF
Series path broken : No pull-down
```
Output: HIGH (VDD)

For A = 0, B = 1
PMOS Network:
```
PMOS_A: Gate = 0 : ON
PMOS_B: Gate = 1 : OFF
One PMOS ON : Pull-up path exists
```
NMOS Network:
```
NMOS_A: Gate = 0 : OFF
NMOS_B: Gate = 1 : ON
Series broken by NMOS_A : No complete pull-down
```
Output: HIGH (VDD) 

For: A = 1, B = 0
PMOS Network:
```
PMOS_A: Gate = 1 : OFF
PMOS_B: Gate = 0 : ON
One PMOS ON : Pull-up path exists
```
NMOS Network:
```
NMOS_A: Gate = 1 : ON
NMOS_B: Gate = 0 : OFF
Series broken by NMOS_B : No complete pull-down
```
Output: HIGH (VDD) 

For A = 1, B = 1
PMOS Network:
```
PMOS_A: Gate = 1 : OFF
PMOS_B: Gate = 1 : OFF
No pull-up path
```
NMOS Network:
```
NMOS_A: Gate = 1 : ON
NMOS_B: Gate = 1 : ON
Complete series path : Strong pull-down to ground
```
Output: LOW (0V)

### CMOS NOR Gate

Construction

2 PMOS in series (pull-up network)
2 NMOS in parallel (pull-down network)
Opposite of NAND structure

For A = 0, B = 0
PMOS Network:
```
PMOS_A: Gate = 0 : ON
PMOS_B: Gate = 0 : ON
Complete series path : Strong pull-up to VDD

NMOS Network:
```
NMOS_A: Gate = 0 : OFF
NMOS_B: Gate = 0 : OFF
No pull-down path
```
Output: HIGH (VDD) 

For A = 0, B = 1
PMOS Network:
```
PMOS_A: Gate = 0 : ON
PMOS_B: Gate = 1 : OFF
Series broken by PMOS_B : No pull-up
```
NMOS Network:
```
NMOS_A: Gate = 0 : OFF
NMOS_B: Gate = 1 : ON
NMOS_B provides pull-down path
```
Output: LOW (0V) 

For A = 1, B = 0
PMOS Network:
```
PMOS_A: Gate = 1 : OFF
PMOS_B: Gate = 0 : ON
Series broken by PMOS_A : No pull-up

NMOS Network:
```
NMOS_A: Gate = 1 : ON
NMOS_B: Gate = 0 : OFF
NMOS_A provides pull-down path
```
Output: LOW (0V)

For A = 1, B = 1
PMOS Network:
```
PMOS_A: Gate = 1 : OFF
PMOS_B: Gate = 1 : OFF
No pull-up path
```
NMOS Network:
```
NMOS_A: Gate = 1 : ON
NMOS_B: Gate = 1 : ON
Both parallel paths ON : Strong pull-down
```
Output: LOW (0V) 

### NOT gate
![CMOSTechnologyCMOSInverter](https://github.com/user-attachments/assets/a5994d80-06af-4f1d-a8e6-7eeeafcacdde)

    PMOS transistor connected between VDD and output
    1 NMOS transistor connected between output and ground
    Both gates connected to input A
    Complementary operation: When one is ON, the other is OFF

For A = 0 (Input LOW)
PMOS Transistor:
```
Gate = 0V : ON (conducts)
Creates path: VDD to PMOS to Output
Pulls output HIGH
```
NMOS Transistor:
```
Gate = 0V : OFF (does not conduct)
No path from output to ground
No pull-down

Current Path: VDD to PMOS to Output (no current to ground)
```
Output: HIGH (VDD = 1) 

For A = 1 (Input HIGH)
PMOS Transistor:
```
Gate = VDD : OFF (does not conduct)
No path from VDD to output
No pull-up
```
NMOS Transistor:
```
Gate = VDD : ON (conducts)
Creates path: Output to NMOS to Ground
Pulls output LOW

Current Path: Output to NMOS to Ground (no current from VDD)
```
Output: LOW (0V = 0) 
