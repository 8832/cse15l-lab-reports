# Lab Report 1
By: Sara Standlee
## `cd` command
**Using `cd` command with no arguments:** \
The current working directory is /home. \
The cd command is used to change into directories, and the argument for this command is the directory we want to change into. In this case, we have given no directory to change into, so there is no output. 
```
[user@sahara ~]$ cd
[user@sahara ~]$
```

**Using `cd` command with a path to a directory as an argument:** \
The current working directory is /home. \
Now, let us change into the lecture1 directory. 
```
[user@sahara ~]$ cd lecture1/
[user@sahara ~/lecture1]$ 
```
Notice that there is no output. However, the terminal command prompt has changed to indicate that we are now in the lecture1 directory.


**Using `cd` command with a path to a file as an argument:** \
Using the command 'pdw' , we can observe that we are currently in the lecture1 directory. See below. 
```
[user@sahara ~/lecture1]$ pwd
/home/lecture1
```
Using the ls command, we can see the possible files and directories we can change into from the lecture1 directory. See below. 
```
[user@sahara ~/lecture1]$ ls
Hello.class  Hello.java  messages  README
```
Let us to try to use the `cd` command to change into the README file. See below. 
```
[user@sahara ~/lecture1]$ cd README
bash: cd: README: Not a directory
```
Since README is a file, and the `cd` command is used to change into directories, the output gives use the message that the file is not a directory.


## `ls` command
**Using `ls` command with no arguments:** \
The current working directory is /home. \
This command without an argument lists the files and directories available to access from the current working directory. Below, since we are in the home directory, we can see from the output that there is one directory listed. 
```
[user@sahara ~]$ ls
lecture1
```

**Using `ls` command with a path to a directory as an argument:** \
The current working directory is /home. \
Let us use the `ls` command with the lecture1 driectory as an argument. The output is the directories and files available from the lecture1 directory. 
```
[user@sahara ~]$ ls lecture1
Hello.class  Hello.java  messages  README
```

**Using `ls` command with a path to a file as an argument:** \
The current working directory is the home directory, and let us use the path to the README file. The output is the path to the file we gave as an argument. Since the argument is a file, there are no files or directories to list. 
```
[user@sahara ~]$ ls /home/lecture1/README
/home/lecture1/README
```

## `cat` command
**Using `cat` command with no arguments:** \
The current working directory is /home. \
The command `cat` is used to print the contents of one or more files gieven by the paths. When using the `cat` command without arguments in the terminal, no output is given but the terminal keeps running. This is an error. It is neccessary to force stop the terminal (ctrl+Z) in order to get back to the command line prompt.
```
[user@sahara ~]$ cat

```
**Using `cat` command with a path to a directory as an argument:** \
The current working directory is /home. \
The cat command is used to print the contents of *files*, not directory. Thus, when running this command with a directory argument, we get the output notifying us that our argument is a directory. See below. 
```
[user@sahara ~]$ cat lecture1/
cat: lecture1/: Is a directory
```

**Using `cat` command with a path to a file as an argument:** \
The current working directory is /home. \
The `cat` command prints the contents of the file that we give the path to. 
```
[user@sahara ~]$ cat /home/lecture1/messages/en-us.txt 
Hello World!
```
Also, notice that we do not always need to give the absolute file path. For example, if we want to access the same file text and our current working directory is the lecture1 directory, we only need to provide the path messages/en-us.txt.
```
[user@sahara ~/lecture1]$ cat messages/en-us.txt 
Hello World!
```


