
## Learning basic command line tools to make our lives easier

# What is the command line?

The command line interface is a way to use your computer mostly without the GUI (graphical user interface- that enables you to work with your mouse or touchpad). We will be typing commands on the shell- a program that takes commands from the keyboard and feeds them to the operating system.

# Why is command line useful?

1. It opens up possibility of using many open source code/programs/scripts for data analysis.
2. It enables making manual tedious jobs to be automated.
3. It is a great tranferable skill to have in the age of big data.
4. It makes you understand your data, the data analyses processes better, which helps you troubleshoot more effectively.
5. It might be scary at first but it is a lot of fun!

# Basic commands

Incase you woke up confused that morning:

```
$ whoami
``` 

```
$ date
```

```
$ cal
```

```
$ man whoami
``` 
man = manual, is your friend!

# navigating on the shell, directory = folder
 ```
 $ pwd
 ``` 
 prints working directory, if you get lost use this command to navigate the maze.
 
 ```
 $ ls
 ``` 
 lists what is in this directory.
 
 ```
 $ ls -l
 ```
 lists what is in this directory in lines.
 
 ```
 $ ls -lh
 ```
 lists what is in this directory in lines with Human-readable format.
 
 ```
 $ ls -la
 ``` 
 lists what is in this directory in lines with hidden files.
 
 ```
 $ cd
 ``` 
 change directory: this one takes you to your home directory.
 
 ```
 $ cd ..
 ``` 
 change directory: this one takes you to one upper directory.
 
 ```
 $ cd ../.. # do not do this 
 ``` 
 change directory: this one takes you to two upper directory.
 
 ```
 $ cd directory_sub1
 ``` 
 change directory: this one takes you to a lower directory within the directory you are on.
 
 ```
 $ cd ..
 $ cd directory_sub1/directory_sub2
 ``` 
 change directory: this one takes you to a subdirectory within the directory you are on.
 
 ```
 $ cd
 ``` 
 let's move to home directory.
 
 ```
 $ mkdir cl_workshop
 ``` 
 make directory with the name cl_workshop.
 
 ```
 $ ls cl_workshop
 ```
 This will show you what is inside the directory.
 
Remember the command line does not like spaces, use underscores or dash instead
Trick of tab: Now let's start typing the below command "cd cl" and now press tab and you should see the directory name to be completed automatically. This can be very handy if you hate typing like me.
 
 ```
 $ cd cl_workshop
 ``` 
 now we are in our newly created folder.
 
 ```
 $ mkdir files
 ``` 
 we created a subfolder called files.

Another way to make these 2 directories is: 
 
 ```
 $ cd ..
 ```
 
 ```
 $ mkdir -p cl_worksop2/test
 ```
 
 ```
 $ cd cl_workshop
 ```

# to print something on your shell

```
$ echo 'Hello world!'
```

# writing on a text document

```
$ echo 'Hello world!' > hello.txt
``` 
">" automatically creates the file but beware if there is already a file with that name, it will be overwritten!

```
$ ls
```

# reading files

```
$ less hello.txt
``` 
this is one way of visualizing what is in that text document, to exit "less" press "q" on your keyboard for quit.

To add more text to the document:

```
$ echo 'Life is good!' >> hello.txt
```

```
$ less hello.txt
``` 
exit with q.

Now, let's create a txt file from scratch.

```
$ touch myFile.txt
```

```
$ ls
``` 
you can see a new file is created.

```
$ less myFile.txt
``` 
you can see it is empty, let's write somethings in the file now.

# writing into files

There are several ways to modify files. I sarted with nano but now use vi/vim only. Nano is a bit more intuitive, but I find vi to be more capable. But to make it simpler for now let's try nano:

```
$ nano myFile.txt
``` 

```
$ vi myFile.txt
``` 
with nano you can start typing right away, and you have the options at the bottom to choose from. ^ means ctrl in this case.

Now you have written some words in there, let's now learn about some other functions.

# copying, moving, deleting files

```
$ cp myFile.txt ../
``` 
this will create a copy of this file in the upper directory.

```
$ ls
```

```
$ cd ..
```

```
$ ls
```

```
$ mv myFile.txt ../
``` 
this will move the file to an upper directory.

```
$ cd ..
```

```
$ ls
```

```
$ rm myFile.txt
``` 
this is for remove. You just deleted the file and remember to be careful with rm because there is no going back.

Remember that directory we created a few steps back, let's delete that.

```
$ ls
```

```
$ rm -r cl_workshop2
``` 
with -r you can delete entire directories, again do this with caution.

```
$ cd cl_workshop
```

# other ways to visualize text files that can come handy:

```
$ head  myFile.txt
``` 
will print top 10 lines from this file.

```
$ head -n 3 myFile.txt
``` 
will print first 3 lines.

```
$ tail -n 1 myFile.txt
``` 
likewise print last line of the file.

```
$ cat myFile.txt
``` 
will print what is inside the file on your command line, it stands for concatenate.

```
$ echo 'somewords on the second file' > myFile2.txt
```

```
$ cat myfile.txt myFile2.txt > combinedFile.txt
``` 
now you combined the 2 files into 1.

```
$ wc -l myFile.txt
``` 
will print the number of lines in this file.


Let's leave some more complex commands for next time. These are: grep, sed, pipe (|), and wild cards (*), uniq, sort, awk...






