# Bootloaders: The Bridge Between Firmware and Kernel

> OS Development learning path — conceptual lesson. Study the ideas before attempting implementation.

## Learning objectives
- Explain why bootloaders exist.
- Identify common bootloader responsibilities.
- Understand the difference between a boot manager and a kernel.

## 1. Definition
A **bootloader** is a program that prepares an operating system kernel to run and then transfers control to it. A **boot manager** may present a menu when several operating systems or kernel choices are available. Some tools combine both roles.

## 2. Typical responsibilities
- Locate the kernel and related files.
- Load the kernel into memory.
- Load an initial RAM filesystem (where used).
- Pass command-line options and hardware information.
- Select a kernel or OS entry.
- Transfer execution to the kernel's entry point.

## 3. BIOS and UEFI contexts
Older BIOS boot commonly begins with a small boot sector, which may load additional stages. UEFI firmware can load an EFI application from a supported file system, so the boot path is different. Do not assume every bootloader uses a 512-byte sector.

## 4. Conceptual chain
```mermaid
flowchart LR
 FW["Firmware"] --> BM["Boot manager"]
 BM --> BL["Bootloader"]
 BL --> K["Kernel"]
 K --> US["User space"]
```

## 5. Common examples
GRUB is widely used in Linux systems. Windows Boot Manager is used in Windows boot environments. systemd-boot is another UEFI boot manager. Their configuration and capabilities differ.

## 6. Practical observation
If your computer already has a boot menu, observe its available entries without changing them. You can also read screenshots or documentation for GRUB's menu. Do not experiment by overwriting boot sectors on your main computer.

## Knowledge check
1. Does a bootloader normally provide the desktop interface? **No.**
2. Name two bootloader/boot-manager examples. **GRUB and Windows Boot Manager.**
3. What is an initramfs? **A temporary early-userspace filesystem image often used during Linux startup.**

## Key terms
Bootloader, boot manager, boot entry, kernel image, initramfs, boot configuration.

## Further reading
Read the GRUB manual and the UEFI boot manager documentation.
