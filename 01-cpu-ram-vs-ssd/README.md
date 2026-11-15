# CPU, RAM, and SSD: How a Computer Moves and Executes Data

## Learning objectives
By the end, you should be able to explain the jobs of the CPU, registers, cache, RAM, and SSD; trace how a program is loaded; and distinguish instruction execution from storage I/O.

## 1. The big picture

Think of a computer as a kitchen:
- **SSD:** the pantry; it keeps ingredients when the kitchen closes.
- **RAM:** the workbench; it holds ingredients currently being used.
- **CPU:** the chef; it carries out instructions.
- **CPU cache:** a small shelf beside the chef for frequently used ingredients.
- **Registers:** the tiny space in the chef's hands, holding values needed immediately.

The analogy is useful, but not exact.

## 2. What each component does

| Component | Main job | Keeps data without power? | Relative speed |
|---|---|---:|---|
| SSD | Long-term storage for programs and files | Yes | Much slower than RAM |
| RAM | Holds active program code and data | No | Fast |
| CPU cache | Keeps copies of recently/frequently used data close to CPU | No | Faster than RAM |
| Registers | Hold operands, addresses, and CPU state being used immediately | No | Extremely fast |
| CPU | Fetches, decodes, and executes instructions | Not a storage device | Executes instructions |

An SSD is persistent storage. RAM is volatile working memory: its contents are normally lost when power is removed.

## 3. How the parts communicate

A simplified path when an application starts:

```mermaid
flowchart LR
  SSD["SSD: program stored"] -->|"I/O request"| CTRL["Storage controller"]
  CTRL -->|"data transfer, often DMA"| RAM["RAM"]
  RAM --> CACHE["CPU cache"]
  CACHE --> REG["CPU registers"]
  REG --> CPU["CPU executes instructions"]
```

1. A program is stored as a file on the SSD.
2. The operating system asks its storage stack to read the required file data.
3. A storage controller communicates with the SSD. Data is commonly transferred into RAM using **DMA (Direct Memory Access)**, with the CPU coordinating the operation.
4. The OS maps the program's code and data into the process's virtual address space.
5. The CPU fetches instructions through the memory hierarchy. Needed data may be found in cache; otherwise, hardware fetches it from RAM.
6. The CPU uses registers while carrying out instructions.

Modern CPUs have multiple cache levels, memory controllers, virtual memory, and several I/O mechanisms, so this is a simplified model.

## 4. Can the CPU communicate with an SSD directly?

Saying “the CPU cannot read an SSD directly” is too absolute.

The CPU does not normally execute a program by treating SSD storage like ordinary RAM. It communicates with storage hardware through controllers and I/O mechanisms. The controller transfers data, commonly using DMA, into RAM. The CPU then works with that data through the memory system.

The distinction:
- **Instruction execution** normally uses instructions available through the CPU's memory system.
- **Storage I/O** is coordinated through device controllers, drivers, and the OS. The CPU can issue commands and inspect device status, but it does not normally fetch every program instruction straight from the SSD.

## 5. What happens when you open an application?

Imagine opening a text editor:
1. The application is stored on the SSD.
2. You click its icon. The OS receives the request.
3. The OS creates a process and arranges for its executable code and required data to be available in the process's virtual memory.
4. Pages are brought into physical RAM as needed. Some pages may be loaded only when first accessed.
5. The CPU executes the application's instructions. Cache helps avoid repeatedly waiting for RAM.
6. When the application opens a document, the OS requests file data from storage and makes it available to the process.

## 6. Why not use only an SSD?

SSDs are persistent and have large capacity, but their access latency is much higher than that of registers, cache, and RAM. The CPU needs instructions and data quickly. The memory hierarchy balances speed, capacity, and cost.

## 7. Knowledge check

1. Which component normally stores files when the computer is powered off? **SSD.**
2. Which component holds code and data a running process is actively using? **RAM (with working copies also held in caches and registers).**
3. What is CPU cache for? **Keeping useful copies of data/instructions close to the CPU to reduce average access time.**
4. Does the CPU copy every byte from an SSD into RAM itself? **Not necessarily; controllers commonly use DMA while the CPU and OS coordinate the transfer.**

## Key terms

- **Volatile memory:** memory that normally loses its contents when power is removed.
- **Persistent storage:** storage that retains data without power.
- **Storage controller:** hardware interface managing communication with a storage device.
- **DMA:** a mechanism allowing a device to transfer data to/from memory without the CPU handling every byte.
- **Cache:** small, fast memory holding copies of frequently or recently used information.
- **Virtual address:** an address used by a process and translated by hardware into a physical memory location.

## Further reading
- An operating-systems textbook chapter on I/O and memory management.
- CPU vendor documentation on cache hierarchy and memory.
- Linux kernel documentation on DMA and block I/O.
