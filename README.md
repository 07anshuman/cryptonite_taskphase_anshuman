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

## Conclusion

The first 6 modules of Linux Luminarium have been both challenging and rewarding. I’ve learned how to work with the command line more confidently, manipulate files, navigate directories, and master piping. I’m no longer scared of making mistakes (well, not as much), and I’m excited to keep hacking forward.

--- 

