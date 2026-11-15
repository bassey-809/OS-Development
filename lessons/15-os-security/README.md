# Operating System Security: Isolation, Permissions and Updates

> OS Development learning path — conceptual lesson. Study the ideas before attempting implementation.

## Learning objectives
- Identify core OS security mechanisms.
- Explain least privilege and process isolation.
- Recognize the role of updates and secure boot.

## 1. Security goals
An OS must protect confidentiality, integrity, and availability. It needs to prevent unauthorized access, limit damage from failures, and maintain reliable operation.

## 2. Core mechanisms
- **Authentication:** establishes who a user or service is.
- **Authorization:** determines what that identity may do.
- **Permissions:** control access to files and resources.
- **Process isolation:** limits one process's access to another's memory and resources.
- **Privilege separation:** keeps ordinary applications out of highly privileged execution.
- **Updates:** patch known vulnerabilities and improve reliability.
- **Secure Boot:** verifies parts of the startup chain according to trusted keys and policy.

## 3. Least privilege
Give each user, process, and service only the permissions required for its task. Running everything as administrator/root increases the impact of mistakes and compromise.

## 4. Defense in depth
No single control is sufficient. A secure system combines authentication, access control, isolation, encryption, updates, backups, monitoring, and secure configuration.

## 5. Practical security checklist
- Enable automatic security updates where appropriate.
- Use a standard account for everyday work.
- Use unique passwords and multi-factor authentication.
- Install software from trusted sources.
- Keep backups and test that they can be restored.
- Review application permissions.

## Knowledge check
1. What is least privilege? **Grant only the minimum permissions needed.**
2. Is authentication the same as authorization? **No; authentication verifies identity, authorization decides permitted actions.**
3. Does Secure Boot replace antivirus or patching? **No. It protects part of the boot chain and complements other controls.**

## Key terms
Confidentiality, integrity, availability, authentication, authorization, least privilege, isolation, Secure Boot, vulnerability, patch.

## Further reading
Read the security documentation for your OS and the NIST Cybersecurity Framework.
