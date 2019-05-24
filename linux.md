# Using the command line

- ### Intro ###
    - A directory is simply another name for a folder. When we’re working at the command line, we will refer to folders as directories.
    - A computer’s files and folders are structured like a tree. At the beginning is a root directory that ultimately branches out to many other folders (each with the potential to contain more folders and files). What we’re doing when we navigate our computer’s file system is effectively walking up and down certain branches of this figurative tree structure.
    - When we enter a command line interface, we should think of ourselves as being present at a particular location on the computer — meaning that we’re currently inside some directory.
    - By default, when we open the shell, we’ll be starting at the Home folder on our computer, indicated by a tilde (```~```) symbol.
    - We’ll notice in the shell that a cursor appears after a dollar sign (```$```). This is where we will enter commands.

- ### ```pwd``` ###
    - The first command that will be useful for us is called ```pwd```, which stands for “print working directory.” When we type this command and hit the ```RETURN``` or ```ENTER``` key on our keyboards, the shell will respond by outputting what’s called an absolute path to where we are in the computer’s file structure system.
    ```console
        ~ $ pwd
        /home/ubuntu
    ```
    - By default, when we open the shell, we’ll be starting in our computer’s Home directory, displayed in abbreviated form by a tilde (```~```) symbol in the command prompt. The path to your own computer's home directory may differ depending on your username and operating system.

- ### ```ls``` ###
    - To see the contents of a directory, we can use the ```ls``` (or “list”) command, as shown below.
    ```console
        ~ $ ls
        Desktop Documents Downloads Library Movies Music Pictures Public
    ```
    - If you want to see all files in a directory (including hidden ones), you can add a flag ```ls -a``` to list “all” of the contents present. Hidden files will appear with a . preceding their names.

- ### ```xdg-open``` ###
    - To open a file or a directory
    ```console
        ~ $ open Downloads
    ```
    This will bring up a window displaying (through a GUI) the contents of the ```Downloads``` directory.
    - You can use the ```TAB``` key on your keyboard to autocomplete file and directory names that reside in your current (or “working”) directory. You may notice that autocompleting a directory name will add a trailing slash (/).
    - To open the current (working) directory, you can type the following command:
    ```console
        ~ $ open .
    ```
    The ```.``` in this context indicates your current (working) directory.

- ### ```cd``` ###
    - Recall that when you open the shell, you start out at your computer’s Home directory, abbreviated in the prompt as ```~```. If you want to move from your Home directory into another, you can use the ```cd``` (or “change directory”) command.
    - To move into a different directory, you provide that new directory’s name.
    ```console
        ~ $ cd Desktop
        ~/Desktop $
    ```
    This command will move you from the Home directory into the Desktop directory.
    - Notice that, when our current (working) directory changed from the Home (or ~) directory to the Desktop directory, the prompt text also changed from ```~ $``` to ```~/Desktop $```, That’s because the text before the $ in the prompt is, by default, set up to display an absolute path to your current location in the computer’s file structure. This can be a helpful reminder of where you are if you’re ever traversing deep into the computer’s file structure. (Alternatively, you can always use the ```pwd``` command to print out your working directory!)
    - Once you’ve changed directories, you can easily access files and folders contained in that new directory. So if you used ```ls``` command now displays the contents of the Desktop rather than the contents of the Home directory.
    - Just as we can move deeper into our computer’s file structure, we can also move back up to a higher-level folder.
    ```console
        ~/Desktop $ cd ..
    ```
    Using ```..``` indicates the parent directory, or the one above our working directory.
    - Finally, no matter where we are, if we simply type in the ```cd``` command without any destination directory, we’ll just be taken to our ```home``` directory.

