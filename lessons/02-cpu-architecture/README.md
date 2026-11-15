# CPU Architecture and the Fetch–Decode–Execute Cycle

> OS Development learning path — conceptual lesson. Study the ideas before attempting implementation.

## Learning objectives
- Identify the major functional parts of a CPU.
- Describe the fetch–decode–execute cycle.
- Explain the roles of the program counter, instruction register, and general-purpose registers.

## 1. What is a CPU?
The **Central Processing Unit (CPU)** executes machine instructions. A modern CPU contains multiple cores, and each core contains execution units, registers, control logic, and access to one or more cache levels.

## 2. Main components
| Component | Responsibility |
|---|---|
| Control logic | Coordinates instruction execution and control signals |
| ALU | Performs integer arithmetic, comparisons, and bitwise logic |
| Registers | Hold operands, addresses, and intermediate results |
| Floating-point/vector units | Perform floating-point and data-parallel operations |
| Cache | Keeps copies of useful instructions and data near the core |

The traditional Control Unit (CU) and Arithmetic Logic Unit (ALU) model is a useful introduction. Real processors are more complex and may execute several instructions in overlapping stages.

## 3. Fetch–decode–execute
```mermaid
flowchart LR
 A["Fetch instruction"] --> B["Decode instruction"]
 B --> C["Execute operation"]
 C --> D["Write back result"]
 D --> A
```
1. **Fetch:** the CPU uses the program counter (PC) to locate the next instruction.
2. **Decode:** control logic interprets the instruction and identifies operands and operation.
3. **Execute:** an execution unit performs the operation, accesses memory, or changes control flow.
4. **Write back:** a result is placed in a register or memory as required. The PC is updated to the next instruction or branch target.

A branch, interrupt, cache miss, or pipeline dependency can alter the simple flow.

## 4. Example
For an instruction conceptually equivalent to `ADD R1, R2`, the CPU reads the values in registers R1 and R2, adds them, and stores the result in the destination register. Exact instruction syntax depends on the processor architecture.

## 5. Practical observation
Open Task Manager (Windows) or System Monitor and observe CPU utilization while a program runs. Compare idle activity with a CPU-intensive task. This shows workload, not the internal instruction cycle itself.

## Knowledge check
1. What does the PC identify? **The address of the next instruction (subject to control-flow changes).**
2. Which unit commonly performs integer addition? **An ALU or equivalent integer execution unit.**
3. Does every modern CPU execute exactly one instruction at a time? **No. Pipelining, superscalar execution, and multiple cores allow overlapping or parallel work.**

## Key terms
Core, register, ALU, program counter, instruction register, instruction set architecture (ISA), pipeline, cache.

## Further reading
Read an introductory computer architecture text and the programmer's manual for an ISA such as x86-64 or ARM.
