# BasicLinux

1. [Overview](#overview)

2. [Linux Distribution](#distribution)

3. [Kernel Architecture](#kernel)

4. [Filesystem](#filesystem)

5. [Linux tree structure of directory](#treedir)

6. [man (manual) commands](#man)

7. [Commands working with files](#filecmd)

8. [Linux users](#user)
<a name="overview"></a>
## 1. Overview

### Linux origin

Unix originated in the late 1960s at Bell Labs, created by Ken Thompson, Dennis Ritchie, and others. It began as a project to develop a multi-user, time-sharing operating system. Initially, it ran on a small computer called the PDP-7, but its simplicity and portability quickly gained attention. Unix's use of the C programming language, developed alongside it, made it versatile and easy to adapt to various hardware. It laid the groundwork for many modern operating systems.

### What is Linux

Linux is an open-source operating system modeled after Unix. It was created in 1991 by Linus Torvalds, a Finnish software engineer, as a personal project while he was a university student. His goal was to develop a free and flexible operating system that anyone could use, modify, and distribute. Linux quickly gained popularity because of its collaborative development model and adaptability, becoming the foundation for countless systems, from servers to smartphones (like Android).

### Linux and windows 

Linux and windows are two major operating systems that differs in several fundamental ways. While Linux being an oper-source OS that everyone can use, modify or distribute. In constrast, Windows is a close-source OS made by Microsoft that required paying for access.

With Linux having many distributions that users can modify from the source to suit the user's need based on their preference. On the other hand, Windows are only limited to the surface-level where user can customize themes and basic settings. 

<a name="distribution"></a>
## 2. Linux distribution and license 

Linux has a wide-range of distribution suitable for each preferences and user need. Some of the most well-known distributions include Ubuntu, Fedora, Debian, Arch Linux, RHEL, CentOS, and openSUSE.

### RHEL and CentOS Distribution

RHEL is a distribution developed by Red Hat. It is known for its stability, reliability and security. With its subscription-based system, providing users with extensive support, updates, and access to a wealth of documentation and resources. It is widely used in corporate environments, data centers, and on servers due to its robust performance and reliability.

CentOS was originally a free, community-supported clone of RHEL, offering the same features and capabilities without the cost of a subscription. It was popular among small businesses and developers who wanted a reliable enterprise-grade system but didn’t require Red Hat’s official support.

### Linux Licensing

Linux is licensed with the GNU General Public License (GPL), a document devised for the GNU project by the Free Software Foundation. The GPL allows anybody to redistribute, and even sell, a product covered by the GPL, as long as the recipient is allowed to rebuild an exact copy of the binary files from source.

### Development Cycle

Linux distributions usually go through these cycles:

**Upstream Development:** This phase involves improvements and bug fixes to the Linux kernel and associated software by the global open-source community.

**Integration:** Distribution maintainers select kernel versions, software, and tools to create a cohesive system.

**Testing:** Distributions undergo thorough testing to ensure stability, security, and performance.

**Release:** A stable version is officially released, which may include Long-Term Support (LTS) for extended maintenance.

**Updates and Patches:** The maintainers provide regular updates for bug fixes, security patches, and software upgrades during the distribution's lifecycle.

### Organization Contribution

**Linux Foundation:** A nonprofit organization that supports the growth of Linux and open-source projects. It provides resources for developers and hosts events like the Open Source Summit.

**GitLab:** A platform that facilitates collaboration on Linux-related projects. For example, Kali Linux uses GitLab to attract community contributions and streamline its development process.

**Ratomir Repository**: This site discusses how the open-source developer community contributes to Linux and UNIX systems, emphasizing collaborative coding and bug fixing.

<a name="kernel"></a>
## 3. Kernel Architecture

The Linux kernel is the core of the OS, responsible for managing system resource and communication between system hardware and software.

### The structure of Kernel

**Process Management:** Handles process creation, scheduling, and termination.

**Memory Management:** Manages RAM and virtual memory.

**Device Drivers:** Interfaces with hardware devices like disks, network cards, and peripherals.

**File System:** Manages data storage and retrieval using file systems like ext4 or xfs.

**Networking:** Provides support for network communication.

**System Call Interface:** Acts as the bridge between user applications and the kernel.

### Linux boot process

**BIOS/UEFI:** The system firmware initializes hardware and loads the bootloader.

**Bootloader:** Loads the kernel into memory and passes control to it.

**Kernel Initialization:** The kernel sets up low-level hardware, mounts the root file system, and starts the first process.

**INIT/Systemd Process:** Initializes user space and starts services based on the runlevel or target.

### The INIT system defines different levels for system operation

0: System halt.

1: Single-user mode (maintenance).

2: Multi-user mode without networking.

3: Full multi-user mode with networking.

4: Undefined, user-configurable.

5: Multi-user mode with a graphical interface.

6: System reboot.

<a name="filesystem"></a>
## 4. Filesystem

Filesystem is used to manage and organize stored data on the system, allowing users for quick access securely

### Filesystems supported by Linux

**Basic filesystem:** EXT2, EXT3, EXT4, XFS, Btrfs, JFS, NTFS,…

**Filesystem for Flash storage:** memory card,…

**Special purpose filesystem:** procfs, sysfs, tmpfs, squashfs, debugfs,…

Basic filesystems are versatile, general-purpose filesystems like EXT4 and XFS are widely used for desktops and servers.

Flash storage focused on wear-leveling and performance optimization, ideal for SSDs and embedded systems.

Special purposes serve specific roles like debugging (``debugfs``), temporary storage (``tmpfs``), or virtual interfaces (``procfs``).

### Linux File Hierarchy Structure

1. ``/``Root:

- The top level directory containing all files

2. ``/bin``:

- Contains essential binary programs (commands) like ``ls``,``cp``,``mv`` and  that are needed during boot and for basic system operation.

3. ``/boot``:

- Stores files needed for booting the system, such as the kernel and bootloader configurations.

4. ``/dev``:

- Contains device files that represent hardware devices

5. ``/etc``:

- Houses configuration files for the system and applications.
 
6. ``/home``

- Contains personal directories for users.

7. ``/lib``:

- Contains personal directories for users.

8. ``/media`` and ``/mnt``:

- Used for mounting external storage devices like USB drives or CDs.

9. ``/proc``:

- A virtual filesystem providing information about running processes and system hardware.

10. ``/usr``:

- Contains user-installed programs and libraries.

11. ``/var``:

- Stores variable files such as logs (``/var/log``), cached data, and spooled files

12. ``tmp``:

- Temporary files created by the system or users.

<a name="treedir"></a>
## 5. Linux tree structure of directory

The Linux directory tree is the hierarchical structure of directories and files in a Linux file system. It starts from the root directory (``/``) and branches out into various subdirectories, representing the organization of files and directories on the system.

Directories are containers used to organize files and other directories. Represented as ``d`` in permissions (like ``drwxr-xr-v``).

Sockets are special files used for interprocess communication (IPC). Allow processes to exchange data, often over a network or locally.

Other File Types:

- Regular Files: Most files in the system, like text or binary files.

- Symbolic Links: Shortcuts that point to other files or directories.

- Pipes: Temporary connections between commands, often used in scripting.

- Character/Block Devices: Represent hardware devices

### Path concept 

Paths help specify the location of a file or directory.

Starts from the root directory (``/``) then after that there is relative to the current working directory. Example: ``/home/user/doc``

### Basic directory commands

1. ``cd``: change directory

   ``cd home/user`` (Moves to "user" directory)

   ``cd ..`` (moves up to one directory)

   ``cd ~`` (moves to home directory)

2.  ``pwd`` (Print Working Directory): Displays your current location in the directory structure. Which outputs ``/home/user/doc`` while you are inside ``doc`` directory.

3.  ``ls`` (List Files): Lists the files and directories in your current location.

<a name="man"></a>
## 6. man (manual) commands

``man`` command in Linux is used to display the user manual of any command that we can run on the terminal. It provides a detailed view of the command.

Example: ``man ls`` displays the manual for the ``ls`` command.

To navigate through the list of command use arrow keys to scroll up and down, or use ``/`` to enter keyword. Once done press ``q`` to quit the man command.

<a name="filecmd"></a>
## 7. Commands working with files

### Reading files

``cat``: Displays the contents of a file

```sh 
cat file.txt
```

``less``: Lets you view file contents one screen at a time (better for large files).

```sh
less file.txt
```

``tail``: Displays the last few lines of a file (default: 10 lines).

```sh
tail file.txt
```

``head``: Displays the first few lines of a file (default: 10 lines).

```sh
head file.txt
```

### Writing file

``echo``: Write text to the file

```sh
echo "Hello, world" > file.txt
```

Use ``>>``to append instead of overwriting

``nano``: Text editors to create and edit files directly in the terminal.

```sh
nano file.txt
```

``touch``: Creates ane empty file

```sh
touch file.txt
```

### Copy and move files

``cp``: Copies files

```sh
cp source.txt destination.txt
```

``mv``: Moves or rename files

```sh
mv oldname.txt newname.txt
```

``rm``: Removes files

```sh
rm filename.txt
```

``grep``: Searches for a specific text pattern in a file.

```sh
grep "pattern" filename.txt
```

``file``: Identifies the file type.

```sh
file filename.txt
```

``stat``: Displays detailed information about a file

```sh
stat filename.txt
```

``ls -l``: Lists files with detailed information, including permissions.

<a name="user"></a>
## 8. Linux users

### User groups
Linux user groups are a way to manage permissions and access control for multiple users on a system. They allow users to share access to files, directories, and system resources based on group membership.

Primary Groups: Each user has one primary group, which is usually the same as their username. Files created by the user are associated with this group by default.

Secondary Groups: Users can belong to additional groups, granting them access to other resources or privileges.

### User types

**Root User:** The most powerful user with unrestricted access to the system. Can perform administrative tasks like installing software, managing users, and modifying system files. Should be used cautiously to avoid accidental system damage.

**Regular Users:** These are standard accounts created for everyday use. Have limited access to system resources but can use ``sudo `` to temporarily gain administrative privileges. Typically have their own home directories under ``/home``.

**System Users:** Created by the operating system during installation. Used for running system services and processes (e.g., ``www-data`` for web servers). Do not have login privileges and operate with restricted permissions.

**Service Accounts:** Similar to system users but specifically tied to applications or services. Used for managing tasks like database operations or web hosting.

### User rights and permissions

Linux uses a permission model to control access:

- Read (r): Allows viewing the contents of files or directories.

- Write (w): Enables modifying files or adding content to directories.

- Execute (x): Permits running executable files or accessing directories.

Permissions are assigned to three categories:

- Owner: The user who owns the file or directory.

- Group: A set of users who share access.

- Others: All other users on the system.







