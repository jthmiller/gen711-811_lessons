---
title: "Lab 5"
author: "Jeffrey Miller"
date: "2026 Feb 20"
output: pdf_document
---

# Lab 5: Quality control of sequencing data

Start out in home directory and then navigate to the untrimmed_fastq directory where your FASTQ files are located.
```
cd ~/gen711-811/shell_data/untrimmed_fastq
```

Warm up: 
*Exercise: What is the last read in the SRR2584863_1.fastq file? How confident are you in this read?

# File permissions

Here the three positions that relate to the file owner are rw-. The r means that you have permission to read the file, the w indicates that you have permission to write to (i.e. make changes to) the file, and the third position is a -, indicating that you don't have permission to carry out the ability encoded by that space (this is the space where x or executable ability is stored, we'll talk more about this in a later lesson).

Our goal for now is to change permissions on this file so that you no longer have w or write permissions. We can do this using the chmod (change mode) command and subtracting (-) the write permission -w.

```
chmod -w SRR098026-backup.fastq
ls -l 
```
This shows that the permissions for the file have changed from rw- to r--, meaning that you can still read the file but you can no longer write to it. If you try to edit the file now, you will get a permission denied error.

To prove to ourselves that you no longer have the ability to modify this file, try deleting it with the rm command:

```
rm SRR098026-backup.fastq
```

You'll be asked if you want to override your file permissions:

You should enter n for no. If you enter n (for no), the file will not be deleted. If you enter y, you will delete the file. This gives us an extra measure of security, as there is one more step between us and deleting our data files.

Important: The rm command permanently removes the file. Be careful with this command. It doesn't just nicely put the files in the Trash. They're really gone.

By default, rm will not delete directories. You can tell rm to delete a directory using the -r (recursive) option. Let's delete the backup directory we just made.

Enter the following command:

```rm -r backup
``` 

rm -r will delete not only the directory, but all files within the directory. If you have write-protected files in the directory, you will be asked whether you want to override your permission settings.

Important: This cannot be undone.

rm -i will prompt you to confirm that you want to delete every file regardless of permission settings.

## DO EXERCISE 5.1

Make sure that you have deleted your backup directory and all files it contains.
Create a backup of each of your FASTQ files using cp.
Use a wildcard to move all of your backup files to a new backup directory.
Solution:
```
rm -r backup
cp SRR098026.fastq SRR098026-backup.fastq 
cp SRR097977.fastq SRR097977-backup.fastq
mkdir backup
mv *-backup.fastq backup
```

### DO EXERCISE 5.2
Change the permissions on all of your backup files to be write-protected.
```
chmod -w backup/*-backup.fastq
```
It's always a good idea to check your work with ls -l backup. You should see something like:
```
-r--r--r-- 1 dcuser dcuser 47552 Nov 15 23:06 SRR097977-backup.fastq
-r--r--r-- 1 dcuser dcuser 43332 Nov 15 23:06 SRR098026-backup.fastq
```


# Conda environments

Discuss conda environments. What is conda? What is a package manager? Demostrate that fastqc is not available in the base environment, and then activate the genomics environment and show that it is available there.

A package manager is a tool that automates the process of installing, updating, configuring, and removing software packages. It helps users manage software dependencies and ensures that the correct versions of packages are installed. Examples of package managers include pip for Python, npm for JavaScript, and conda for managing environments and packages across multiple programming languages.

A conda environment is an isolated directory on your computer that contains a specific collection of software packages, including their dependencies, libraries, and even different versions of programming languages like Python or R. 
This isolation is crucial for managing different projects that may require conflicting versions of the same library, ensuring that changes in one project do not affect

What is a dependency? A dependency is a software package that another software package relies on to function properly. For example, if you have a Python program that uses the NumPy library for numerical computations, then NumPy is a dependency of your program. If you try to run your program without having NumPy installed, it will not work correctly because it relies on the functions and features provided by NumPy.

What is Python? What is R? What is Bash?
Bash is a command-line shell and scripting language that is commonly used in Unix-based operating systems. It allows users to interact with the operating system, execute commands, and automate tasks through scripts.
Python and R are both high-level programming languages that are widely used in data science, bioinformatics, and other scientific computing fields. Python is known for its simplicity and readability, making it a popular choice for beginners and experienced programmers alike. R is particularly strong in statistical analysis and data visualization, making it a favorite among statisticians and data analysts.


```
conda activate /home/share/anaconda/envs/genomics
```

At this point, lets validate that all the relevant tools are installed. Test with 
```
fastqc -h
```

There is a lot of output here, but the important part is that it shows you the version of FastQC that is installed and the usage information. If you see this, then you know that FastQC is installed and ready to use.

We can check where the FastQC executable is located with:
```which fastqc
```     

FastQC can accept multiple file names as input, and on both zipped and unzipped files, so we can use the *.fastq* wildcard to run FastQC on all of the FASTQ files in this directory
```
fastqc *.fastq*
```

After that has finished, see the files and size:
```
ls -lh 
```

Lets organize these files a bit. Sep. the fastqc files from the data by making a directory and moving the fastq files into it. 
```
mkdir -p ~/dc_workshop/results/fastqc_untrimmed_reads
mv *.zip ~/dc_workshop/results/fastqc_untrimmed_reads/
mv *.html ~/dc_workshop/results/fastqc_untrimmed_reads/
```

lets head into the fastqc results folder and take a look into one of the summary files:
```
cd ~/dc_workshop/results/fastqc_untrimmed_reads/
```

The output files are zipped up. Lets see if we can unzip them with all in one command.
```
unzip *.zip
```

Then, we will use less to look a the summary
```
less SRR2584863_1_fastqc/summary.txt
```

Lastly, lets try to download one of those html files to our computer using vscode's remote explorer. Then, we can open it in our web browser and see the interactive report that FastQC generates.


Q: Which samples failed at least one of FastQC’s quality tests? What test(s) did those samples fail?
```
cat */summary.txt > ~/dc_workshop/docs/fastqc_summaries.txt
```

### Start this lesson
https://github.com/datacarpentry/shell-genomics/blob/main/episodes/04-redirection.md



