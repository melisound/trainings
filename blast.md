## Powerful blasting on the command line

Have you ever done blasts manually one by one on a website maybe for 10+ genes? You are now at the right place to do this with a single liner, ok well maybe 2 single liners.

# BLAST Command Line Applications installation

You can find the manual [here](https://www.ncbi.nlm.nih.gov/books/NBK279690/). Most software you use like BLAST also have command line interface applications with far more options. You can usually find info if you type name of the software and "command line" to get to where you can find information. From the manual go to installation and MacOSX or your operating system. There are several options here and we will continue with one of the hardest ways as most programs do not have user friendly options. Let's first download:

```
$ cd # go to your home directory
$ mkdir blast # make a directory for blast
$ curl https://ftp.ncbi.nlm.nih.gov/blast/executables/LATEST/ncbi-blast-2.13.0+-x64-macosx.tar.gz # this will probably not work, if not try the next
$ curl https://ftp.ncbi.nlm.nih.gov/blast/executables/LATEST/ncbi-blast-2.13.0+-x64-macosx.tar.gz --output ncbi-blast-2.13.0+-x64-macosx.tar.gz 
$ tar zxvpf ncbi-blast-2.13.0+-x64-macosx.tar.gz # getting the ingredients of the downloaded tarball
```

This should have created a folder called ncbi-blast-2.13.0+, which should include several other folders/files including the bin folder. Our executables are usually under bin for many software, so let's explore there:

```
$ cd ncbi-blast-2.13.0+
$ ls
$ cd bin
$ ls
```

The blast option we will use today is blastn and we can see it is in the folder. Let's try to run it to see if it works:

```
$ blastn # if this does not work try:
$ ./blastn # you sometimes have to indicate the folder with ".\"
```
Now if you go to another folder and type blastx, the command line will not know where to look for it and throw you an error:

```
$ cd ..
$ blastn
```

Alternatively we can add this to our PATH with:

```
$ echo $PATH
$ pwd
$ export PATH=$PATH:$PWD
```
# Sound Genome Repository

Now we have blast installed, let's see how we can make use of our genome repository. For this you either need to be on the network or use vpn for connecting to the servers. Open finder and Go>Connect to Server. Enter the IP address, then username and password. Now you should have access to the genome repo and everything inside. Today we will use tomato to do our blasts. 

# Creating a database

We already have a blast database here in the repo so we do not need to create one. But this is the code in case you need to create one:

```
$ cd 
$ cd /Volumes/Data/genomics/
$ ls
$ cd solanum_lycopersicum/microtom/ITAG4.0/
$ ls
$ makeblastdb -in ./ITAG4.0_CDS.fasta -dbtype nucl -parse_seqids -out ./blast_indices/ITAG4.0_CDS -logfile ./blast_indexes/ITAG4.0_CDS_Log.txt
$ cd
$ cd blast
$ mkdir results
$ cd results
$ blastn -help
```

# Running blast

It looks like we are ready to start doing some fancy blasting! Here is the  one-liner we need:

```

$ blastn -query /Volumes/Data/genomes/Solanum_lycopersicum/Reference/microtom/ITAG4.0/ITAG4.0_CDS.fasta -db /Volumes/Data/genomes/Solanum_lycopersicum/Reference/microtom/ITAG4.0/blast_indices/ITAG4.0_CDS -out microtom_CDs_to_CDs.txt -num_alignments 25 -outfmt "7 qseqid qlen sseqid slen qstart qend sstart send evalue bitscore score length pident nident mismatch positive gapopen gaps"
```
Now, if you have a gene that you would like to analyze further, you can have a look at all the blast results for that gene with:

```
$ grep Solyc01g017080 microtom_CDs_to_CDs.txt
```


