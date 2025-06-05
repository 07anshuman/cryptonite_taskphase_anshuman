

# Transistor Logic Gates:

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

## Challenge 2: 
![img2](https://github.com/user-attachments/assets/3726a3d5-d26a-4f88-8d49-e4e707db07a3)

### Flag: HTB{4_G00d_Cm05_3x4mpl3}

