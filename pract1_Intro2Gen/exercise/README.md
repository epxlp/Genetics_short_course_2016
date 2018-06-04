# Practical 1: Introduction to genetic data 
# Objectives
1.	Get familiar working in a Linux environment
2.	Learn some simple Linux commands
3.	View some genetic data
4.	Understand Plink file formats
5.	Compare ‘calls’ and ‘dosage’ formats

(OPTIONAL: understand SNPTEST file formats)


# Linux
Genetic epidemiologists tend to work in a Linux Environment for several reasons:

- File sizes are generally large and so more easily stored on a cluster rather than a personal machine. It also means in a department, only one copy of the data is needed for many researchers to work on. 

- Lot of genetic software has been written for the Linux environment.

- Using a cluster means you can run jobs in parallel (e.g. analyses for each chromosome can be run at the same time, on different nodes).

<br/>

# Logging on
On a windows machine, from `All Programs` launch the program `PuTTy`.

The Host Name is `bluecrystalp3.acrc.bris.ac.uk` Click `Open`

Type your `username` `{enter}` `password` `{enter}`

You should now see a command line that looks like: 	`[username@newblue2 ~]$`

  
 <br/>

# Navigating the directories
When you log onto bluecrystal you land in your home directory (shortcut '~'). You can find the full pathname of your current directory by using the following command:

`pwd`	This returns (prints) the current working directory (wd)

This directory should currently be empty. Check this with the following command:

`ls`	This lists the contents of the current directory.

The data necessary for this course is located here: /panfs/panasas01/sscm/shortcourse/genetic.epidemiology. You can change to this directory using the following command.

`cd /panfs/panasas01/sscm/shortcourse/genetic.epidemiology` This changes directory. 

Now use `pwd` and `ls` to see check you are and see what is there.

Now move into the data directory and see what files are there. 
Note you can use relative paths 
e.g. `cd pract1_Intro2gen` rather than `cd /panfs/panasas01/sscm/shortcourse/genetic.epidemiology/pract1_Intro2gen`
and `cd ..` is a shortcut for moving one level up the directory structure.
Have a play with these commands. Finish in the `pract1_Intro2gen/data` directory


# Exercise 1 - Viewing file contents
Because genetic data is often so big, we don’t typically ‘open’ a file in the same way you might with windows. Instead we tend to view a section of the file using the following commands:

`head {file}`	This shows the top 10 rows of a file

`tail {file}`	This shows the bottom 10 rows of a file

`less	{file}` 	Shows the first page. The option `–S` before `{file}` can be really useful. Typing `q` quits less.

Try these commands out on the files in the pract1_Intro2gen/data directory. 

**_Question:_**
> (1) When is `less –S {file}` a better command to use to have a quick look at a file?

Another useful command to get a feel for the contents of a file is:

`wc -l {file}`	This tells you the number of rows a file has.

# Exercise 2 - Exploring the genetic files
The basic Plink file format is two files: PED/MAP (see Plink website: https://www.cog-genomics.org/plink2)

Using the commands above get the answers to the following question:

**_Questions:_**
> (2) What do you think the 4 columns in a .map file are? (TIP: you can check on the file formats page on the plink website)

> (3) How many variants are there in this dataset?

> (4) How many individuals are there in this dataset?

> (5) How many columns are there in the .ped file before the genetic data columns? What might these be? (TIP: you can check on the file formats page on the plink website)

> (6) What are the 2 possible alleles for the first SNP in the dataset? What is the name of this SNP?


You can use `grep {string} {file}` to search for a string in a file.

**_Question:_**
> (7) Search for SNP rs7288409. What is the bp position for this SNP?


Plink also has another file format: BED/BIM/FAM

Here the same data is stored in binary format.

Explore the `.bed` `.bim` & `.fam` files and read about this format on the plink website.

**_Questions:_**
> (8) What is the difference between a .bim and a .map file?

> (9) What is the difference between a .fam and a .ped file?


So far all the data has been coded with the actual alleles. Often genetic data is coded as ‘dosage’. 

**_Question:_**
> (10) Above, you listed the possible alleles for rs5747968 (hopefully as G & T). If we were to represent the data as dosage of G, what would the dosages be for the first 8 people in the dataset?


Now check your answer, by opening the `chr22_dosage.txt file`, where the data has been recoded to dosage format. 

Dosage format will become much more relevant when you learn about imputation later in the course.

# EXTRA - SNPTEST format questions

If you think you might use SNPTEST (.gen .sample format) go to this website to read about file formats: stats.ox.ac.uk/~marchini/software/gwas/file_format.html

**_Questions:_**
> (11) What format are genotypes displayed in?

> (12) How can you tell which individual the first three columns of data in the .gen file belong to (how is this different to the Plink format)?

