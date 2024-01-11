# Lab Report 1
## `cd` command
1. **Using `cd` command with no arguments:** \
The cd command is used to change into directories, and the argument for this command is the directory we want to change into. In this case, we have give no directory to change into, so there is no output. 
```
[user@sahara ~]$ cd
[user@sahara ~]$
```

2. **Using `cd` command with a path to a directory as an argument:** \
For context, using the command `pdw`, we see that we are currently in the home directory. See below. 
```
[user@sahara ~]$ pwd
/home
```
Now, we are going to change into the lecture1 directory. See below.
```
[user@sahara ~]$ cd lecture1/
[user@sahara ~/lecture1]$ 
```
Notice that there is no output. However, the terminal command prompt has changed to indicate that we are now in the lecture1 directory.


3. **Using `cd` command with with a path to a file as an argument:** \
Again, we are going to use the command 'pdw' to observe that we are currently in the lecture1 directory. See below. 
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
Since README is a file, and the `cd` command is used to change into directories, we receive the message that the file is not a directory.


## `ls` command
1. **Using `ls` command with no arguments:** \
This command without an argument lists the files and directories available to access from the current working directory. Below, we are in the home directory, and using the `ls` command, we can see from the output that there is one directory listed. 
```
[user@sahara ~]$ ls
lecture1
```

2. **Using `ls` command with a path to a directory as an argument:** \
Currently in the home directory, let us use the `ls` command with the lecture1 driectory as an argument. The output is the directories and files available from the lecture1 directory. 
```
[user@sahara ~]$ ls lecture1
Hello.class  Hello.java  messages  README
```

3. **Using `ls` command with with a path to a file as an argument:** \
The current working directory is the home directory, and let us use the path to the README file. The output is the path to the file we gave as an argument. Since the argument is a file, there are no files or directories to list. 
```
[user@sahara ~]$ ls /home/lecture1/README
/home/lecture1/README
```

## `cat` command
**Using `cd` command with no arguments:**

**Using `cd` command with a path to a directory as an argument:**

**Using `cd` command with with a path to a file as an argument:**

