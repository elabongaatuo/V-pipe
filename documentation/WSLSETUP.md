# Introduction

V-pipe is a bio-informatics pipeline built on top of the Snakemake workflow management system.
Bioconda is optimized for use on Unix and MacOS systems but does not have a Windows Channel. For that reason, WSL (Windows Subsystem for Linux) installation is advised.

This Markdown shares resources that makes installation easier and solutions for problems you may encounter when using WSL.

For this project setup , VSCode IDE was used.


## Installation Resources
1. How to [Setup WSL](https://learn.microsoft.com/en-gb/windows/wsl/install) on your windows device  
2. Install and configure [Anaconda](https://medium.com/@sawepeter6/conda-command-not-found-ac28bea24291)
3. [V-pipe](https://github.com/cbg-ethz/V-pipe/blob/master/docs/tutorial_0_install.md) setup tutorial  


> Handy tips - From step 2, aim to work in the 'home' directory of WSL to avoid errors as will be seen.

## Probable Errors & Their Solutions

### 1. Symbolic Links aka Symlinks
A symbolic link is a special type of file that acts like a shortcut to another file or directory.
A symbolic link directly or indirectly points back to itself, creating an infinite loop. The system gets stuck trying to follow the chain of links forever.
#### Error

```
CreateCondaEnvironmentException:
Could not create conda environment from 
 OSError: [Errno 40] Too many levels of symbolic links: '/mnt/c/Users/..'
```

#### Solution

Check your V-pipe working directory and move it from `mnt/c/Users/... ` (Windows) to `/home/projects...` (Linux) to resolve the *__"too many levels of symbolic links"__* error because of the inherent differences in how Windows and Linux handle file systems and symbolic links.

### 2. The Assertion Error

#### Error
```
AssertionError in file /home/user/v-pipe/vp-analysis/V-pipe/workflow/rules/common.smk, line 505:
ERROR: Line '1' does not contain at least two entries!
  File "/home/user/v-pipe/vp-analysis/V-pipe/workflow/Snakefile", line 12, in <module>
  File "/home/user/v-pipe/vp-analysis/V-pipe/workflow/rules/common.smk", line 505, in <module>
```


#### Solution

The pipeline expects at **minimum two tab seperated values in the samples.tsv**

(For VSCode IDE) - Check your Tab settings. For Python, it is important that the tab size is set to 4. Here is a useful [resource](https://araldhafeeri.medium.com/specify-indentation-tab-size-per-filetype-in-vs-code-91d95d51248a) to ensure that.

### 3. Locked directories 
#### Error

If maybe after running `./vpipe -p --cores 2 ` and for some reason, the set up doesnt complete after a few processes or encounter an error that halts the pipeline execution.

#### Solution
Snakemake by default prevents  production of the same output file, to continue working, 
Run `./vpipe -p --cores 2 --unlock` first then  `./vpipe -p --cores 2 ` again to resolve the issue.

### 4. Conda environment
#### Error

`Conda environment not activated`

#### Solution 

Ensure you have rightfully activated the Conda Environment as detailed [here.](https://medium.com/@sawepeter6/conda-command-not-found-ac28bea24291)




