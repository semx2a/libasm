# libasm

Get familiar with Assembly through utility function

## Instructions

- Your functions should not quit unexpectedly (`segmentation fault`, `bus error`, `double free`, etc) apart from undefined behaviors. If this happens, your project will be considered non functional and you will receive a 0 during the evaluation.
- Your `Makefile` must at least contain the rules `$(NAME)`, `all`, `clean`, `fclean` and `re`. And must recompile/relink only necessary files.
- We encourage you to create test programs for your project even though this work won’t have to be submitted and won’t be graded. It will give you a chance to easily test your work and your peers’ work. You will find those tests especially useful during your defence. Indeed, during defence, you are free to use your tests and/or the tests of the peer you are evaluating.
- You must write 64 bits ASM. Beware of the "calling convention".
- You can’t do inline ASM, you must use `.s` files.
- You must compile your assembly code with nasm.
- You must use the Intel syntax, not AT&T's.

/!\ -no-pie flag use is forbidden.

## Requirements

- The library must be called libasm.a.
- You must submit a main that will test your functions and that will compile with your library to show that it’s functional.
- You must rewrite the following functions in asm:
  - ft_strlen (man 3 strlen)
  - ft_strcpy (man 3 strcpy)
  - ft_strcmp (man 3 strcmp)
  - ft_write (man 2 write)
  - ft_read (man 2 read)
  - ft_strdup (man 3 strdup, you can call to malloc)
- You must check for errors during syscalls and properly set them when needed
- Your code must set the variable errno properly.
- For that, you are allowed to call the `extern ___error` or errno_location.

## Questions

- How to write test files for ASM functions?
- What are the 'calling conventions' for x86-64?

A calling convention is a set of rules for how functions should be called and how arguments should be passed between functions. The calling convention specifies things like:

- Which registers should be used to pass arguments.
- Which registers should be preserved across function calls.
- How the stack should be used to pass arguments.
- How the stack should be used to save the return address.
- How the stack should be used to save the frame pointer.

There are many different calling conventions, each with its own set of rules. Some of the most common calling conventions are:

- **CDECL**: The CDECL calling convention is used by the C programming language. It specifies that arguments should be passed on the stack from right to left, and that the caller is responsible for cleaning up the stack after the function returns.

- **STDCALL**: The STDCALL calling convention is used by the Windows operating system. It specifies that arguments should be passed on the stack from right to left, and that the callee is responsible for cleaning up the stack after the function returns.

- **FASTCALL**: The FASTCALL calling convention is used by some compilers to optimize function calls. It specifies that the first few arguments should be passed in registers, and that the callee is responsible for cleaning up the stack after the function returns.

- **SYSCALL**: The SYSCALL calling convention is used by the Linux operating system. It specifies that arguments should be passed in registers, and that the callee is responsible for cleaning up the stack after the function returns.

- What is a `.s` file?

