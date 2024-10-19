# Linux Luminarium: First 6 Modules

Welcome to my README of the Linux Luminarium, where I explore the essential commands and concepts of Linux. Here's a summary of my experience across the first 6 modules, including some commands that I struggled with and later conquered.

---

## 1. Hello Hackers 🌐

This module introduced me to basic commands and arguments.

- **Commands**: Linux is all about commands like `ls`, `pwd`, and `cd`.
    ```bash
    ls  # lists the contents of the current directory
    pwd # prints the current working directory
    cd /path/to/directory  # changes to another directory
    ```
- **Arguments**: Commands become more powerful with arguments.
    ```bash
    ls -l  # lists detailed info of files and directories
    ```

At first, understanding the power of arguments was tricky, but this module set a solid foundation.

---

## 2. Pondering Paths 🗺️

Navigating Linux's file system was a bit confusing at first, but I learned to handle absolute and relative paths effectively.

- **Paths**:
    ```bash
    pwd             # show current location
    cd /            # move to the root directory
    cd ..           # move one directory up
    cd ~/Documents  # move to the Documents folder inside home
    cd ./folder     # move into a folder relative to where I am
    ```

I remember getting lost using relative paths, but now I’m comfortable jumping from one place to another, especially between home and root.

---

## 3. Comprehending Commands 🛠️

This module got me into actual file handling and manipulation, which was both exciting and frustrating at times.

- **Viewing and Creating Files**:
    ```bash
    cat file.txt     # show the contents of file.txt
    ls -a            # list all files, including hidden ones
    touch newfile.txt # create an empty file
    mkdir newdir     # create a new directory
    ```
    I struggled with hidden files for a while, not realizing that `ls` won’t show them unless I used `ls -a`.

- **Removing Files**:
    ```bash
    rm file.txt      # delete file.txt
    rmdir folder     # remove an empty directory
    rm -r folder     # remove a directory and its contents
    ```

I accidentally deleted a file early on with `rm`, realizing there’s no undo! It was a hard-learned lesson in caution.

---

## 4. Digesting Documentation 📚

This was an eye-opener—learning how to access manuals and help. I now know that almost every command has a man page!

- **Reading Documentation**:
    ```bash
    man ls          # open the manual for 'ls'
    man -k search   # search for commands related to 'search'
    ls --help       # quick help for the 'ls' command
    help cd         # help for built-in commands like 'cd'
    ```
    
Finding out about `man` and `--help` was a relief. I used `man grep` so many times to understand different flags.

---

## 5. Globbing 🌟

This was the start of something powerful—using patterns to work with multiple files at once. I had a few hiccups here (like missing out the `*` at the end), but it all made sense with practice.

- **Wildcards**:
    ```bash
    ls *.txt          # match all .txt files
    ls [abc]*.txt     # match files starting with 'a', 'b', or 'c'
    ```
    
    I faced issues with globbing, like this one where I had to fix my pattern:
    ```bash
    echo LOOK: [cep]*  # correctly matches files starting with 'c', 'e', or 'p'
    ```

Globbing was hard to wrap my head around at first, but it’s a huge time saver.

---

## 6. Practicing Piping 🔧

Finally, piping—one of the most interesting parts of Linux. I learned how to pass the output of one command to another.

- **Piping and Redirection**:
    ```bash
    ls | grep txt        # pipe output of 'ls' into 'grep' to find .txt files
    echo "hello" > file  # redirect the output to a file
    cat file >> otherfile # append file contents to another file
    ```
    I also ran into challenges piping stderr and stdout separately:
    ```bash
    /challenge/hack 2> >(tee /challenge/the) | tee /challenge/planet
    ```
    Here I was working with `stderr` and `stdout` simultaneously using `tee`.

---
Here’s a more detailed README document from a student's perspective, highlighting the concepts and techniques learned during the command line exploitation challenge. This version emphasizes a learning journey, includes explanations, and is structured for clarity.

---

# README: Learning Arc in Command Line Exploitation Challenge

## Introduction

