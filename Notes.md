# Docker

## What is Docker

Docker is a platform for building, running and shipping applications. It aims to solve the "it works on my machine"
problem by packaging your application with all it's dependencies, environment variables and specific dependency versions in a stand along containers that can run on any environment (development, production or testing).

## Containers vs Virtual Machines

Virtual Machines are resource intensive, slow to start and can introduce more complexity when you have to run multiple apps and different version.

Containers share the same resource with the host OS, they are fast to start and you can run different versions of the same app without interfering with one another.

**Container**: Is an isolated environment for running an application.

**VM**: Is an abstraction of a machine (physical hardware).

## Docker Architecture

Docker uses a **Client/Server** architecture interacting using **REST APIs** the server is **Docker Engine** which sets at the background and takes care of building and running **Containers** a **Container** is a special kind of process **Containers** share the kernel of the host operating-system
**Note**: Kernel manages applications and hardware resources

## Installing the Docker

Download and install **Docker Desktop** application

`docker version` command to get docker info on your machine

```terminal
Client:
docker version

 Version:           27.2.0
 API version:       1.47
 Go version:        go1.21.13
 Git commit:        3ab4256
 Built:             Tue Aug 27 14:17:17 2024
 OS/Arch:           windows/amd64
 Context:           desktop-linux
```

## Docker Workflow

1. take an application and DOCKERIZE! it:
   - simply put a Dockerfile (a plain text file that contains instructions for docker) to it
2. give it to Docker for packaging our application into an Image
3. tell the Docker to start a container using that image

A Docker workflow typically involves a series of steps to develop, package, and deploy applications in isolated containers. Here’s an overview of the Docker workflow:

```docker
# typically start with a base image
# we can start with linux and add node on top of it
# or we can just start with node! which are build on top of linux distributions
# these images are all defined in the dockerhub
# node build on top of linux alpine distribution which results in a very small image file
FROM node:alpine
# here we say COPY all the files in the current directory into the app directory
# that image has a file-system and we're gonna create a directory called 'app'
COPY . /app
# here we specify the working directory to make file paths easier to work with
WORKDIR /app
# now using the CMD command we write the commands that start our application
# if we didn't specify the working-directory we had to write "CMD node app/app.js" because we've created an app directory withing that image
CMD node app.js
```

now that we have the **Dockerfile** we can tell the Docker to create an image of our application

in the terminal run `docker build -t image-name path-to-the-Dockerfile` for e,x: `docker build -t hello-docker .` when we're in the `docker-learning/hello-docker` folder path

the image file is not stored inside the project! it's Docker's business to store it!

to see all docker images on your machine in the terminal run `docker image ls` ls (list)

```terminal
PS D:\Courses\Docker\docker-learning> docker image ls
REPOSITORY         TAG       IMAGE ID       CREATED         SIZE
hello-docker-new   latest    8c4284648ad1   9 minutes ago   158MB
hello-docker       latest    ee4aa78d435d   2 hours ago     158MB
```

to run the image in the terminal run `docker run image-name` for e,x:

```terminal
PS D:\Courses\Docker\docker-learning> docker run hello-docker-new
Hello Docker!
```

## Essential Linux Commands

### Running Linux

first install **Ubuntu**

`docker pull ubuntu` to get it from the docker-hub but if you run `docker run ubuntu` instead it's gonna run it if it finds it in local machine otherwise will pull it from the docker-hub

`docker ps` shows the running containers

`docker ps -a` shows all the containers stopped/running

`docker run -it imageName` to run a container and interact with it `-it` stands for interactive

to start ubuntu container in interactive mode `docker run -it ubuntu`

this is the shell `root@0c53e4ac76ca:/#`, `root` is the default user with the highest privileges, `@0c53e4ac76ca` is the machine id, `#` indicates that the current user is the **root** if you log-in as normal user that symbol will be `$`

`echo` prints whatever you put after it in the terminal

`echo $0` prints the location of bash or the shell

`history` prints all the recently used commands

`Note`: bash is case-sensitive

```terminal

root@0c53e4ac76ca:/#
root@0c53e4ac76ca:/# echo hello
hello
root@0c53e4ac76ca:/# echo $0
/bin/bash
root@0c53e4ac76ca:/# Echo $0
bash: Echo: command not found
root@0c53e4ac76ca:/# history
    1  echo hello
    2  echo $0
    3  Echo $0
    4  history

```

