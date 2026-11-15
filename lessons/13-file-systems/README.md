# File Systems: How Operating Systems Organize Data

> OS Development learning path — conceptual lesson. Study the ideas before attempting implementation.

## Learning objectives
- Explain the purpose of a file system.
- Distinguish files, directories, partitions, and volumes.
- Compare common file systems at a high level.

## 1. What is a file system?
A **file system** defines how data is named, organized, stored, retrieved, and protected on a storage volume. It maintains metadata such as file names, sizes, timestamps, permissions, and the locations of data blocks.

## 2. Basic concepts
- **File:** a named collection of data.
- **Directory:** an organizational structure that maps names to file-system objects.
- **Partition:** a defined region of a storage device.
- **Volume:** a storage area presented for use, often containing a file system.
- **Metadata:** information describing a file or directory.

## 3. Examples
| File system | Common context |
|---|---|
| FAT32 | Removable media and broad compatibility; has file-size limitations |
| exFAT | Removable flash storage and large files |
| NTFS | Common Windows system volumes |
| ext4 | Common Linux file system |
| APFS | Apple's modern file system for its platforms |

This is a broad overview; feature support depends on OS and configuration.

## 4. What happens when you save a file?
1. An application asks the OS to create or update a file.
2. The OS checks permissions and passes the request to the file-system implementation.
3. The file system updates metadata and allocates storage blocks as needed.
4. The storage stack sends writes to the device.
5. Caching and write-back policies mean data may not reach physical media at the exact instant the application calls save; applications and OSes use flush/sync mechanisms when durability matters.

## 5. Practical observation
Create a folder and a small text file, rename it, inspect its properties, then delete it. Notice that deleting a file usually removes its directory reference/metadata; it does not necessarily erase every underlying data byte immediately.

## Knowledge check
1. What does a file system manage? **Files, directories, metadata, and storage allocation.**
2. Is a partition the same thing as a file? **No.**
3. Does deleting a file guarantee secure erasure? **No.**

## Key terms
File, directory, metadata, partition, volume, block, journaling, permissions, mount.

## Further reading
Read the official documentation for NTFS, ext4, APFS, or exFAT.
