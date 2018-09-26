# VNVM
Tiny Von Neumann VM with custom assembly
### Registers:
 - r0-r9 - general purpose
 - sp - StackPointer
 - lr - LinkRegister (return address)
 - pc - ProcessCounter (current instruction)

### "Headers"
 - .stack (n) - size of a stack, allocated when program image is loaded
 - .entry (label) - entry point
 - .ascii "(some str)" - static const string
 - .number #some_n - static const integer
 - (label): - label
### Instruction
 - mov (reg), (reg/#some_n) - move from -> to
 - push { (reg/reg1, reg2/reg1 - reg2) } - push register/pair of registers/all registers in segment to stack
 - pop { (reg/reg1, reg2/reg1 - reg2) } - pop register/pair of registers/all registers in segment from stack
 - add (reg), (reg/$some_n) - addition (+=)
 - sub (reg), (reg/$some_n) - subtraction (-=)
 - inc (reg) - increment
 - dec (reg) - decrement
 - cmp (regA), (regB/#some_n) - compare, write value to r0: 0 - regA==regB, >0 - regA > regB, <0 - regA < regB
 - jeq (label) -  jump to label if r0 == 0
 - bl (label) - call label (write return address and jump)
 - printf - print zero-terminated string with address [r0]
 - printn - print number stored in r0
 - scann - read number to r0

### Additional comments
In case if pc == 0, the program is in terminal state, the execution is finished

## VNVM/VNAsm/VNDasm tools

### VNVM - Virtual Machine with pseudo-debugger

#### Starting VM
```
./VNVM #Start VM
./VNVM <binary file> #Load program image and start VM
```
#### VM Commands
 - run - begin the execution of loaded image of a program to the terminal state
 - load <path (.bin)> - load an image from binary file
 - step - one step of execution
 - regs - print register values
 - stack <n> - show last n values on stack
 - dump <path (.bin)> - save current VM image to binary file
 - exit - leave VM

### VNAsm - assembly translator

```
./VNAsm <assembly (.vn) path> #translate to binary file <assembly path>.bin
./VNAsm <assembly (.vn) path> <image (.bin) path> #Translate to bin image
```

### VNDasm - disassembly translator

```
./VNDasm <image (.bin) path> #Translate to assembly language <image path>.vn
./VNDasm <image (.bin) path> <assembly (.vn) path> #Translate to assembly
```
