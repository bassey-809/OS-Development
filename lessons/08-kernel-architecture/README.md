# Kernel Architecture: The Core of an Operating System

> OS Development learning path — conceptual lesson. Study the ideas before attempting implementation.

## Learning objectives
- Define the kernel.
- Compare monolithic and microkernel designs.
- Explain system calls and user/kernel mode.

## 1. What is the kernel?
The **kernel** is the privileged core of an operating system. It manages hardware resources and provides controlled services to applications. An OS includes more than the kernel: utilities, libraries, services, and user interfaces are also part of the complete system.

## 2. Common responsibilities
- Process and thread management
- Virtual memory and protection
- Device and I/O management
- File-system support
- Interrupt and exception handling
- Security and access control

## 3. User mode and kernel mode
Applications normally run with restricted privileges in **user mode**. The kernel runs with elevated privileges in **kernel mode**. When an application needs a protected service, it requests it through a **system call**. The CPU transitions to kernel mode through a controlled entry mechanism, the kernel validates the request, performs work, and returns a result.

## 4. Kernel architectures
| Design | Idea | Trade-off |
|---|---|---|
| Monolithic | Many core services run in kernel space | Performance can be strong; a kernel bug can affect the whole system |
| Microkernel | Keep a small core in kernel; move more services to user space | Better isolation/modularity potential; communication overhead and design complexity |
| Hybrid | Combines aspects of multiple designs | Practical compromise; categories can be debated |

Examples are simplified: real systems often mix design ideas.

## 5. Practical observation
On Linux, read `uname -a` to identify the running kernel. On Windows, use System Information to inspect OS and kernel-related version information. These commands observe a running system; they do not expose all internal architecture.

## Knowledge check
1. Is the kernel the entire operating system? **No.**
2. Why use system calls? **To request privileged OS services safely.**
3. What is a microkernel's design goal? **Keep the privileged kernel core small and move more services outside it.**

## Key terms
Kernel, user space, kernel space, privilege, system call, monolithic kernel, microkernel, hybrid kernel.

## Further reading
Study Linux kernel architecture and microkernel designs such as MINIX 3 or seL4.