`.s` files are source code files written in Assembly.
.S (capital S) stands for assembly code that must still pass through a pre-processor. That means it can have #include and #define among other macros. It may also be written as .sx.
.s (lowercase s) is pure assembly code that can be compiled into an object.
source: [What are .S files?](https://stackoverflow.com/questions/10285410/what-are-s-files)

- What is nasm and what does it do?

NASM (Netwide Assembler) is an assembler for the x86 architecture. It is used to translate assembly code into machine code that can be executed by the processor. NASM is a popular choice for writing low-level system software, such as operating systems and device drivers, because it produces highly optimized code that runs efficiently on the target hardware.

- What is the ASM Intel syntax?

The Intel syntax is the assembly language syntax used by Intel processors. It is characterized by the following features:

- Instructions are written in the form `operation destination, source`.
- Registers are specified by their names, such as `eax`, `ebx`, `ecx`, etc.
- Immediate values are specified by a dollar sign `$` followed by the value, such as `$5`.
- Memory addresses are specified by square brackets `[]`, such as `[eax]`, `[ebx]`, etc.
- The Intel syntax is used by the NASM assembler and is the most common syntax used in x86 assembly language programming.

## A little explaination about how processors work

### **Definitions**

#### Architecture

<p align=center>
  <img src=.img/busstructure.gif raw=true alt="Processor Architecture" width="600px" height="auto">
</p>

- **Processor**
  - **CPU** : Central Processing Unit
    - **ALU** : Arithmetic Logic Unit
    - **Control Unit** : to control the execution of instructions.
    - **Registers** : to store data temporarily.
      - **Instruction Register** : to store the current instruction being executed.
  - **Memory** : to store data and instructions.
    - **Caches** : to store frequently accessed data and instructions.
      - **L1 Cache** (Level 1 Cache)
      - **L2 Cache**
      - **L3 Cache**
      - ...
  - **Bus** : to transfer data between the processor and memory.
    - **Data Bus** : to transfer data between the processor and memory.
    - **Control Bus** : to control the execution of instructions.
    - **Address Bus** : to specify the location of data in memory.
  - **I/O** : to transfer data between the processor and external devices.

- **Processor**: The processor is the brain of the computer. It is responsible for executing instructions.
  - **CPU**: The CPU (Central Processing Unit) is the main component of the processor. It is responsible for executing instructions.
    - **ALU**: The ALU (Arithmetic Logic Unit) is a component of the processor that performs arithmetic and logical operations.
    - **Control Unit**: The control unit is a component of the processor that controls the execution of instructions.
    - **Registers**: Registers are small storage locations inside the processor. They are used to store data temporarily.
      - **Instruction Register**: The instruction register is a component of the processor that stores the current instruction being executed.
      - **Decoding Unit**: The decoding unit is a component of the processor that decodes instructions and sends them to the appropriate components for execution.
      - **Program Counter**: The program counter is a component of the processor that stores the address of the next instruction to  be executed.
      - **Accumulator**: The accumulator is a component of the processor that stores the result of arithmetic and logical operations.
      - **Address Register**: The address register is a component of the processor that stores the address of data in memory.
      - **Flag Register**: The flag register is a component of the processor that stores status information about the execution of instructions.
  - **Memory**: Memory is a storage system that holds data and instructions that the processor needs to execute.
    - **Cache**: Cache is a small, fast memory that is used to store frequently accessed data and instructions.
      - **L1 Cache**: L1 Cache is the first level of cache in a processor. It is small and fast, but also expensive.
      - **L2 Cache**: L2 Cache is the second level of cache in a processor. It is larger and slower than L1 cache.
    - **L3 Cache**: L3 Cache is the third level of cache in a processor. It is even larger and slower than L2 cache.
  - **Bus**: The bus is a communication system that allows the processor to transfer data to and from memory and other devices.
    - **Data Bus**: The data bus is a communication system that allows the processor to transfer data to and from memory and other devices.
    - **Address Bus**: The address bus is a communication system that allows the processor to specify the location of data in memory.
    - **Control Bus**: The control bus is a communication system that allows the processor to control the execution of instructions.
  - **IO**: IO (Input/Output) is the process of transferring data between the processor and external devices.

#### **Concepts**

- **Pipeline**: The**: The instruction set is the set of all instructions that a processor can execute.
- **Instruction**: An**: The instruction fetch is the process of fetching an instruction from memory.
- **Instruction Set**: The instruction set is the set of all instructions that a processor can execute.
- **Instruction Fetch**: The instruction fetch is the process of fetching an instruction from memory.

#### **Programming**

- **Assembly Language**: Assembly language is a low-level programming language that is specific to a particular processor.
- **Machine Language**: Machine language is the binary representation of the instructions that a processor executes.

## Assembly

Assembly is a low level language, which means its code is directly translated into machine code (binary code) by the processor. This makes it very fast and efficient, but also very difficult to read and write. Assembly language is specific to a particular processor, so code written in one assembly language will not work on another processor.

### **The microprocessor and its registers**

A processor is linked to memory through a bus. Registers store data that the processor needs to execute instructions. These registers follow this nomenclature:

| Register | Description |
|----------|-------------|
| General Registers | |
| `ax`     | Accumulator |
| `bx`     | Base        |
| `cx`     | Counter     |
| `dx`     | Data        |
| Segment Registers | |
| `cs`     | Code Segment |
| `ds`     | Data Segment |
| `es`     | Extra Segment |
| `ss`     | Stack Segment |
| Offset Registers | |
| `ip`     | Instruction Pointer |
| `sp`     | Stack Pointer |
| `si`     | Source Index|
| `di`     | Destination Index |
| `bp`     | Base Pointer |

- The *AX, BX, CX* and *DX* registers are general purpose registers. They can be used for any purpose, and mostly for arithmetic operations.
- The *IP* register is used to store the address of the next instruction to be executed.
- The *SI* and *DI* registers are used for string operations.
- The *CS, DS, SS* and *ES* registers are used to store segment addresses.
- The *SP* and *BP* registers are used to store stack addresses.

The *AX, BX, CX* and *DX* can be divided into two 8-bit registers, four 8-bit registers, or one 16-bit register. The 8-bit registers are named *AL, AH, BL, BH, CL, CH, DL* and *DH*. `L` stands for low byte and `H` stands for high byte.

Furthermore, in x86 32 bits architectures, the registers are extended to 32 bits. The 16-bit registers are extended to 32 bits by adding an `E` at the beginning of the register name. For example, `AX` becomes `EAX`, `BX` becomes `EBX`, and so on.

|EAX (32 bits)|
|--------|
| AX (16 bits) |
| AH (8 bits)|
| AL (8 bits) |

Another type of register is the flag register. The flag register is a special register that stores status information about the execution of instructions. The flag register is divided into several flags, each of which stores a different type of information. The most common flags are:

| Flag | Description |
|------|-------------|
| CF   | Carry Flag  |
| PF   | Parity Flag |
| AF   | Auxiliary Flag |
| ZF   | Zero Flag |
| SF   | Sign Flag |
| OF   | Overflow Flag |
| TF   | Trap Flag |
| IF   | Interrupt Flag |
| DF   | Direction Flag |
| OF   | Overflow Flag |

### **Syntax**

Assembly language has a very simple syntax. Each line of code consists of an instruction followed by one or more operands. The instruction tells the processor what to do, and the operands specify the data on which the instruction should operate. For example, the following code adds two numbers together:

```asm
mov eax, 5
add eax, 10
```

In this code, `mov` is the instruction that moves the value 5 into the `eax` register, and `add` is the instruction that adds the value 10 to the `eax` register.

Instructions can be formatted in different ways depending on the processor architecture. The two main formats are the Intel syntax and the AT&T syntax. The Intel syntax is used by Intel processors, while the AT&T syntax is used by AMD processors.

The instruction formats are similar, but the order of the operands is different. In the Intel syntax, the destination operand comes first, followed by the source operand. In the AT&T syntax, the source operand comes first, followed by the destination operand.

Here are some examples of instruction formats in Intel syntax:

- Unary instructions: `inc eax`
- Binary instructions: `add eax, ebx`
- Immediate instructions: `mov eax, 5`
- Ternary instructions: `lea eax, [ebx + ecx]`

The types of instruction formats are:

- **Register to Register**: `mov eax, ebx`
- **Immediate to Register**: `mov eax, 5`
- **Memory to Register**: `mov eax, [ebx]`
- **Register to Memory**: `mov [ebx], eax`
- **Immediate to Memory**: `mov [ebx], 5`

An assembly program can be divided into three sections:
  
- The data section,
- The bss (Block Started by Symbol) section, and
- The text section.

## Resources

- [Crash course in Assembly Language](https://medium.com/reverse-engineering-for-dummies/a-crash-course-in-assembly-language-695b07995b4d)
- [asmtest](https://github.com/briansteffens/asmtest)
- [Calling Convention in Computer Science](https://en.wikipedia.org/wiki/Calling_convention)
- [Qu'est-ce qu'un CPU ?](http://apotis3.free.fr/lectures/apo/siteEtudiants/qcmArchitectureOrdinateur/CPU.html)
- [Microprocessor and Memory Basics](http://www-mdp.eng.cam.ac.uk/web/library/enginfo/mdp_micro/lecture1/lecture1-2.html)
- [Composition d'un processeur](https://apcpedagogie.com/composition-dun-processeur/)
- [Le Langage Assembleur](https://lacl.u-pec.fr/tan/asm.pdf)
- [Introduction à l'assembleur](https://web.archive.org/web/20130324111007/https://www.commentcamarche.net/contents/asm/assembleur.php3)
- [Cours sur l'Assembleur](https://benoit-m.developpez.com/assembleur/tutoriel/index.php)