### Managing Packages

In Ubuntu we have `apt` which stands for **advanced package tool**

```terminal

root@0c53e4ac76ca:/# apt
apt 2.7.14 (amd64)
Usage: apt [options] command

apt is a commandline package manager and provides commands for
searching and managing as well as querying information about packages.
It provides the same functionality as the specialized APT tools,
like apt-get and apt-cache, but enables options more suitable for
interactive use by default.

Most used commands:
  list - list packages based on package names
  search - search in package descriptions
  show - show package details
  install - install packages
  reinstall - reinstall packages
  remove - remove packages
  autoremove - automatically remove all unused packages
  update - update list of available packages
  upgrade - upgrade the system by installing/upgrading packages
  full-upgrade - upgrade the system by removing/installing/upgrading packages
  edit-sources - edit the source information file
  satisfy - satisfy dependency strings

See apt(8) for more information about the available commands.
Configuration options and syntax is detailed in apt.conf(5).
Information about how to configure sources can be found in sources.list(5).
Package and version choices can be expressed via apt_preferences(5).
Security details are available in apt-secure(8).
                                        This APT has Super Cow Powers.
```

install a package `nano` which is a simple text-editor for commandline

```terminal
root@0c53e4ac76ca:/# apt install nano
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
E: Unable to locate package nano
```

that is saying that the **nano** is not listed in the package-database of ubuntu, run `apt list` to see all the packages but not all the packages we need is listed there by default! that is when you run `apt update` to update the package-database. now you can install `nano`

### Linux File System

The Linux file system is structured in a hierarchical, tree-like directory format that organizes files and directories in a top-down approach, beginning from the root directory. Each directory can contain files and subdirectories, and it is designed to keep system and user data organized and accessible. Here are the key parts:

#### 1. **Root Directory (/)**

- The top level of the Linux file system, represented by a single forward slash (`/`).
- All other files and directories are contained within this root directory.

#### 2. **Key Directories in the Root**

- **/bin**: Essential command binaries needed for system operation, including basic commands like `ls`, `cp`, and `mv`. These commands are necessary for both regular users and the root user.

- **/sbin**: System binaries, mainly for administrative commands (like `shutdown`, `reboot`, `fdisk`) that are typically restricted to the root user.

- **/usr**: Contains user binaries and programs. It's one of the largest directories and includes subdirectories like `/usr/bin` (user commands), `/usr/lib` (libraries), and `/usr/share` (shared files).

- **/home**: Contains directories for each user on the system. For example, if there’s a user named "alex", they would have a directory `/home/alex` for personal files and settings.

- **/var**: Stands for "variable" and stores data that frequently changes, such as log files (`/var/log`), spool files, and temporary files used by applications.

- **/etc**: Stores system configuration files and shell scripts used to boot and initialize system settings. Examples include network configuration files, user account details, and application settings.

- **/tmp**: Temporary files created by system processes or users. Data in this directory is often deleted upon reboot.

- **/dev**: Contains device files, which represent hardware components like hard drives (`/dev/sda`), USB drives, and other peripherals. Linux treats these devices as files, allowing you to interact with hardware through the file system.

- **/lib**: Essential shared libraries required by binaries in `/bin` and `/sbin`.

- **/proc**: A virtual file system providing runtime system information, like process details, CPU info, and memory usage. Files here are generated dynamically by the system.

- **/boot**: Contains bootloader-related files, like the kernel and initial ramdisk, necessary for booting the system.

- **/opt**: Used for optional, add-on software packages that are not part of the default installation. It’s often used for third-party applications.

- **/mnt and /media**: Directories for temporarily mounting filesystems, like USB drives or CD-ROMs. `/mnt` is a general-purpose mount point, while `/media` is typically used by desktops to auto-mount devices.

- **/root**: The home directory for the root (superuser) account, separate from other user directories.

#### 3. **File Types**

- **Regular files**: Normal files that store data, text, and code.
- **Directory files**: Containers for other files and directories.
- **Device files**: Represent hardware devices, allowing the system to interact with them as if they were files.
- **Symbolic links**: Shortcuts that point to other files or directories.
- **Sockets and Named Pipes**: Used for inter-process communication (IPC).

#### 4. **Permissions and Ownership**

- Each file has permissions for the owner, group, and others, defining read, write, and execute rights.
- Ownership includes both a user (owner) and a group, which is essential for access control and system security.

