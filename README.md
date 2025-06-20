# BasicLinux

1. [Overview](#overview)

2. [Linux Distribution](#distribution)

3. [Kernel Architecture](#kernel)

4. [Filesystem](#filesystem)

5. [Linux tree structure of directory](#treedir)

6. [man (manual) commands](#man)

7. [Commands working with files](#filecmd)

8. [Linux users](#user)

9. [Package Manager](#package)

10. [Processes](#process)

11. [Virtual RAM and SWAP](#RAM)

12. [Network configuration](#Network)

13. [Command types](#commands)

14. [Sudo and su](#sudo)

15. [File commands](#filecmd)

16. [Environment Variables](#var)

17. [Bash Shell](#bash)

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

### Adding new disk on VMware

1. Add a new disk

Go to storage setting of the virtual machine manager

In the options below press new "hard disk"

Press on "New" to create a new disk

VDI disk type is recommended for OracleVM, choose everything default with disk size set to 2GB

Finish setup and Power up the VM

2. Identify the new disk

After booting, run:

```sh
lsblk
```

You’ll see something like:

```sh
sda      20G
└─sda1   20G
sdb       2G  # <-- This is the new disk
```

3. Partition the disk 

Run:

```sh
sudo fdisk /dev/sdb
```

Inside fdisk:

```sh
n   # new partition
p   # primary
1   # partition number
Enter  # default first sector
Enter  # default last sector
w   # write and exit
```

Verify partition:

```sh
lsblk
```

You’ll now see ``/dev/sdb1``.

Format the Partition with a Filesystem:

```sh
sudo mkfs.ext4 /dev/sdb1
```

5. Mount the Partition

Create a mount point:

```sh
sudo mkdir /mnt/data_disk
```

Mount it:

```sh
sudo mount /dev/sdb1 /mnt/data_disk
```

Verify mount:

```sh
df -h | grep /mnt/data_disk
```

7. Make the Mount Permanent with /etc/fstab
Get UUID of the partition:

```sh
sudo blkid /dev/sdb1
```

Example output: ``/dev/sdb1: UUID="abcd-1234" TYPE="ext4"``

Edit fstab:

```sh
sudo nano /etc/fstab
```

Add this line:

```sh
UUID=abcd-1234  /mnt/data_disk  ext4  defaults  0 2
```

Test:

```sh
sudo umount /mnt/data_disk
sudo mount -a
df -h | grep /mnt/data_disk
```

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

### Symbolic links of linux

Field	Meaning

``lrwxrwxrwx  1 root root   16 Jan 10 11:56 99-environment.conf -> /etc/environment``

``l``	First character: indicates it's a symbolic link (l = link)

``rwxrwxrwx``	Permissions: link has full permissions (not meaningful for symlinks)

``1``	Link count (for symlinks, usually 1)

``root``	Owner of the file (root user)

``root``	Group owner (root group)

``16``	Size of the symlink target string (length of /etc/environment)

``Jan 10 11:56``	Last modification time of the link (not the target file)

``99-environment.conf``	The name of the symlink

``-> /etc/environment``	The file it points to

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

### File permission example

``drwxrwxr-x  12 root   root  4096 Apr 10 07:27 tmp``

``d``: the directory

First three digits ``rwx``: Permission of the owner 

Second three digits ``rxw``: Permission of the group 

Last three digits ``r-x``: Permission of other users 

The first ``root``: The owner name 

The second ``root``: The group name

``4096``: The size of the directory

``Apr 10 07:27``: The last modified timestamp when a directory contents were changed

``tmp``: Directory name

### Giving permission for users

``chown (user) (directory/file)`` giving the ownership of the directory/file to an user

``chmod (u/g/o/a)(+/-/=)(r/w/x) filename`` 

``(u/g/o/a)``: Giving permission to (owner/group/other/all)

``(+/-/=)``: Add, remove or overwrite the last permission

``(r/w/x)``: Giving permission to read/write/execute

### Permission 777

The permissions can be represented in three groups, with each group represented by 3 numbers:

Owner: First number

Group: Middle number

Others: Last number

When a file or directory has 777 permissions means the user/group/others has full access

In numerical terms: 

4 = Read (`r`)

2 = Write (`w`)

1 = Execute (`x`)

0 = no permission

4 + 2 + 1 = 7 (full access)

4 + 2 = 6 (Read and write only)

4 + 1 = 5 (Read and execute only)

2 + 1 = 3 (Write and execute only)

Giving permission is more simple with this command:

``chmod 777 filename``

By default, Linux assigns the permission  (full read, write, and execute access) to the ``/tmp`` directory.

``/tmp``is used to store temporary files by all users and applications. Since it's globally accessible,  ensures users can create, modify, and delete temporary files as needed.

The decision to represent permissions using numbers in Linux was driven by the need for simplicity, efficiency, and universality.

### Advanced permissions

**SUID (Set User ID):**

Allows a program to run with the permissions of the file owner, rather than the user executing it. When the SUID bit is set on an executable file, it runs with the privileges of the file's owner. Represented by an ``S`` in the owner's execute position (e.g., ``-rwSr--xr-x``).

Example:

```sh
chmod u+s filename
```

**SGID (Set Group ID):**

Similar to SUID, it allows a program or directory to run with the permissions of the group owner.

Example:

```sh
chmod g+s filename
```

**Sticky Bit:**

Restricts file deletion in a directory to the file's owner, even if others have write permissions. When the sticky bit is set on a directory, users can only delete their own files, even if they have write access to the directory. Represented by a ``T`` in the others' execute position (e.g., ``drwxrwxrwT``).

Example:

```sh
chmod +t directoryname
```

**Umask:**

Sets default permissions for newly created files and directories by masking certain bits. The ``umask`` value subtracts permissions from the default settings. Example: Files being 666 (read and write to all)

### Change user password

Access ``/etc/shadow`` using ``sudo vim`` command and change the user password

However, editing passwords directly in ``/etc/shadow`` is not recommended, as it can compromise security.

The /etc/shadow file stores encrypted passwords and looks like this:

```sh
username:$id$salt$hashedpassword:lastchange:min:max:warn:inactive:expire:
```
Example: ``jason:$6$GsQ1UXK3$OqtccFXxK3Ujc5HDV2rD7xC9WdjZmpfknwPq69zRNTzqkjXSGf4vU8YgydJvmuDRT27Ir.LSXYwNFpm2g2vdX/:19430:0:99999:7:::``

``$6$`` = SHA-512

The second field is the hashed password

1. Generate a new hashed password

Use the openssl or mkpasswd command:

```sh
openssl passwd -6
```

It will ask for a password, and return something like:

```sh
$6$random_salt$encrypted_hash_here
```

Save that output.

2. Open /etc/shadow safely

```sh
sudo cp /etc/shadow /etc/shadow.bak
sudo nano /etc/shadow
```

Find the line for the user, for example: ``jason:$6$oldhashhere:...``

Replace the entire password hash (2nd field) with the one you generated.

3. Save and exit
In nano: Ctrl + O to save, Ctrl + X to exit.

4. Test the password
Try logging in as the user (or su - username) and use the new password.

<a name="package"></a>
## 9. Package Managers

**dpkg (Debian Package Manager):**

dpkg is a core tool for managing ``.deb`` packages. It works directly with package files. You can use it to install, remove, and query ``.deb`` packages. dpkg does not automatically resolve or install dependencies. If a package requires other packages, you need to manually install them.

``.deb`` packages are software packages used in Debian-based Linux distributions, including Ubuntu. They are essentially archives containing files and metadata required to install software.

Example:

```sh
dpkg -i package.deb  # Install a .deb package
dpkg -r package_name  # Remove a package
```

**apt (Advanced Package Tool):**

apt is a front-end for dpkg that simplifies package management. apt automatically resolves and installs dependencies, making it more user-friendly. apt can fetch packages from remote repositories, whereas dpkg only works with local files. 

Example:

```sh
apt install package_name  # Install a package and its dependencies
apt remove package_name  # Remove a package
apt update  # Update package lists
apt upgrade  # Upgrade installed packages
```

dpkg is a powerful tool for manual package management, while apt provides a more streamlined and automated experience by handling dependencies and accessing repositories.

**apt-get:**

A lower-level tool designed for scripts and advanced users. Offers more granular control and additional options.

``apt`` is simpler and more intuitive for everyday users, while ``apt-get`` is better suited for scripting and automation.

``apt`` provides a more polished and readable output compared to ``apt-get``.

<a name="process"></a>
## 10. Processes

A process in Linux is essentially a running instance of a program. Whenever you execute a command, open an application, or perform a task in Linux, it creates a process. Processes are fundamental to how Linux and other operating systems function.

### Foreground processes

These run interactively, meaning they require user input and block the terminal until they're complete.

### Background processes

These run in the background, allowing you to continue using the terminal.

### Daemon processes

These are background processes that run independently of the terminal and often handle system tasks or services.

### Zombie processes

These are processes that have finished executing but still occupy an entry in the process table. They are harmless but indicate that the parent process didn't properly clean them up.

### Orphan Processes

These are processes whose parent process has been terminated. They are adopted by the init process (PID 1).

### Key commands to manage processes

``ps`` lists only processes associated with the current terminal session.

``kill`` Sends a signal (like terminate) to a process using its PID.

``killall`` Kills all processes by name.

``pkill`` Kills processes by name but adds more advanced matching capabilities.

``fg`` Resumes a process in the foreground.

``bg`` Resumes a paused process in the background.

``sleep`` pause the execution of a script or a command for a specified amount of time.

``top`` A real-time process manager that shows resource usage (CPU, memory, etc.) for each process.

``htop`` An enhanced version of ``top`` with a more user-friendly interface and better features. Provides color-coded stats and supports mouse interactions.

``lsof`` Display information about files that are currently open by processes.

### Foreground and background

<a name="RAM"></a>
## 11. Virtual RAM and SWAP

Virtual RAM, or virtual memory, is a system that allows Linux to use both physical RAM and secondary storage (like a hard disk or SSD) to create an illusion of having more memory than physically available.

When a program needs memory, the kernel decides whether to keep it in RAM or move it to the disk (swap space). This technique enables running large applications even with limited physical RAM.

SWAP is a designated area on the disk used as an extension of physical RAM. When the system runs out of RAM, it moves inactive pages to the SWAP space, freeing up RAM for active processes. 

SWAP can be set up as a partition or a file. While SWAP helps prevent system crashes due to memory exhaustion, it is slower than RAM, so excessive reliance on SWAP can lead to performance issues.

In certain situations, they can be useful due to their flexibilty enhancing system stability while running heavy tasks. However, excessive reliance on SWAP can degrade performance because disk access is much slower than RAM access. 

In modern systems with ample RAM, SWAP might only be lightly used or even unnecessary for general tasks, only for servers and datasets where it really useful.

<a name="Network"></a>
## 12. Network configuration

Configuring network settings on Ubuntu can be done using various methods, depending on your needs.

**Netplan:** Ubuntu uses Netplan for network configuration. It allows you to define settings in YAML files. For example, you can set up static IPs or configure DHCP.

**Command Line:** You can use commands like ``ip a`` to view network interfaces or ``ipconfig`` to configure them. For more advanced tasks, commands like ``sude route add`` can set up gateways.

### Setting a static network

Open the Netplan configuration file:

```sh
sudo nano /etc/netplan/01-netcfg.yaml
```

Add the configuration into the file:

```sh
network:
  version: 2
  renderer: networkd
  ethernets:
    enp0s3:
      dhcp4: no
      addresses:
        - 192.168.1.100/24
      gateway4: 192.168.1.1
      nameservers:
        addresses:
          - 8.8.8.8
          - 8.8.4.4

```

Apply the configuration:

```sh
sudo netplan apply
```

### Setting a dynamic network

Change the dhcp4 to ``yes`` inside the yaml file

Then use the apply command again

### Add/Remove IP address

```sh 
sudo ip addr add/del 192.168.1.101/24 dev enp0s3
```

### VMware network setup

Add a Network card:

+ Power off the VM.

+ Open VMware Workstation or VMware Player.

+ Right-click the VM > Settings.

+ Click Add… > Select Network Adapter > Next.

+ Choose Custom (to use a specific VMnet) or Bridged/NAT.

+ Finish and Power On the VM.

+ Run ip link or ip a inside the VM to find the new interface (e.g., ens33, eth1, etc.).

Use command ``ip link`` to find any interface that is currently down

Assuming the interface is ``enp0s8``, manually test the interface:

```sh
sudo ip link set enp0s8 up
```

It should now say ``BROADCAST,MULTICAST,UP,LOWER_UP`` — indicating it's active.

To test assigning a static IP without a gateway, run:

```sh
sudo ip addr add 192.168.100.50/24 dev enp0s8
```

```sh
ip a show enp0s8
```
Open static IP YAML file:

```sh
sudo nano /etc/netplan/02-static-ip.yaml
```

Fix the configure content:

```sh
network:
  version: 2
  ethernets:
    enp0s8:
      dhcp4: no
      addresses:
        - 192.168.100.50/24
      nameservers:
        addresses: [8.8.8.8]
```

Apply the configuration: ``sudo netplan apply``

Verify the configuration: 

```sh
ip a show enp0s8 
ip r
```
<a name="commands"></a>
## 13. Command types

The ``type`` command is used to identify and distinguish between different kinds of commands.

### Types of commands

**Built-in Commands:** Commands that are part of the shell itself (``cd``, ``echo``). These do not have an external executable file,  the shell processes them directly. Output example: ``cd is a shell builtin``

**External Commands:** These are executable programs stored as files on the filesystem (e.g., ``/bin/ls``, ``/usr/bin/grep``). Output example: ``mv is /usr/bin/mv``

**Aliases:** Shortcuts or custom names for commands that users define (``alias ll='ls -la'``). Output example: ``ls is aliased to `ls --color=auto'``

**Functions:** User-defined functions within the shell script. Output example: ``myFunction is a funciton``

**Keyword:** Special words that have specific meaning in the shell. Output example: ``if is a shell keyword``

<a name="sudo"></a>
## 14. Sudo and su

The ``sudo`` group in Linux is used to grant specific users administrative privileges without requiring them to log in as the root user. Members of the sudo group can execute commands with elevated privileges by preceding them with the sudo command.

Membership in this group is a safer alternative to using the root account directly, as it requires users to authenticate with their own password and records their actions.

``sudo`` commands stands for "superuser do." It allows a permitted user to execute a command as another user (default is root) without needing the root password.

sudo requires the user to authenticate using their own password instead of the target user's password.

Run almost any commands with sudo: 

```sh
sudo <command>
```

### Add an sudo rights to an user

``cat /etc/group | grep sudo`` checks current users in the group

``sudo usermod -aG sudo username`` adds the user to the group

``groups username`` checks the groups that user currently in

### su command

Purpose: Stands for "substitute user" or "switch user." It allows you to switch to another user account, most commonly the root user.

How It Works: When using su, you will be prompted to enter the password of the target user. This means if you're switching to root, you need to know the root password.

Switch to another user account: ``su <username>``

Execute a command as another user: ``su -c "command" <username>``

<a name="filecmd"></a>
## 15. File commands

### vim command

Vim is a highly powerful and customizable text editor in Linux.

Vim has 3 modes:

**Normal mode:** Vim is a highly powerful and customizable text editor in Linux.

**Insert mode:** Allows text entry (press i to enter Insert mode).

**Command mode:** Used to execute commands (press : to enter Command mode).

Open a file:

```sh
vim filename
```

Open multiple file:

```sh
vim file1 file2
```

Basic functions inside vim:

``:w`` to save change

``:q`` to quit vim

``:wq`` to save and quit

``:q!`` quit without save

Navigation:

``h / l / k / j`` to move up/right/left/down

``0`` jump to the start of a line

``$`` jump to the end of a line

``gg`` move to the beginning of a file

``G`` move to the end of a file

Text editing:

``x`` deletes a character

``u`` undo change

``Crtl + r`` redo change

``yy`` copy a line

``p`` paste

### cat and echo 

``cat`` Used to display the contents of files, concatenate files, or create new ones.

Basic Syntax: ``cat <file>``

Combine text files: ``cat file1.txt file2.txt > combined.txt``

Create a new file: ``cat newfile.txt``

Display the text files with number of lines: ``cat -n <file>``


``echo `` Used to print text or the value of variables to the terminal.

Basic Syntax: ``echo <text>``

Use variables: ``MY_VAR="Learning Linux" `` and ``echo $MY_VAR``

Append text into a file ``echo <text> >> file.txt``

Read permission for a directory allows a user to list the contents of the directory. However, it doesn't necessarily mean the user can access the files within the directory or view their contents additional permissions are required for that.

If a user has read (r) permission for a directory, they can use commands like ``ls`` to view the names of files and subdirectories inside the directory.

To open or interact with files inside a directory, the user also needs execute (x) permission for the directory.

Example: If a directory has read but not execute permission, the user can list the file names but cannot access their contents or navigate into subdirectories.

### Text processing command-line tools

``awk``: Pattern scanning and processing language

Purpose: Extracts and processes text based on patterns and fields (columns).

Typical Use: Parsing structured data like CSVs or log files.

Example:
```sh
awk '{print $1}' file.txt  # Prints the first field (column) of each line.
awk -F, '{print $2}' file.csv  # Uses a comma as a delimiter and prints the second column.
```

``cut``: Extracts specific sections of text based on delimiters or character positions.

urpose: Extracts specific columns or fields by character or delimiter.

Typical Use: Quick field extraction from simple delimited files.

Example:
```sh
cut -d',' -f1 file.csv  # Extracts the first field (column) using a comma delimiter.
cut -c1-5 file.txt  # Extracts characters 1 through 5 from each line.
```

``sed``: Stream editor

Purpose: Performs basic text transformations on an input stream (like substitution, deletion, insertion).

Typical Use: Search and replace in files or input.

Example:
```sh
sed 's/foo/bar/' file.txt  # Replaces the first occurrence of "foo" with "bar" in each line.
sed '/pattern/d' file.txt  # Deletes lines matching "pattern".
```

``grep``: Global regular expression print

Purpose: Searches for patterns (regular expressions) in files.

Typical Use: Filtering lines from text based on pattern matching.

Example:s
```sh
grep "error" logfile.txt  # Finds lines containing "error".
grep -i "info" file.txt  # Case-insensitive search for "info".
grep -r "keyword" /path  # Recursively searches for "keyword" in all files under `/path`.
```

### Hardlink and softlink

Hardlink: 

Creates a direct reference to the original file’s data.

Both the hard link and the original file share the same inode number (meaning they point to the same physical data on disk).

Even if the original file is deleted, the data remains accessible via the hard link.

Hard links work only within the same filesystem.

Softlink:

Creates a shortcut to another file.

Soft links have their own inode, separate from the target file.

If the original file is deleted, the soft link becomes broken

Works across different filesystems and can reference directories.

<a name="var"></a>
## 16. Environment Variables

Environment variables in Linux are used to store information that affects the behavior of the system and applications. They act like placeholders for configuration values and provide flexibility when working with scripts, processes, and the shell.

### Defining Environment Variables

Temporarily Define Variables in a Shell Session:

```sh
VARIABLE_NAME=value
export VARIABLE_NAME
```

Example:

```sh
export MY_VAR="Hello, Linux World!"
```

### Define System-Wide Variables: For all users on the system, add variables to /etc/environment or /etc/profile (requires root privileges).

```sh
sudo nano /etc/environment
```

Add ``VARIABLE_NAME=value``

### Using Environment Variables

``echo $VARIABLE_NAME`` Access a variable

``cd $HOME`` Use in command

### Listing and Managing Variables

``printenv`` View all variables

``echo $VARIABLE_NAME`` Display 1 variable

``unset VARIABLE_NAME`` Unset a variable

<a name="bash"></a>
## 17. Bash Shell

Bash stands for Bourne Again SHell. It's one of the most common command-line interpreters used in Linux and macOS systems. You use it to interact with the operating system by typing commands.

### Bash shell script that stores user/pass login to a server, create a key pair, copy the key to that server

1. Prepare a logins.txt file that stores login data

```sh
user1@192.168.1.100 password123
user2@server.example.com mysecretpass 
```

2. Make a script contains the functions

```sh
#!/bin/bash

# File containing login credentials
LOGIN_FILE="logins.txt"

# Generate SSH key pair if not exists
KEY_PATH="$HOME/.ssh/id_rsa"
if [ ! -f "$KEY_PATH" ]; then
  echo "[*] Generating SSH key pair..."
  ssh-keygen -t rsa -b 2048 -f "$KEY_PATH" -N ""
else
  echo "[*] SSH key pair already exists."
fi

# Loop through each line in the login file
while IFS=' ' read -r userhost password; do
  echo "[*] Processing $userhost..."
  
  # Use sshpass to send the public key to the server
  sshpass -p "$password" ssh-copy-id -o StrictHostKeyChecking=no "$userhost"
  
  if [ $? -eq 0 ]; then
    echo "[+] Key copied successfully to $userhost"
  else
    echo "[!] Failed to copy key to $userhost"
  fi

done < "$LOGIN_FILE"
```

Make sure the script is executable then run the script

It will output similar to:

```sh
[*] Copying key to user1@hostname...
...
Number of key(s) added: 1
...
[*] Copying key to user2@hostname...
...
[*] Copying key to user3@hostname...
...
```

Each of those:

Successfully found key at ``~/.ssh/id_rsa.pub``

Copied it to the server via ``ssh-copy-id``

Printed confirmation and a tip on how to test it using ``ssh``

This means:

The ``sshpass`` + ``ssh-copy-id`` combination worked.

The login credentials were accepted.

The key was correctly added.
