# Highlevel architecture
Hardware -> Kernel -> Shell -> User

# Kernel Architecture
hardware -> Kernel space -> System call -> User space

# Boot process
BIOS -> Level 1 bootloader [Master Boot Record (MBR)] -> Level 2 boot loader[ LILO, GRUB etc.] -> Kernel -> init

# Overview of boot process
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

In unix everything is considered as file

Regular files these can be text or binary files
- directory a special file that stores links to other file. Symbolized by d
- link a file that references to other file. It is marked with l
- named pipe special files that used for interprocess communication. Marked with a p
- socket special file used for interprocess communication. Marked with s
- device file files that represent the hardware in the system. It has two types 
  character device, marked as c & block device, marked as b

stat <- file or file system status
File system is logical collection of files on partition or disk

* Advantages of partitioning *
  Ease of use
  Performance
    Swap partition <- Swap partiton serves as overflow space for your ram
  Security
  Backup and Recovery <- eassier backup and recovery
  Stability and efficiency
  Testing <- Boot multiple operating system
  
  partition naming
    /dev/xxyN
    How to find partitions?
      /etc/fstab <- lists the partitions and mount points
      /proc/partitions
      /dev/sda*
      
 File system structure:
  Inode <-  Internal representation of file is given by inode. Many file names can point to same inode. each file will have inode. "ls -i" to view inode
  Unix file system is based on File Hierarchy Standard (FHS). But not all unix variants follow the standards completely
  "/" <- root directory. Everything starts with root directory
  "~" home directory
  "du" <- gives estimate of space used by files/directories
  "df" <- Estimae space used by file system

File permissions <- users are given restricted permissions of the files and directories
File permission sequence
  user -> group -> other -> user that own the file -> group the file belongs to
 Change permissions in relative mode:
   $sudo chmod a+w samtools-1.17.tar.bz2 <- add write permission to all users
   "+ and -" <- add and remvoe the permissions keeping other unchanged
   "=" <- asign new permissions removeing existing permissions
  Change permission in absolute mode:
    1,2,4 <- execute, write, read respectively
 File Links:
  Hard links and Soft links
  
  Hard Links: Any change made .through one file link will reflect in other. These are pointers to the inode number. Father than symbolic links. The file data is not destroyed until last link is destroyed. Links can not be created accross the partitions. Can not hardlink directory.
    $ln <source> <hardlink>
  Soft link: Its a file taht contains name of other file. Its a pointer to files content. If file is deleted the soft link becoems dangling link. Can not change permissions of soft link. Can be created across the partitions. Slower than hardlinks. Directories can have softlinks
    $ls -s <source> <softlink>
  
# File editing
  Vi requires fewer resources than other editors
  Command mode, commandline mode and insert mode
  command always starts with ":"
  vi -r <file name> : edits last saved version after crash
  vi + <filename> : places cursor on last line
  vi -R <fn> : open in readonly mode
  :w <- save changes
  :q <- quit
  :q! <- quit without save
  :<line number> <- go to line number
   gg <- first line
  G <- go to lastline
   dd <- delete line with cursor
  u <- undo previous action
  ctrl+r <- redo
  set ic <- ignore case while searching
  %s/old/new/g <- substitute old with new throught the file
  set nu <- show line numbers
 TO apply vi settings across the session edit vimrc( /etc/vim/vimrc then /home/username/.vimrc)
           
 # Shell
            Shell is the program that acts as the interface between user and the system
            Most shells are derived from original bourne shell
            Types of shell:
              sh (Bourne) <- Original
              csh, tsh, zsh <- C shell and derivatives
              ksh, pdksh <- Korn shell and its public domain version
              bash <- Bourne Again Shell. Similar to Ksh. Most popular
                      Offers comand history, command completion , arithmatic function
                      Long list of built in commands
                      Allows configuration of environment
             PATH variable
                      Its set at system level in /etc/profile
             PATH=$PAHT:new value
             Elements of shell configuration
                      Run control(.rc) files:
                        Executed when shell is booted up
                        Global configuration(/etc/profile) -> user acc level configuration files(~/.bash_profile or ~/.bash_login or ~/.profile)
                        ~/.bashrc <- file is read when new subshell starts
                        ~/.bash_louout <- file is read when everytime the login shell exits
                        $source .bash_profile <- to apply the changes in file
              Shell variable
                       To export shell variable to sub shells use "export VARIABLE"
               Prompt strings:
                              <img width="214" alt="image" src="https://github.com/manojbhosale/hello-world/assets/8487293/73a77f63-1e93-4dac-9907-28da2da9e840">
              Alias:
                "ll" is alias for "ls -l"
                $alias ll="ls -l"
              History:
                $echo $HSITFILE -> /home/ionadmin/.bash_history
  # Processes and jobs
                        