#### 5. **Mounting and Unmounting**

- External devices or partitions need to be "mounted" to be accessible within the Linux filesystem.
- The `mount` and `umount` commands are used to attach and detach filesystems to specific directories within the hierarchy.

Linux's structure may initially seem complex, but it is organized this way to make it logical, flexible, and powerful, especially for administrators managing various applications and services.

### Navigating the File System

`pwd` (print working directory) to see where we are in the file-system

`ls` (list) to list all the files and directories in the path you are shows all in multiple lines `ls -1` to list them in one line

The `ls -l` command in Linux lists files and directories in the current directory in **long format**. Each line in the output provides detailed information about a file or directory, organized into columns. Here’s what each part of the output represents:

```terminal
drwxr-xr-x  2 user group 4096 Nov  7 10:30 Documents
-rw-r--r--  1 user group  123 Nov  7 11:00 file.txt
```

`cd path/you/want/to/go` (change directory) changes directory to the absolute/relative path provided (absolute path always starts with /)

`cd ..` to go one level back `cd ../..` to go two levels back

`cd ~` to go to the **home** directory for normal users, the **root** user has a special home directory called **root**

### Manipulating Files and Directories

`mkdir` to create a new directory `mkdir myDirectory`

`touch` to create a new file `touch myFile.sh` to create a shell file or `touch test.txt`

`mv` to move or rename a file `mv oldName.txt newName.txt` or `mv prev/location/name.txt new/location/name.txt`

`rm` to remove files or directories `rm test.txt` remove test.txt file, `rm myDirectory -r` to remove a directory `-r` stands for **recursive**

## Editing and Viewing Files

use `nano` which is a basic text editor for terminal:

in the terminal run `nano` to run the editor, you can optionally give it a file name to open if exists otherwise create or cancel creation by pressing `Ctrl + x`

`cat` command (concatenation) used to view content of small files, for long files it's better to use `more` command to view the large file piece by piece also gives you a **percentage** of how much of the file has viewed, with `more` you can only scroll down by pressing `Enter` key.

`less` is a newer command to replace `more` thus might not be installed by default, first install `apt install less`, now you can view content of a long file and also be able to scroll up and down.

`head -n 5 file/path/test.txt` to get the first 5 lines from the **head/top** of the file,

`tail -n 5 file/path/test.txt` to get the last 5 lines from the **tail/bottom** of the file

## Redirection

In linux the standard **input** and **output** is **keyboard** and **terminal** but we can change it this is called **redirection**.

ex: when we use `cat file.txt` it reads the content of the **file.txt** and prints it on the **standard output** but we can change it using the **redirection operation** `>`.

`cat file.txt > file2.txt`, here we redirect the output of the **cat** command which to **file2.txt**

`cat` can also be used to combine the output of multiple files into one, as following:

create two files "numbers.txt" and "letters.txt":

```terminal

root@f637cef4b947:/# echo "1 2 3 4 5" > numbers.txt
root@f637cef4b947:/# cat numbers.txt
1 2 3 4 5
root@f637cef4b947:/# echo "a b c d e" > letters.txt
root@f637cef4b947:/# cat letters.txt
a b c d e

```

use **cat** and **>** to combine "numbers.txt" and "letters.txt"

```terminal

root@f637cef4b947:/# cat numbers.txt letters.txt > alphanumeric.txt
root@f637cef4b947:/# cat alphanumeric.txt
1 2 3 4 5
a b c d e

```

the **redirection** `>` is not limited to **cat** or **echo** you can use it along with other commands as well

```terminal
root@f637cef4b947:/# ls -l > longlist.txt
```

to store the result of long listing into longlist.txt file

`<` is the **redirection** operator for changing the **standard input**

**Note**: there might not be much use cases for this command

## Searching for Text

For searching a text in a file there is `grep` command **"Global Regular Expression Print"**, `grep options regex path/to/file.txt`.

1. searching in a single file:
   `grep -i hello hello.txt`
2. searching multiple files
   `grep -i hello file1.txt file2.txt`
3. searching multiple files using a pattern for the files
   `grep -i hello file*`
   **Note**: searching all files with their names starting with **file**
4. searching in a directory and all it's sub-directories
   `grep -i -r hello /path/to/dir`
   **Note**: `-r` is for **recursive** `-i` is for **case insensitive**

**Note**: In Linux you can combine options like this: `-i -r` into `-ir`

