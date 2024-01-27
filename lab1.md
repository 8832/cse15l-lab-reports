# Lab Report 1
By: Sara Standlee
## `cd` command
**Using `cd` command with no arguments:** \
The cd command is used to change into directories, and the argument for this command is the directory we want to change into. When we do not give an argument, and the home environment variable is non-empty, the `cd` command operates as if the home environment was the specified directory we want to change into. In other words, when we use the `cd` command with no arguments, we will change into the home environment. If our current working directory is the home environment, then we will remain in the home environment. Below are some cases: \
*Case One:* Let's consider the case where our current working directory is the home directory:
```
[user@sahara ~]$ pwd
/home
```
Note that `pwd` is the command used to print the working directory. As we can see by the above code, the home directory is represented by the command line prompt `[user@sahara ~]$`. Thus, as we can see, we are currently in the home directory. Let us now use the `cd` command:
```
[user@sahara ~]$ cd
[user@sahara ~]$ 
```
Notice that in the case where the current working directory is the home directory, nothing happens. We remain in the home directory. Since we were already in the home environment, and the `cd` command without an argument will use the home directory as the argument, nothing happens, since we are 'changing' into the home directory, and were already in the home directory. \
*Case 2:* Let's consider the case when we are NOT in the home directory, but instead in a random directory:
```
[user@sahara ~/lecture1]$ pwd
/home/lecture1
```
As we can see by the `pwd` command, our current working directory is now the lecture1 directory. Let's now use the `cd` command with no arguments:
```
[user@sahara ~/lecture1]$ cd
[user@sahara ~]$
```
Notice the command line prompt has changed back to `[user@sahara ~]$`. This shows that we are now in the home directory. \
*Case 3*: Say we are in directory that is deeply nested: 
```
[user@sahara ~/lecture1/messages]$ pwd
/home/lecture1/messages
```
Now, let us use the `cd` command with no arguments.
```
[user@sahara ~/lecture1/messages]$ cd
[user@sahara ~]$
```
As we can see, we have returned to the home directory, as shown by the change in the command line prompt to `[user@sahara ~]$`. As shown above, this new command line prompt shows that we are in the home directory. 
*Case 4:* Suppose we are in the root directory.
```
[user@sahara /]$ pwd
/
```
As shown by the `pwd` command, our current working directory is now the root directory, which is shown by the `/`. Now, let us ise the `cd` command with no arguments:
```
[user@sahara /]$ cd
[user@sahara ~]$ 
```
Notice that we have changed into the home directory, as shown by the command line prompt `[user@sahara ~]$`. As shown above, this command line prompt shows that our current working directory is the home directory. \ 
To conclude, the `cd` command with no arguments will operate as if the home directory was the argument. We will change into the home directory no matter whether we are in a random directory, a deeply nested directory, the root directory, etc. \
This output is not an error. 
 
**Using `cd` command with a path to a directory as an argument:** \
The current working directory is /home. \
Now, let us change into the lecture1 directory. 
```
[user@sahara ~]$ cd lecture1/
[user@sahara ~/lecture1]$ 
```
Notice that there is no output. However, the terminal command prompt has changed to indicate that we are now in the lecture1 directory. \
This output is not an error. 


**Using `cd` command with a path to a file as an argument:** \
Using the command `pwd` , we can observe that we are currently in the lecture1 directory. See below. 
```
[user@sahara ~/lecture1]$ pwd
/home/lecture1
```
Using the ls command, we can see the possible files and directories we can change into from the lecture1 directory. See below. 
```
[user@sahara ~/lecture1]$ ls
Hello.class  Hello.java  messages  README
```
Let us try to use the `cd` command to change into the README file. See below. 
```
[user@sahara ~/lecture1]$ cd README
bash: cd: README: Not a directory
```
Since README is a file, and the `cd` command is used to change into directories, the output gives us the message that the file is not a directory.
This output is not an error. Instead, we get a message indicating that our argument needs to be a directory. 


## `ls` command
**Using `ls` command with no arguments:** \
The current working directory is /home. \
This command without an argument lists the files and directories available to access from the current working directory. Below, since we are in the home directory, we can see from the output that there is one directory listed. 
```
[user@sahara ~]$ ls
lecture1
```
This output is not an error. 


**Using `ls` command with a path to a directory as an argument:** \
The current working directory is /home. \
Let us use the `ls` command with the lecture1 directory as an argument. The output is the directories and files available directly from the lecture1 directory. 
```
[user@sahara ~]$ ls lecture1
Hello.class  Hello.java  messages  README
```
This output is not an error.\
**Using `ls` command with a path to a file as an argument:** \
The current working directory is the home directory, and let us use the path to the README file. The output is the path to the file we gave as an argument. Since the argument is a file, there are no files or directories to list. 
```
[user@sahara ~]$ ls /home/lecture1/README
/home/lecture1/README
```
This output is not an error. 

## `cat` command
**Using `cat` command with no arguments:** \
The current working directory is /home. \
The command `cat` is used to print the contents of one or more files given by the paths. When using the `cat` command without arguments in the terminal, no output is initially given but the terminal keeps running. The terminal will wait for input from the user. When you manually type text and hit enter, the text you type will be repeated back to you on the following line. You can press Ctrl+D to return to the command line prompt. The text displayed is the text you wrote with each line duplicated. 
```
[user@sahara ~]$ cat

```
This is not an error. 


**Using `cat` command with a path to a directory as an argument:** \
The current working directory is /home. \
The cat command is used to print the contents of *files*, not directories. Thus, when running this command with a directory argument, we get the output notifying us that our argument is a directory. See below. 
```
[user@sahara ~]$ cat lecture1/
cat: lecture1/: Is a directory
```
This output is not an error. 


**Using `cat` command with a path to a file as an argument:** \
The current working directory is /home. \
The `cat` command prints the contents of the file that we give the path to. In this case, we enter the path to the file en-us.txt, which contains the sentence "Hello World!". 
```
[user@sahara ~]$ cat /home/lecture1/messages/en-us.txt 
Hello World!
```
Also, notice that we do not always need to give the absolute file path. For example, if we want to access the same file text and our current working directory is the lecture1 directory, we only need to provide the path messages/en-us.txt.
```
[user@sahara ~/lecture1]$ cat messages/en-us.txt 
Hello World!
```
These outputs are not errors. 