This document serves as a comprehensive overview of my learning journey through a command line exploitation challenge. My goal was to understand various concepts related to shell scripting, process management, file permissions, and command hijacking. By the end of this challenge, I have gained practical knowledge in manipulating the command line environment, managing processes, and executing commands to retrieve a flag from a secure system.

## Objectives

- Gain a foundational understanding of shell variables and their manipulation.
- Learn to manage processes and understand their states.
- Master file permissions and ownership to access protected resources.
- Develop skills in reading files and executing scripts in a secure environment.
- Create custom commands to bypass restrictions and retrieve sensitive data.

## Concepts and Techniques

### 1. Printing Variables

In shell scripting, variables are a crucial way to store information. To print the value of a variable, I can use the `echo` command along with the `$` sign, which denotes variable expansion.

```bash
# Example of printing a variable
echo $FLAG
```
**Output**: This command reveals the value of the `FLAG` variable, which in this case is: 
```
pwn.college{0RZh_h3DR6SUsllkz6pT5w5MSZw.ddTN1QDL3IjN0czW}
```

### 2. Setting Variables

I learned that to set a variable, I simply assign a value to it without the `$` sign. This allows me to create a variable for future use.

```bash
# Setting a variable
VAR="Some value"  # Assign a value to the variable
echo $VAR         # Access the value of the variable
```
**Output**: This will print:
```
Some value
```
**Flag**: 
```
pwn.college{EUhuzaX7IqWtLCI8RAz4POIwV-l.dlTN1QDL3IjN0czW}
```

### 3. Multi-word Variables

When dealing with multi-word variable names, I can use underscores or quotes to ensure the variable is correctly set.

```bash
# Multi-word variable example
MULTI_WORD_VAR="This is a multi-word variable"
echo $MULTI_WORD_VAR
```
**Output**: This will print:
```
This is a multi-word variable
```
**Flag**: 
```
pwn.college{ACBbP4yx6X1LfA4A5I6IVUih_BR.dBjN1QDL3IjN0czW}
```

### 4. Exporting Variables

Exporting a variable using the `export` command makes it available to any child processes spawned from the current shell.

```bash
# Exporting a variable
export MY_VAR="Exported value"
```
**Flag**: 
```
pwn.college{0665MokijzzvRFvpOQ9l2bXoB9q.dJjN1QDL3IjN0czW}
```

### 5. Printing Exported Variables

To display all exported variables, I can use the `env` command. This helps in understanding the environment variables currently set.

```bash
# Display all exported variables
env
```
**Flag**: 
```
pwn.college{QLeSy9tTAMCrWZa1G48k7yAK8S3.dhTN1QDL3IjN0czW}
```

### 6. Storing Command Output

Storing the output of a command in a variable is done using backticks or the `$()` syntax. This is useful for dynamic variable assignment.

```bash
# Store the output of a command
OUTPUT=$(ls)  # Store the output of ls in OUTPUT
```
**Flag**: 
```
pwn.college{UkQsO7622GayCFKZ0BKeey91kHF.dVzN0UDL3IjN0czW}
```

### 7. Reading Input

The ability to read input from either a command or directly from user input is fundamental. I practiced this by piping the output of one command into a variable.

```bash
# Reading input from a command
echo "COLLEGE" | read PWN  # Reads input into PWN variable
```
**Flag**: 
```
pwn.college{oUmZeGd5oB9goWng50kMXqD4j3W.dhzN1QDL3IjN0czW}
```

### 8. Reading Files

Reading the contents of a file into a variable or displaying it helps in data retrieval tasks. Using `cat` is the simplest way to do this.

```bash
# Reading a file's contents
cat filename.txt
```
**Flag**: 
```
pwn.college{YJqoD3AkJvDhkk7Z7rNfB82len5.dBjM4QDL3IjN0czW}
```

### 9. Listing Processes

The `ps` command allows me to see all running processes, which is essential for process management and monitoring.

```bash
# List all running processes
ps aux
```
**Flag**: 
```
pwn.college{InD43oalrfbLQt0_p7Eh89DPTKO.dhzN4QDL3IjN0czW}
```

