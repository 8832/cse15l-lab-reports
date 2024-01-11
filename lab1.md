# Lab Report 1
## `cd` command
**Using `cd` command with no arguments:** \
Notice that this has no output. This command is used to change directories, and the argument is the directory to change into. In this case, we have give no directory to change into, so there is no output. 
```
[user@sahara ~]$ cd
[user@sahara ~]$
```

**Using `cd` command with a path to a directory as an argument:** \
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


**Using `cd` command with with a path to a file as an argument:** \
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
**Using `ls` command with no arguments:**
```
[user@sahara ~]$ ls
lecture1
```

**Using `ls` command with a path to a directory as an argument:**
```
[user@sahara ~]$ ls lecture1
Hello.class  Hello.java  messages  README
```

**Using `ls` command with with a path to a file as an argument:**
```
[user@sahara ~]$ ls lecture1/README 
lecture1/README
```

## `cat` command
**Using `cd` command with no arguments:**

**Using `cd` command with a path to a directory as an argument:**

**Using `cd` command with with a path to a file as an argument:**

