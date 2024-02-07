---
Author:
  - Xinyang YU
Author Profile:
  - https://linkedin.com/in/xinyang-yu
tags:
  - OS
Creation Date: 2024-02-07, 16:20
Last Date: 2024-02-07T17:52:11+08:00
References: 
draft: 
description: FUSE (Filesystem in Userspace) lets programs manage filesystems without kernel privileges, enabling custom cloud storage mounts and powering tools like Rclone. It achieves this by acting as a bridge between user-space filesystem implementations and the kernel, forwarding requests and returning results.
---
## Abstract
---
- Stands for [[File System|Filesystem]] in [[User Space|USErspace]]
- A software interface that enables program in the [[User Space]] to create and manage filesystems without requiring [[Privilege Level#Kernel Mode]]

  </br>
  
- Traditionally, filesystem operations like reading and writing files, creating directories, and managing file metadata are handled by the [[Kernel]]. However, FUSE allows these operations to be implemented in user space by user programs, outside the kernel

>[!success] Flexibility 
> Developer can create their own filesystem with customisations without the need to modify the Kernel
> 
> This is commonly used for mounted Cloud Storage. The files dropped into the mounted Cloud Storage is stored by making network calls instead of IO. We need to have a set of logic for this. FUSE allows us to introduce this new set of logic without modifying the kernel

>[!example] Powers Popular Tools
>- [Rclone](https://rclone.org/) - mount Cloud Storages as a local file system 
### FUSE Mechanism
![[fuse_architecture.png|400]]

- FUSE works by providing a **FUSE Kernel Module** that acts as a **bridge** between the filesystem requests made by **File System User** and the actual filesystem implementation running in user space (**FUSE Driver**)

  </br>
  
- When an application makes a filesystem request, the request is forwarded to the FUSE kernel module, which then passes it to the user-space filesystem implementation. Once the operation is completed in user space, the result is sent back to the kernel module, which returns the result to the application


## References
---
- [CS170 Lab 6: File System](https://sites.cs.ucsb.edu/~trinabh/classes/w19/labs/lab6.html)