- ### ```mkdir``` ###
    - The ```mkdir``` command is used to make a new directory with the name that we provide. For example, if you’re in the ```Desktop``` directory and want to create an ```animals``` directory in that location, you'd type the following command:
    ```console
        ~/Desktop $ mkdir animals
    ```
    - If you wanted to then create a ```rodents``` directory inside of ```animals```, you could do either of the following (starting from the ```Desktop```):
    use ```cd``` to move into ```animals```, and then type: ```mkdir rodents```, or
    simply run the command ```mkdir animals/rodents``` from your current directory.
    - You can also use mkdir to create multiple directories at once. To do so, you provide a list of directory names separated by spaces. For example, to create three directories with names of marsupials, cloven_hoofed_animals, and carnivores inside the animals directory, you can use the following command:
    ```console
        ~/Desktop/animals $ mkdir marsupials cloven_hoofed_animals carnivores
    ```
    - You should avoid using spaces in directory and file names (hence the underscores in ```cloven_hoofed_animals```). If this is unavoidable — perhaps if you encounter a previously created file or directory name with a space in it — you can insert what’s called an escape (```\```) character before the space to tell the shell how to properly interpret the spaces in that file name, e.g. ```mkdir cloven\ hoofed\ animals```.

- ### ```touch``` ###
    - #### Creating a file in your working directory ####
        - Until this point, you’ve most likely created and saved files on your computer by using a particular application — for example, creating a .docx file in Microsoft Word, a .pdf file in Adobe Acrobat, or an .html file in a text editor. At the command line, you can create a file in your working directory with a single command called ```touch```. The ```touch``` command creates a new (empty) file with the name and file extension that you provide. For example, if you’re in the ```Desktop``` directory and want to create a file named ```first_file.txt``` in that location, you can type the following:
        ```console
            ~/Desktop $ touch first_file.txt
        ```
        The inclusion of the file extension (```.txt``` in this case) is crucial because it sets the file type. Running the above command and then listing the contents of the ```Desktop``` directory confirms that a text file with the name ```first_file.txt``` was indeed created.

    - #### Creating a file in a directory other than the working directory ####
        - You can also use the ```touch``` command to create a file that resides in a directory other than your working directory. To do this, you must prepend to your file name the path leading to your desired destination. For instance, given the following file structure, you can create from your Desktop working directory a text file named ```capybara.txt``` that resides several layers deeper than your working directory.
        - Example file structure:<br>
        Home (or ~) directory → Desktop directory → animals directory → rodents directory → capybara.txt file.<br>
        To do so, you’d execute the following command:
        ```console
            ~/Desktop $ touch animals/rodents/capybara.txt
        ```

Creating multiple files
You can create multiple files with the touch command by providing multiple file names (including any appropriate prepended paths), separated by spaces. For example, the code below will create two files:

one file named kangaroo.txt residing at: ~ → Desktop → animals → marsupials, and
another file named giraffe.txt residing at: ~ → Desktop → animals → cloven_hoofed_animals
~/Desktop $ touch animals/marsupials/kangaroo.txt animals/cloven_hoofed_animals/giraffe.txt
Creating different file types
Lastly, it’s important to note that you aren’t restricted to creating only text files with the touch command; you can create any file type you please. For instance, the following command will create (in the Desktop working directory) a Python file with the name test.py:

~/Desktop $ touch test.py
Removing Directories and Files
In this section, you’ll learn how to use the rm command to permanently delete directories and files. We’ll start off by deleting files because it can be a bit more straightforward than deleting directories.

Removing files
The rm command
You can use the rm (or “remove”) command to delete specified files. Please note that THIS DELETION IS PERMANENT — it cannot be reversed. Only use rm if you are sure you want to delete something.

Let’s consider an example. If you want to remove a file named first_file.txt that resides in the Desktop directory, you can run the following command:

~/Desktop $ rm first_file.txt

Using rm to remove a file.

Deleting multiple files is accomplished by providing a list of file names, separated by spaces. For instance, the image below demonstrates a scenario in which we use the touch command to create three text files in our Desktop directory — apples.txt, carrots.txt, and fruits.txt — and then remove (or permanently delete) those files using the rm command. The code to accomplish this deletion is as follows:

$ rm apples.txt carrots.txt fruits.txt`

Caption: Using rm to remove multiple files.

Removing directories
You just learned how to remove files using the rm command. Here, we’ll consider two ways to remove a directory:

using the rmdir command, and
using the rm -r command (NOTE: EXERCISE CAUTION).
The rmdir command
The rmdir command can be used to delete directories, but it’s important to note that it can only remove completely empty directories. For example, you can use mkdir to create a directory called cats inside the Desktop directory. Because cats is just an empty directory (nothing has been added to it), you can successfully use the rmdir command to remove the cats directory, as shown in the image below.


Using rmdir to remove an empty directory.

However, if you try to run rmdir on a directory that is not empty, you’ll receive an error message. For example, if you create a cats directory and then add files to it (e.g. munchkin.txt and tabby.rb), you won’t be able to use rmdir to remove the cats directory, as shown in the image below.


Error message — rmdir cannot remove any directory with contents.

A potential solution would involve first emptying the directory’s contents one file at a time (using the rm command you learned above) and then using rmdir to remove the emptied directory, but this can be inefficient if a directory contains many files. The next section reveals a faster approach.

The rm -r command
As you saw above, using rmdir to remove directories was somewhat limited because it only could remove empty directories. Here, you’ll learn how to delete directories — including those with contents — by executing a slightly different version of the rm command you used earlier to delete files.

To remove a directory, you can add something called a flag or option to the rm command. Flags provide additional execution instructions. They are included after the command name but before the argument. Flags are indicated by letters following a dash (-) symbol. The complete command we’ll use in this section is rm -r, where r stands for recursive.

CAUTION: Before you proceed, you should know that recursive deletion means deleting all contents of a directory — that includes its files, its sub-directories, any files within those sub-directories, and so on. Furthermore, deletion with rm -r is a permanent action. You can easily and irreversibly delete great numbers of files with this one command.

Let’s consider an example. If you want to remove a non-empty directory named cats that lives in your Desktop directory, you could use the following command:

~/Desktop $ rm -r cats
If you’d like to be asked to confirm the deletion of individual items contained in a directory, you can add the interactive (-i) flag to your command, either by combining it with the -r flag (e.g. rm -ri) or by adding it separately (e.g. rm -r -i). For instance, if the cats directory happened to contain two files (file_1.txt and file_2.txt) and four sub-directories (calico, persian, scottish_fold, and siamese), you could use the following command to delete the cats directory after confirming the deletion of its several contents:

~/Desktop $ rm -ri cats
To proceed through these confirmation messages, you can simply type yes or y. The image below depicts this interaction.


Using rm -ri to remove a non-empty directory only after confirming deletion of its contents.

Summary of commands
In the preceding command line tutorial, you learned how to execute the following commands:

ls, which lists the contents of a directory,
cd, which changes your working directory,
pwd, which prints your working (current) directory,
open / start, which opens a file (on Mac or Windows, respectively),
touch, which creates a new file with a specified extension or file type,
mkdir, which makes (creates) a new directory,
rm, which permanently removes a file,
rmdir, which permanently removes an empty directory,
rm -r, which permanently removes a directory and its contents (without confirmation), and
rm -ri, which permanently removes a directory and its contents (with confirmation).

### ```diff``` command
- used to compare files and directories.
  - ```-c``` Provides a listing of differences that include three lines of context before and after the lines differing in content
  - ```-r``` 	Used to recursively compare subdirectories, as well as the current directory
  - ```-i``` 	Ignore the case of letters
  - ```-w``` 	Ignore differences in spaces and tabs (white space)
  - ```-q``` 	Be quiet: only report if files are different without listing the differences
- ```diff3``` command is used to compare three different files.
- ```patch``` command is used to patch a file of differences to a new file. the file is usually generated with the ```diff``` command. ```diff -Nur originalfile newfile > patchfile``` creates the patch file and ```$ patch originalfile patchfile``` patches it.
- ```file``` command is used to test the file type. For example, ```$ file <filename>```.

### ```rsync``` command
- ```rsync``` is very efficient when recursively copying one directory tree to another, because only the differences are transmitted.
- ```rsync``` can be very destructive! It is highly recommended that you first test your rsync command using the -dry-run option to ensure that it provides the results that you want.

### Compressing Commands
- ```gzip -r projectX``` Compresses all files in the projectX directory, along with all files in all of the directories under projectX.
- ```gunzip foo``` de-compresses the archive foo.
- ```zip -r backup.zip ~``` Archives your login directory (~) and all files and directories under it in the file backup.zip.
- ```unzip backup.zip``` Extracts all files in the file backup.zip and places them in the current directory.
- ```tar xvf mydir.tar``` Extract all the files in mydir.tar into the mydir directory.
- ```tar zcvf mydir.tar.gz mydir``` Create the archive and compress with gzip.

### Miscellaneous commands
- ```whoami``` shows the logged in user in the current terminal and ```who``` shows the current logged-in users with option ```-a``` to view more info about them.

## Linux File System
- ![Linux FileSystem Structure](http://bit.ly/2GTNoZY)
- In Linux (and all UNIX-like operating systems) it is often said “Everything is a file”. This means whether you are dealing with normal data files , or with devices such as sound cards and printers, you interact with them through the same kind of Input/Output (I/O) operations. This simplifies things: you open a “file” and perform normal operations like reading the file and writing on it.
- The filesystem is structured like a tree. The tree is usually portrayed as inverted, and starts at what is most often called the root directory, which marks the beginning of the hierarchical filesystem  simply denoted by **/**.
- Linux supports native filesystem types, created by Linux developers "ext3, ext4, squashfs, btrfs" and other filesystems for align os like "ntfs, vfat" for windows or "hfs, hfs+" for MacOS.
- Before you can start using a filesystem, you need to mount it to the filesystem tree at a mount point. This is simply a directory (which may or may not be empty) where the filesystem is to be attached (mounted).

### Mounting and Unmounting
- The mount command is used to attach a filesystem somewhere within the filesystem tree.
- to mount a file system, use the command ```$ sudo mount <device node> <mount directory>```. For example, ```$ sudo mount /dev/sda5 /home```.
- to unmount a file system, use the command ```$ sudo umount <mount directory>```. For example, ```$ sudo umount /home```.

### FileSystem Directory Structure
- ```/bin``` contains executable binaries to load the system and essential commands required by all system users, such as ```cat```, ```cp```, ```ls```, ```mv``` and ```rm```.
- ```/sbin``` is intended for essential binaries related to system administration, such as ```fsck``` and ```shutdown```.
  - Commands that are not essential (theoretically) for the system to boot or operate in single-user mode are placed in the ```/usr/bin``` and ```/usr/sbin``` directories. Historically, this was done so ```/usr``` could be mounted as a separate filesystem that could be mounted at a later stage of system startup or even over a network. However, nowadays most find this distinction is obsolete. In fact, many distributions have been discovered to be unable to boot with this separation. Thus, on some of the newest Linux distributions ```/usr/bin``` and ```/bin``` are actually just symbolically linked together.
- ```/proc``` is called pseudo-filesystems because they have no permanent presence anywhere on the disk, contains virtual files (files that exist only in memory) that permit viewing constantly changing kernel data like ```/proc/cpuinfo```, ```/proc/meminfo```, ```/proc/mounts```, ```/proc/<Process-ID-#>``` and ```/proc/sys```.
- ```/dev``` directory contains device nodes, a type of pseudo-file used by most hardware and software devices like ```/dev/sda1``` (first partition on the first hard disk) and ```/dev/random``` (a source of random numbers).
- ```/var``` contains files that are expected to change in size and content as the system is running like ```/var/log``` "System log files", ```/var/tmp``` "Temporary files", ```/var/spool``` "Print queues" and Network services directories such as ```/var/www``` "the HTTP web service".
- ```/etc``` directory is the home for system configuration files. Files like ```passwd```, ```shadow``` and ```group``` for managing user accounts are found in the ```/etc``` directory. ```/etc``` is for system-wide configuration files and only the superuser can modify files there. User-specific configuration files are always found under their home directory.
- ```/boot``` directory contains the few essential files needed to boot the system like ```vmlinuz``` "compressed Linux kernel", ```initramfs``` "initial ram filesystem" and ```config``` "kernel configuration file". The Grand Unified Bootloader (GRUB) files such as ```/boot/grub/grub.conf``` or ```/boot/grub2/grub2.cfg``` are also found under the ```/boot``` directory.
- ```/lib``` contains libraries (common code shared by applications and needed for them to run) for the essential programs in ```/bin``` and ```/sbin```. On some Linux distributions there exists a ```/lib64``` directory containing 64-bit libraries, while ```/lib``` contains 32-bit versions. Kernel modules (kernel code, often device drivers, that can be loaded and unloaded without re-starting the system) are located in ```/lib/modules/<kernel-version-number>```.
- ```/opt``` is for	Optional application software packages.
- ```/sys``` is for Virtual pseudo-filesystem giving information about the system and the hardware.
Can be used to alter system parameters and for debugging purposes
- ```/srv``` for Site-specific data served up by the system.
- ```/tmp``` 	Temporary files; on some distributions erased across a reboot and/or may actually be a ramdisk in memory.
- ```/usr``` 	Multi-user applications, utilities and data "theoretically non-essential programs and scripts".
### How actual data is stored?
- The Unix filesystem has several separate notions for addressing data on disk:
  - DataBlocks : are a group of blocks on a disk which have the contents of a file.
  - INode : is a data structure in a Unix-style file system which describes a filesystem object such as a file or a directory. Each inode stores the attributes and disk block location(s) of the object’s data. Filesystem object attributes may include metadata (times of last change, access, modification), as well as owner and permission data.
	> Note: That's why some files can be retrieved back after they were deleted. When deleting a file, only its inode is deleted but its datablocks don't get erased. So If those datablocks weren't overwritten, they can be parsed and the file can be retrieved back.

- A file is actually composed of three different things:
  - a PATH in the filesystem
  - an inode with metadata
  - data blocks pointed to by the inode

A directory entry is basically a mapping from filename to inode number. And a directory is a special file that contains directory entries.

### Answers to some weird questions ..
- Why don't directories know their own size?
  - Because they only contain pointers to other stuff, you have to iterate over their contents to find the size
- Why aren't directories ever empty?
  - Because they contain at least the . and .. entries. Thus, a proper directory will be at least as small as the smallest filesize that can contain those entries. In most filesystems, 4096 bytes is the smallest.
- How the size of the directory is calculates when using ```ls -l``` ?
	- It's actually the allocated size for this directory "number of blocks associated with the inode times the size of each block".

## Links
- What is INode ?
- ![File System Simple Structure](http://web.cs.ucla.edu/classes/fall08/cs111/scribe/11/ospfssample3.gif)

### Soft Links
- A soft link is similar to the file shortcut feature which is used in Windows Operating systems. Each soft linked file contains a separate Inode value that points to the original file. Any changes to the data in either file is reflected in the other. Soft links can be linked across different file systems, although if the original file is deleted or moved, the soft linked file will not work correctly (called hanging link).
- You can create a soft link using this command
  ```console
  $ ln -s [original filename] [link name]
  ```

### Hard Links
- Each hard linked file is assigned the same Inode value as the original, therefore they reference the same physical file location. Hard links more flexible and remain linked even if the original or linked files are moved throughout the file system, although hard links are unable to cross different file systems or links directories.
- Just adds a new filename in the filesystem hierarchy that points to the same inode of the target.
- Why can't a hard link to directory be created ?
  - This is just a bad idea, as there is no way to tell the difference between a hard link and an original name. As if you were allowed to do this for directories, two different directories in different points in the filesystem could point to the same thing. In fact, a subdir could point back to its grandparent, creating a loop when traversing.
  **why is this loop a concern?** Because when you are traversing, there is no way to detect you are looping (without keeping track of inode numbers as you traverse). Imagine you are writing the `du` command, which needs to recurse through subdirs to find out about disk usage but there is a hard link to a parent directory within the current directory ? It would be infinite loop.
- You can create a hard link using this command
  ```console
  $ ln [original filename] [link name]
  ```

### Soft Links V.S. Hard Links V.S Regular Copies
| Soft Link | Hard Link | Regular Copy |
|--|--|--|
| you have one file with one filename and a pointer to that file with the other filename. | you have one file with two different filenames. | you have two different versions of the file |
| if you edit the link its really editing the original file | If you edit one, it gets edited in all filename locations | if you edit one, the other one stays the same. |
| if you delete the file the link is broken and if you remove the link the file stays in place. | if you delete one, it still exists in other places | if you delete one, the other one stays there, but it may not be identical if it was edited |
| only one file on disk | only one file on disk | twice as much disk space used (two different files) |

## Vim
- use ```vimtutor``` to enter the vim tutorial provided by the system.
- VI has 3 modes, keystrokes and command behave differently in different modes.
  - Command Mode: Keyboard strokes are interpreted as commands that can modify file contents "the dafault mode".
  - Insert Mode: Type ```i``` to switch to it. Insert mode is used to enter (insert) text into a file. Insert mode is indicated by an ```“? INSERT ?”``` indicator at the bottom of the screen. Press ```Esc``` to exit Insert mode and return to Command mode.
  - Line Mode: Type ```:``` to switch to the Line mode from Command mode. Each key is an external command, including operations such as writing the file contents to disk or exiting.
- use ```:w``` to write to the file, ```:q``` to quit, ```:wq``` to write then quit, ```:w file_name``` to write to a file with a specific name, ```:w! file_name``` to overwrite the file and ```:q!``` to exit without saving file.
- Use ```w``` to move to the next word. ```$``` to go to the end of the line. ```0``` to go to the beginning of the line.
- Use command ```/<pattern>``` to search for a pattern. use ```n``` and ```N``` to move between the patterns occurences.
- Use ```o``` to insert text in a line below the current line, ```O``` to insert text above the current line.
- Use ```dw``` to delete word in the current position, ```dd``` to delete the current line, ```D``` to delete the rest of the current line.
- Use ```yy``` to copy the current line, ```yNy``` or ```Nyy``` to copy N lines and ```p``` to paste the lines in the buffer in the current posistion.
- Use ```: sh``` opens external command shell. When you exit the shell, you will resume your vi editing session. Use ```: ! to run a command within your vim session.

## User Evnironment
- ```alias``` command shows the current defined aliases. You can add your own aliases in ```.bashrc``` with the syntax ```alias <defined_alias>=<aliased_expression>```.

## Users and Groups
- Linux uses the concept of users to separate various people who use the computer. Every user has some properties associated with them, such as a user ID and a home directory.
- In order to make managing users easier, you can add users into a “group”. A group can have zero or more users. A particular user is associated with a “default group”, and can also be a member of other groups on the system.
- to add new user use ```sudo useradd <user>```.
- ```userdel <user>``` will delete the user and you can use ```-r``` flag to remove the home directory for the user ```/home/<user>```.
- ```id``` command will show info about the current user. ```id <user>``` will show info about the user specified.
- To view the users of the system ```cat /etc/passwd```.
- Similarly, you can view the groups on your system by viewing the ```/etc/group``` file, by running ```cat /etc/group```
  > When running these commands, you will notice that there are a number of other users and groups that you didn’t create. These are system users and groups, which are used to run background processes securely.

## File permissions
- Linux is a multi-user operating system, and it ensures the security of files with the concepts of “ownership” and “permissions”.

### Ownership
- Every file and directory on your system is assigned 3 types of owner
- A user is the owner of the file. By default, the person who created a file becomes its owner. Hence, a user is also sometimes called an owner.
- A group can contain multiple users. All users belonging to a group will have the same access permissions to the file. If the owner of the file is in the owner group, users permissions are applied when manipulating the file instead of the group permissions.
- Others “all other users on the system” or “Not the owner of the file or one of the users in the owner group.
- You can change the ownership using ```chown``` command.
  - ```sudo chown root test.txt``` will change the owner for the file to be ```root``` user.
  - ```sudo chgrp root test.txt``` or ```sudo chown :daemon test.txt``` will change group owner for the file to be ```root``` group.
  - ```sudo chown root:daemon test.txt``` will change the owner user and the owner group for the file.

### Permissions
- For the file
  - the read permission allows a user to view the contents of a file
  - the write permission allows a user to modify and delete a file.
  - When set on a file, the write permission allows it to be executed.    
- For the directory
  - the read permission allows the user to list the content of that directory "Just lists the file name and INode number so if you list the dir with ```-l``` flag will not work as it tries to get more information that it has access to".
  - The write permission on a directory gives you the authority to add, remove and rename files stored in the directory.
  - the write permission allows the user to enter the directory (with cd) and view metadata (like file permissions and INode informations) of the files and directories within it.
- ![Linux File Permissions](https://i.ibb.co/yBVthKk/Permissions-Concept.png)
- To wrap up, Each file has 3 types of accessors. Each of them has a 3 set of permissions.
- The default permissions are 775 for directories and 644 for files.
- Why should they have read permissions for others ?
  - It’s a security compromise. For example, /etc directory that has configs files is owned by the root but it’s still accessed by many other services. So it can’t be too-restricted.

#### Changing the permissions
- Absolute
  - Permissions are 3 octet ranging from 0 - 7 indicting the permissions in the format rwx
  - ```chmod <permissions> <filename>```
  - ```chmod 644 file1``` will set read and write permissions for user, read for both group and others.
- Symbolic
  - In the Absolute mode, you change permissions for all 3 owners. In the symbolic mode, you can modify permissions of a specific owner.
  - It has 3 symbols for manipulating permissions
    - \+ Adds a permission to a file or directory.
    - \- Removes the permission.
    - = Sets the permission and overrides the permissions set earlier.
  - It has 3 symbols for representing the ownership to change the permission for
    - u - Owner
    - g - Group
    - o - Others
    - a - All users
  - ```chmod a-rw file1``` this will grant read and write permissions to all the users.
  - ```chmod o-rx,g-w file.txt``` will remove the read and execute permissions from the others and remove write from group.

#### Web App Permissions Example "Production"
- The next model is fine for apps in production. The web server will be the only user to write to the project.
- Make the server user the owner and the group of the project
  - ```sudo chown -R www-data:www-data /var/www/example-project-name/```
- That will make only the web server the ability to write to the project.
  - ```sudo find /var/www/example-project-name/ -type d -exec chmod 755 {} \;```
  - ```sudo find /var/www/example-project-name/ -type f -exec chmod 644 {} \;```

#### Web App Permissions Example "Development"
- The next model is fine for apps in development. The user and the group can write to the project.
- Make the root "or you user" and the server group as owner and group-owner for the project. 
  - ```sudo chown -R root:www-data /var/www/example-project-name```
- Make identical permissions for user and group so that they can write to the project.
  - ```sudo find /var/www/example-project-name/ -type f -exec chmod 664 {} \;```
  - ```sudo find /var/www/example-project-name/ -type d -exec chmod 775 {} \;```

### Access rights flags
#### The Sticky Bit
- When you set a sticky bit on a directory, files in that directory can be only removed or renamed by the root user, the directory owner, or the file owner. That's very useful to be used for directories in shared environments.
- ```chmod +t shared_directory``` or ```chmod 1775 shared_directory``` will add the sticky bit to the directory.
- ```chmod -t shared_directory``` or ```chmod 775 shared_directory``` will remove the sticky bit from the directory.
- A practical example of this is the ```/tmp``` directory, where programs (running under different users) can store temporary files. To prevent accidental deletion of other user’s files, Linux distributions set the sticky bit on ```/tmp```.
- The sticky bit does not have any effect on files.

#### ```setuid``` and ```setgid``` bits
- By default, the ownership of files and directories is based on the default uid (user-id) and gid (group-id) of the user who created them. The same thing happens when a process is launched: it runs with the effective user-id and group-id of the user who started it.
- When the ```setuid``` bit is used, the behavior described above it's modified so that when an executable is launched, it does not run with the privileges of the user who launched it, but with that of the file owner instead.
- So, for example, if an executable has the ```setuid``` bit set on it, and it's owned by root, when launched by a normal user, it will run with root privileges. It should be clear why this represents a potential security risk, if not used correctly.
- The setuid bit has no effect on directories. However, when you set the setgid bit on a directory
  - When a user creates new files or subdirectories inside this directory, they inherit the owner group. This differs from the default behaviour, where newly created files are owned by the user’s default group.
  - Any new subdirectories also have the setgid bit set.
- ```sudo chmod +s <filename>``` will add setuid bit to the file and ```sudo chmod -s <filename>``` will remove it.
- ```sudo chmod g+s <filename>``` will add setgid bit to the file and ```sudo chmod g-s <filename>``` will remove it.
- when using the absolute assignment for the ```setuid```, ```setgid```, and ```sticky``` bits are represented respectively by a value of 4, 2 and 1. So if we want to set the setgid bit on a directory we would execute ```chmod 2775 test```.

### Controlling Default Permissions "umask"
- On most distributions, you will see that ```newFile``` gets a permission of ```664 (rw-rw-r--)``` , and ```newDir``` gets a permission of  ```775 (rwxrwxr-x )```.
- An octal number, called “file mode creation mask” controls these default permissions. ```umask``` command allows you to control this mask. this only controls the behavior of programs launched from the shell.
- Files have a base permission of ```666 (or rw-rw-rw-)``` and directories have a base permission of ```777 (or rwxrwxrwx)```. To get the actual permissions, we take the base permission and subtract it from the mask. By default, shells use a mask of ```002```. If you perform the calculation, you’ll end up with the default permissions we saw earlier.
- use ```umask <mask value>``` to set the umask for the current user session. For example, ```umask 077``` will make the new files with ```600``` permissions and new directories with ```700``` permissions.

## Manipulating Text
### ```grep``` command
- ```grep``` is extensively used as a primary text searching tool. It scans files for specified patterns and can be used with regular expressions.
- ```grep [pattern] <filename>``` searches for and print the lines of the file which match the pattern.
- ```grep -v [pattern] <filename>``` searches for and print the lines of the file which don't match the pattern.
- ```grep -C 3 [pattern] <filename>``` catches and prints the context of lines (specified number of lines above and below the pattern) for matching the pattern.
- ```grep <pattern1|pattern2> <filename>``` to search for multiple patterns.
- ```grep -e <regex> <filename>``` uses regular expression to search in files.

### ```strings``` command
- ```strings``` is used to extract all printable character strings found in the file or files given as arguments. It is useful in locating human-readable content embedded in binary files.
- ```strings book1.xls | grep my_string``` searches for the string my_string in a spreadsheet.