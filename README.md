# Stack-Machine-Emulator
----

An emulator for a hypothetical stack machine operating on 32 bit integers

## Description
----

**Significance**
Demostrates the structure and vast operational capabilities of even a simple two-stack interpreter.

### Prerequisites
----
Java JDK

### Installation
----
1. Download as .zip and unzip in desired directory.
1. Clone onto your local machine via GitHub Desktop or via the git address

## Usage
----

Example input and output are visible with intputInt.bin and outputInt.bin.
The integers in inputInt.bin are converted to 32-bit binary, hexadecimal, 6-bit interger and 16-bit integer

Interpreter reads a set of machine instructions from a binary file (in big-Endian format).
The file name is passed as a command-line argument and load those instructions into code memory.
Then program counter is initialized to 0 and the interpreter runs until a HALT instruction. 

For Java, args[0] = “myprog.bin”, so the command line is:
`> java Vm myprog.bin`

### Instructions
----
```
opcode | instruction | description
  0         HALT      -- stop execution
  1         PUSH v    -- push v (an integer constant) on the stack
  2         RVALUE l  -- push the contents of variable l
  3         LVALUE l  -- push the address of the variable l
  4         POP       -- throw away the top value on the stack
  5         STO       -- the rvalue on top of the stack is place in the lvalue below it and both are popped
  6         COPY      -- push a copy of the top value on the stack
  7         ADD       -- pop the top two values off the stack, add them, and push the result
  8         SUB       -- pop the top two values off the stack, subtract them, and push the result
  9         MPY       -- pop the top two values off the stack, multiply them, and push the result
  10        DIV       -- pop the top two values off the stack, divide them, and push the result
  11        MOD       -- pop the top two values off the stack, compute the modulus, and push the result
  12        NEG       -- pop the top value off the stack, negate it, and push the result
  13        NOT       -- pop the top value off the stack, invert all the bits, and push the result
  14        OR        -- pop the top two values off the stack, compute the logical OR, and push the result
  15        AND       -- pop the top two values off the stack, compute the logical AND, and push the result
  16        EQ        -- pop the top two values off the stack, compare them, and push a 1 if they are equal, and a 0 if they are not 
  17        NE        -- pop the top two values off the stack, compare them, and push a 1 if they are not equal, and a 0 if they are equal
  18        GT        -- pop the top two values off the stack, compare them, and push a 1 if the first operand is greater than the second, and a 0 if it is not 
  19        GE        -- pop the top two values off the stack, compare them, and push a 1 if the first operand is greater than or equal to the second, and a 0 if it is not 
  20        LT        -- pop the top two values off the stack, compare them, and push a 1 if the first operand is less than the second, and a 0 if it is not 
  21        LE        -- pop the top two values off the stack, compare them, and push a 1 if the first operand is less than or equal to the second, and a 0 if it is not 
  22        LABEL n   -- serves as the target of jumps to n; has no other effect
  23        GOTO n    -- the next instruction is taken from statement with label n
  24        GOFALSE n -- pop the top value; jump if it is zero
  25        GOTRUE n  -- pop the top value; jump if it is nonzero
  26        PRINT     -- pop the top value off the stack and display it as a base 10 integer
  27        READ      -- read a base 10 integer from the keyboard and push its value on the stack
  28        GOSUB l   -- push the current value of the program counter on the call stack and transfer control to the      statement with label l
  29        RET       -- pop the top value off the call stack and store it in the program counter
  30        ORB       -- pop the top two values off the stack, compute the bitwise OR, and push the result
  31        ANDB      -- pop the top two values off the stack, compute the bitwise AND, and push the result
  32        XORB      -- pop the top two values off the stack, compute the bitwise XOR, and push the result
  33        SHL       -- pop the top value off the stack, logical shift the bits left by 1 bit, and push the result
  34        SHR       -- pop the top value off the stack, logical shift the bits right by 1 bit, and push the result
  35        SAR       -- pop the top value off the stack, arithmetic shift the bits right by 1 bit, and push the result
```
For two operand instructions, the second operand is on top of the stack, and the first operand is one below it. 
All instructions are 32 bits: bits 32-22 are ignored, bits 21-16 hold the opcode, and bits 15-0 hold the operand. 
If there is no operand, bits 15-0 are filled with zeroes, andt ignored.  

Harvard memory model: two 256KB (65,536 32-bit) words for instructions and data.
The memory is be word-addressable: a 32-bit word is the smallest addressable memory location.
Having word addressability means that the location counter is incremented by 1 rather than by 4 at each step.

Two stacks:  A data stack, and a call stack.
A third memory segment of fixed size is used as the stack segment.
It is allocated the data segment, lets it grow downward from the highest memory location.
The dedicated call stack is used for the subprogram call/return mechanism, not the operand stack.

## Support
----
1. Open a request on this repository
1. Email me at nsean.robinson@gmail.com

## Authors
----
- **Nathan Robinson**

## License
----
This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details



