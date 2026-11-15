# OS Development — Structured Learning Path

This directory contains beginner-friendly conceptual lessons for understanding operating systems before moving into implementation. The existing boot-sector and Assembly exercises remain separate and unchanged.

## Recommended order

| Lesson | Topic | What you will learn |
|---|---|---|
| [02](02-cpu-architecture/README.md) | CPU architecture | CPU components and fetch–decode–execute |
| [03](03-memory-architecture/README.md) | Memory architecture | Registers, cache, RAM, virtual memory |
| [04](04-storage-systems/README.md) | Storage systems | HDDs, SSDs, interfaces, storage I/O |
| [05](05-bios-uefi-firmware/README.md) | BIOS, UEFI and firmware | How firmware initializes a computer |
| [06](06-boot-process/README.md) | Boot process | From power-on to login |
| [07](07-bootloaders-concepts/README.md) | Bootloaders | How firmware hands control to a kernel |
| [08](08-kernel-architecture/README.md) | Kernel architecture | Kernel responsibilities and design styles |
| [09](09-interrupts-io/README.md) | Interrupts and I/O | Events, handlers, polling, DMA |
| [10](10-processes-threads/README.md) | Processes and threads | Running programs and concurrent execution |
| [11](11-cpu-scheduling/README.md) | CPU scheduling | How the OS chooses what runs next |
| [12](12-memory-management/README.md) | Memory management | Paging, virtual memory, protection |
| [13](13-file-systems/README.md) | File systems | Files, directories, metadata, storage blocks |
| [14](14-device-drivers/README.md) | Device drivers | How the OS communicates with hardware |
| [15](15-os-security/README.md) | OS security | Isolation, permissions, least privilege |
| [16](16-virtualization/README.md) | Virtualization | VMs, hypervisors, and containers |

## How to study each lesson

1. Read the learning objectives first.
2. Work through the explanation and redraw the diagrams in your own words.
3. Try the practical observation using your existing computer; do not change firmware, partitions, or boot settings unless a lesson explicitly guides you and you understand the risks.
4. Answer the knowledge-check questions without looking.
5. Explain the topic aloud as if teaching a classmate.

## Existing repository material

- [CPU, RAM and SSD](../01-cpu-ram-vs-ssd/README.md) introduces the memory and storage path.
- [First boot sector](../02-first-boot-sector-code/README.md) is a hands-on implementation exercise.
- [Operating systems notes](../operating-systems-notes.md) contains broader lecture notes and overlaps with several concepts in this learning path.

The structured lessons complement the lecture notes; they do not replace them. Lesson numbering starts at 02 because the existing introductory material is already in the repository.
