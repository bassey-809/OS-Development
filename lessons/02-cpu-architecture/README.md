# Lesson 02 — CPU Architecture and the Fetch–Decode–Execute Cycle

> OS Development learning path · Foundations before implementation

## Learning objectives

By the end of this lesson, you should be able to:
1. Explain what a CPU does.
2. Identify the control unit, ALU, registers, and cache.
3. Describe fetch, decode, execute, and write-back.
4. Explain the program counter, instruction register, and stack pointer.
5. Distinguish an ISA from a microarchitecture.
6. Explain why CPU state matters to an operating system.

## 1. What is a CPU?

The **Central Processing Unit (CPU)** executes machine instructions. A C++ program is compiled into machine code for a target instruction set architecture (ISA); the processor executes those instructions. The CPU fetches instructions and data through the memory system. It does not normally execute a program directly from an SSD.

- **CPU:** executes instructions.
- **RAM:** holds programs and data currently in use.
- **SSD/HDD:** stores programs and files persistently.

## 2. Main CPU components

### Control unit / control logic
The control unit coordinates instruction execution. It interprets instructions and directs the movement of data and control signals. It coordinates calculations; it does not itself perform every calculation.

### Arithmetic Logic Unit (ALU)
The ALU, or an equivalent integer execution unit, performs integer arithmetic and logical operations such as addition, subtraction, AND, OR, XOR, and comparisons.

### Registers
Registers are small, very fast storage locations within a CPU core. They hold operands, addresses, and intermediate results.

| Register | Purpose |
|---|---|
| Program Counter (PC) | Identifies the next instruction address according to the ISA. |
| Instruction Register (IR) | In a simplified CPU model, holds the instruction being processed. |
| General-purpose registers | Hold values, addresses, and temporary results. |
| Stack Pointer (SP) | Tracks the current stack position. |
| Status/flags register | Holds condition information such as zero or carry flags where supported. |

Do not confuse registers with RAM: registers are inside the processor core and are much smaller and faster.

### Cache
CPU cache keeps copies of useful instructions and data close to the processor, reducing average access time compared with fetching everything from RAM. L1 is commonly smallest and fastest; L2 is often larger; L3 is often larger still and may be shared across cores. Exact arrangements vary by CPU.

### Other execution units
Modern CPUs may also have floating-point units, vector/SIMD units, load/store units, and branch-handling hardware. The traditional CU-and-ALU model is useful for learning, but real CPUs are more complex.

## 3. Instruction Set Architecture (ISA)

An **ISA** is the software-visible contract of a processor. It defines supported instructions, registers, data sizes, addressing rules, and privileged operations. Examples include x86-64 and AArch64.

- **ISA:** what software can rely on.
- **Microarchitecture:** how a particular CPU internally implements the ISA.

Different CPU models can implement the same ISA using different internal designs.

## 4. Fetch–decode–execute

1. **Fetch:** the processor uses the PC to locate and fetch the next instruction.
2. **Decode:** control logic interprets the instruction and identifies its operation and operands.
3. **Execute:** an execution unit performs the operation, accesses memory, or changes control flow.
4. **Write back:** when required, the result is stored in a register or memory. The PC is updated to the next instruction or branch target.

This is a simplified teaching model. Modern processors overlap instruction stages through pipelining and may execute instructions out of order while preserving the required architectural behavior.

## 5. Example: addition

Consider the conceptual instruction `ADD R1, R2, R3`, meaning add R2 and R3 and place the result in R1. Exact syntax depends on the ISA.

If R2 contains 5 and R3 contains 3:
1. Fetch the ADD instruction.
2. Decode the operation and registers.
3. Read the operands (5 and 3).
4. An integer execution unit calculates 5 + 3.
5. Write 8 into R1.

## 6. Clock speed, cores, and threads

Clock frequency is measured in hertz. A 3 GHz clock represents three billion cycles per second, but clock speed alone does not determine performance. Microarchitecture, instructions completed per cycle, cache, memory delays, core count, power limits, and workload all matter.

A **core** is a hardware execution engine. Some cores support multiple hardware contexts through simultaneous multithreading (SMT). A **software thread** is an OS-schedulable sequence of execution. A **process** is an OS-managed program instance with its own resources and address-space context.

## 7. Why the OS cares about CPU architecture

### Privilege levels
Processors provide privilege mechanisms. The OS uses them to restrict ordinary applications and reserve sensitive operations for the kernel. Applications request protected services through controlled mechanisms such as system calls.

### Interrupts and exceptions
An **interrupt** is an event that transfers control to an interrupt handler. Hardware devices can raise interrupts to request attention. An **exception** is a synchronous event associated with instruction execution, such as an invalid operation or page fault. We will study these in Lesson 09.

### Context switching
When the OS switches between threads, it must preserve and restore the required CPU state. This can include general-purpose registers, the instruction pointer, stack pointer, and status information. This lets a thread resume from the correct point with its previous execution state.

## 8. Practical activities

### A. Observe CPU utilization
1. Open Windows Task Manager with Ctrl + Shift + Esc.
2. Select Performance → CPU.
3. Compare idle utilization with activity while running a demanding program.
4. Observe core and logical processor counts if displayed.

CPU utilization shows processor activity over time; it does not reveal the exact instructions being executed.

### B. Inspect your processor
Run this in PowerShell:

```powershell
Get-CimInstance Win32_Processor |
  Select-Object Name, NumberOfCores, NumberOfLogicalProcessors, MaxClockSpeed
```

### C. Connect C++ to machine instructions
Save and compile this program:

```cpp
#include <iostream>

int main() {
    int a = 5;
    int b = 3;
    int result = a + b;
    std::cout << result << '\\n';
    return 0;
}
```

With GCC or Clang, emit assembly using `g++ -S -O0 main.cpp -o main.s`. The output contains additional instructions for program setup and output; it will not necessarily resemble the conceptual ADD example.

## 9. Knowledge check

Try these before checking your notes:
1. What is the CPU's main job?
2. How is a register different from RAM?
3. What does the control unit do?
4. What kind of work does an ALU perform?
5. What does the PC identify?
6. What does an ISA define?
7. How does an ISA differ from a microarchitecture?
8. Why does a higher GHz rating not guarantee a faster CPU?
9. What is the difference between a core and a software thread?
10. Why does the OS save and restore CPU state during a context switch?

### Suggested answers
1. Execute machine instructions.
2. A register is a tiny, very fast storage location inside a CPU core; RAM is larger main memory.
3. Coordinates instruction execution and control signals.
4. Integer arithmetic and logical operations.
5. The next instruction address, as defined by the ISA.
6. The instructions and architectural behavior software can rely on.
7. ISA is the software-visible contract; microarchitecture is its internal implementation.
8. Performance also depends on work per cycle, architecture, cache, memory, cores, and workload.
9. A core is hardware; a software thread is a schedulable execution sequence.
10. So the thread can resume with the correct registers, instruction location, stack, and other required state.

## Key terms

CPU · CU · ALU · register · PC · IR · SP · ISA · microarchitecture · cache · core · hardware thread · interrupt · context switch

## Further reading

- [RISC-V specifications](https://riscv.org/technical/specifications/)
- [Intel 64 and IA-32 Software Developer Manuals](https://www.intel.com/content/www/us/en/developer/articles/technical/intel-sdm.html)
- [Arm architecture documentation](https://developer.arm.com/documentation)

**Next lesson:** Lesson 03 — Memory Architecture: connecting registers and cache to RAM, address spaces, and the memory hierarchy.