### 10. Killing Processes

To terminate a process, I need to know its PID (Process ID). Using the `kill` command, I can stop any unnecessary processes.

```bash
# Terminating a process using its PID
kill <PID>
```
**Flag**: 
```
pwn.college{IWC32AQijSQrq8uvXsxx2CZqFuv.dJDN4QDL3IjN0czW}
```

### 11. Interrupting Processes

I learned how to send an interrupt signal to a process using the `kill` command with the `-SIGINT` option.

```bash
# Sending an interrupt signal to a process
kill -SIGINT <PID>
```
**Flag**: 
```
pwn.college{Am2tYQni_CrOF9POBbXYtYUpLm1.dNDN4QDL3IjN0czW}
```

### 12. Suspending Processes

Using `Ctrl + Z`, I can suspend a running process, allowing me to temporarily pause it without terminating it.

**Flag**: 
```
pwn.college{Y39ckkzk_TzB7M3dxitq5rqD5e4.dVDN4QDL3IjN0czW}
```

### 13. Resuming Processes

To resume a suspended process, I can bring it back to the foreground using the `fg` command, or continue it in the background with `bg`.

```bash
# Resuming a suspended process in the foreground
fg %1
```
**Flag**: 
```
pwn.college{I9pWI0C7NXG2Qjr4wAGJkCaIjsR.dZDN4UDL3IjN0czW}
```

### 14. Backgrounding Process

Running a process in the background allows me to continue using the terminal for other commands. This is done by appending `&` to the command.

```bash
# Running a process in the background
./long_running_process &
```
**Flag**: 
```
pwn.college{8sLDJi6AKEh6KgeOwWS-eRfDLPx.dlDN4QDL3IjN0czW}
```

### 15. Foregrounding Processes

To bring a background process back to the foreground, I can use the `fg` command followed by the job number.

```bash
# Bringing a background process to the foreground
fg %1
```
**Flag**: 
```
pwn.college{YHcG12kSp68ItGeFGecj0u2MiRN.dhDN4QDL3IjN0czW}
```

### 16. Starting Backgrounded Process

I can start a long-running process directly in the background with the `&` at the end of the command.

**Flag**: 
```
pwn.college{8sLDJi6AKEh6KgeOwWS-eRfDLPx.dlDN4QDL3IjN0czW}
```

### 17. Process Exit Codes

Understanding exit codes is essential for troubleshooting. The exit status of the last executed command can be checked with `$?`.

```bash
# Checking the exit status
echo $?
```
**Flag**: 
```
pwn.college{QnxUJw6qSr4vwMhQW4DqKg4sSqX.dljN4UDL3IjN0czW}
```

### 18. Changing File Ownership

To change the owner of a file, I used the `chown` command, which is vital for managing file access rights.

```bash
# Changing file ownership
chown newowner filename
```
**Flag**: 
```
pwn.college{sGZjnWeoMMm6b7dVpmxsTl_Sd5e.dFTM2QDL3IjN0czW}
```

### 19. Groups and Files

Managing file permissions involves understanding user groups. Changing

 group ownership can be done using `chgrp`.

```bash
# Changing group ownership
chgrp newgroup filename
```
**Flag**: 
```
pwn.college{ExTshF_zOFH9NGgCEv_YG3wUTuA.dhDN4QDL3IjN0czW}
```

### 20. File Permissions

Setting file permissions correctly is crucial. I practiced using the `chmod` command to set read, write, and execute permissions for files and directories.

```bash
# Changing file permissions
chmod 755 filename
```
**Flag**: 
```
pwn.college{FlRX4rZ_vx8cQcv7CEYjGNBkdfhD.dDZN4QDL3IjN0czW}
```

## Conclusion

Through this command line exploitation challenge, I have gained significant knowledge and practical skills in shell scripting and command line operations. Understanding variables, process management, file permissions, and command execution has equipped me to tackle real-world challenges in system administration and cybersecurity. This learning experience has reinforced my interest in exploring further into these topics and enhancing my technical capabilities.


