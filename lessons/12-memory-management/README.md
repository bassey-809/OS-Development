# Memory Management: Allocation, Paging and Protection

> OS Development learning path — conceptual lesson. Study the ideas before attempting implementation.

## Learning objectives
- Explain why an OS manages memory.
- Describe paging and page tables.
- Understand protection and page faults.

## 1. The memory manager
The OS must allocate memory to processes, track which regions are in use, isolate processes, and reclaim memory when it is no longer needed.

## 2. Virtual memory
Each process generally sees a virtual address space. The MMU translates virtual addresses to physical addresses using page tables. This lets processes use separate address spaces even though they share physical RAM.

## 3. Paging
Virtual address spaces are divided into pages; physical memory is divided into frames. Page-table entries map pages to frames and include permissions and status information.

```mermaid
flowchart LR
 V["Virtual page"] --> PT["Page table / MMU"]
 PT --> F["Physical frame in RAM"]
```

A **page fault** occurs when the CPU cannot complete a memory access using the current translation. The OS may load a page from storage, create a zero-filled page, or reject an invalid access.

## 4. Allocation and protection
The OS tracks memory regions and access permissions such as read, write, and execute. Protection helps stop one process from freely reading or overwriting another process's memory. Programs also use concepts such as stack and heap, which are memory regions managed under OS and runtime rules.

## 5. Practical observation
Use Task Manager or System Monitor to inspect memory usage. Observe how usage changes as you open and close applications. Do not attempt to manually alter page tables or kernel memory.

## Knowledge check
1. What is a frame? **A fixed-size block of physical memory.**
2. What does a page table do? **Maps virtual pages to physical frames and stores related permissions/status.**
3. Can a page fault be handled successfully? **Yes; it is not automatically an error or crash.**

## Key terms
Virtual memory, page, frame, page table, MMU, page fault, stack, heap, memory protection.

## Further reading
Read your OS's virtual-memory documentation and a textbook chapter on paging.
