## More complex commands that will make life easier for text editing

We already learned about some useful commands previously. Just a recap:

```
$ pwd # prints working directory
$ ls # lists what is inside that directory
$ cd # change directory to home
$ mkdir folder # creates a directory with name folder
$ touch myFile.txt # creates an empty file named myFile.txt
$ nano myFile.txt # starts a text editor for you to read/write to myFile.txt
$ cp myFile.txt ../ # copies myFile.txt to an upper directory
$ mv myFile.txt myNewFile.txt # changes name of the file
$ mv myNewFile.txt ../ # moves the new file to upper directory
$ rm ../myFile.txt # removes the file in the upper directory
$ cd .. # cd to upper directory
$ head myNewFile.txt # shows the first 10 lines from that file
$ tail myNewFile.txt # shows the last 10 lines from that file
$ less myNewFile.txt # will show you contents of the file, quit by "q" on your keyboard
$ cat myNewFile.txt # prints the file on the shell and can be used to concatenate files
$ wc -l myNewFile.txt # prints number of lines on the file
$ cat file1 file2 > combined_file # concatenates file1 and file2 and writes them on a new file combined_file
$ cat file3 >> combined_file # adds file3 to the end of combined_file
```

Now we know the basics, we can move to more complex but super useful commands. Let's go!

We will be using a gff file to do some manipulations and extract useful information that we might need. This file can be found [here](https://github.com/melisound/trainings). Let's start first by examining this file.

```
$ less Araport11.gtf # examining the file
$ wc -l Araport11.gtf # gives you line numbers
$ uniq Araport11.gtf > Araport11_uniq.gtf # prints only the unique lines to the new file
$ wc -l Araport11_uniq.gtf
$ uniq -d Araport11.gtf # print repeated lines 
$ uniq -u Araport11.gtf | wc -l # only print unrepeated lines and pipe that to less to examine
```

Which brings us to a super useful command "pipe" or "|". This is where your backslash is on your keyboard. What is does is, it takes the output from a prevous command and feeds it into a new command. This is very useful to look at large files after you do a modification for example.

```
$ head -n 51 Araport11_uniq.gtf | tail -n 1 # this will print the 51st line on the file
$ uniq -u Araport11.gtf | less
```

Remember uniq only looks at adjacent lines, it is possible that this file had other duplicates but not in an ordered manner.

```
$ sort Araport11.gtf | uniq | wc -l # first sort the file, then find uniq lines and count them
```

Sort assumes a string not a number so for sort 11 comes before 2! If you want to do a numeric sort, do:

```
$ sort -n file.txt | less 
```

Let's say that you want to create a new file with the chr, start and end from the gtf file:

```
$ cut -f1,4,5 Araport11.gtf | less # we are cutting column 1, 4 and 5, but see they are not sorted and there are also non-unique lines there 
$ sort Araport11.gtf | uniq | cut -f1,4,5 | less # I always first examine new files by less before I write them to a new file
$ sort Araport11.gtf | uniq | cut -f1,4,5 > Araport11.bed
```
Oh but shoot, this bed file now also have all the info of exons, CDs etc on the bed file and I only want the gene information. We got you! 
grep (global regular expression print:
```
$ grep gene Araport11.gtf | less # well that did not work because gene is on other fields "gene_id"
$ grep "\tgene" Araport11.gtf | less # aha that worked! 
```
Here 2 important things to know:
  1. "\t" stands for tab in unix text language
  2. "\n" stands for new line
[Here](https://regexr.com/) info on regular expressions.
With grep you can also find on which line an exact word is:
```
$ grep -n "\tgene" Araport11.gtf | less
```
Let's say that you do not want to have Araport11 in this file and want to replace it with At_gene_model (remember no spaces!). sed (stream editor) comes to rescue, but be careful when using it. I only use sed in substitute mode:
```
$ sed 's/Araport11/At_gene_model/g' Araport11.gtf > Araport11_updated.gtf # this substitutes Araport11 with At_gene_model
$ sed 's/Chr//g' Araport11.gtf | less # this will remove Chr from the text
```
sed has many more functionalities, check the manual! I usually google what I want to do and add sed to the search phrase if I feel like it is something that I can do with sed.
```
$ man sed
```
awk is a similar tool, but some say more powerful. It kinda intimidates me so I try to solve issues with other commands but sometimes I give up and go to awk. awk will read your file line by line and perform a function, such as print, replace, edit. It works like this:
```
$ awk '{print}' Araport11.gtf | less # will print the whole thing, but now with less just exploring
$ awk '{print $1,$4,$5}' Araport11.gtf > Araport11.bed # oops it has spaces instead of tabs.
$ awk 'OFS="\t" {print $1,$4,$5}' Araport11.gtf > Araport11.bed # OFS=output field separator
```
The next useful thing we will learn about is "*". The star stands for Life, the universe and everything, meaning you can use it to replace any text pattern.

```
$ cp *.gtf ../ # this will cp all the files that has a gtf extention to the upper directory
$ rm ./* # this will delete all the documents in the current directory! BE CAREFUL!
```

