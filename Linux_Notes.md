#Highlevel architecture
Hardware -> Kernel -> Shell -> User

#Kernel Architecture
hardware -> Kernel space -> System call -> User space

#Boot process
BIOS -> Level 1 bootloader [Master Boot Record (MBR)] -> Level 2 boot loader[ LILO, GRUB etc.] -> Kernel -> init

#Overview of boot process
• The system BIOS checks the system and launches the first stage boot loader on the MBR of the primary hard disk.
• The first stage boot loader launches the second stage boot loader from the /boot/ partition.
• The kernel is loaded into memory, which in turn loads any necessary modules and mounts the root partition read-only.
• The kernel hands control of the boot process to the /sbin/init program
• The /sbin/init program loads all services and user-space tools, and mounts all partitions listed in /etc/fstab.
• The user is presented with a login prompt for the freshly booted Linux system


pstree <- process tree starting from init process

Run levels: 
0 = Halt
1 = single user(for maintainance)
2 = Multisuer mode without multiuser networking
3 = Full multiuser mode with networking
4 = User definalble, but duplicate of 3
5 = Full multi-user mode (with X based login screen)
6 = reboot

Command-line is not resource intensive as UI

cat /proc/version <- To get kernel version
halt <- brings down the system immediately
init 0 <- poweroff system using predefined scripts to cleanup system prior to shutdown
inti 6 <- Reboot system (Not available on all linux versions)
poweroff <- shuts down the system by powering off 
reboot <- reboots the system
shoutdown <- shutdown the system 

Unix IS CASE SENSITIVE 

Ctrl + c <-Terminat ecurrent command 
Ctrl + D <- logoff or terminate the session

man, info, whatis, apropos <- commands for help. whatis serches the database of oneline description for commands 

3 types of unix accounts:
root acc <- can  do absoulutely anything on the system
system acc <- req. for system specific components e.g. mail acc, sshd acc
user acc <- limited access to the critical system files and directories

/etc/passwd <-name and user ids are stored
homedir and shell are assigned to each user
users can not read write and execute each other files without permissions
users, w, who <- lists currently logged in users with
/etc/group <- gids are stored 
/etc/shadow <- holds all encrypted passwords

There are three main user administration files
- /etc/passwd – identifies the authorized accounts for the system
- /etc/shadow – holds the encrypted password of the corresponding account. Was not present on earlier Unix systems
- /etc/group – Contains information on group accounts

su <-  need to login to another account without logging out of the system. Running just "su" will take to the root account
sudo <- used to run command as another user or super user

## Files ad directories
