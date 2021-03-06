# Introductory Version Control with Git
Marian L. Schmidt, @micro_marian, marschmi@umich.edu  
February 2nd, 2017  

#### Do you have ...  
1. <a href="https://www.rstudio.com/products/rstudio/download/" target="_blank">RStudio?</a>  
2. <a href="http://www.inside-r.org/download" target="_blank">R?</a>  
    + Please install these packages:  
        + `install.packages("knitr")`  
        + `install.packages("rmarkdown")`  
        + `install.packages("ggplot2")` 
3. A <a href="https://github.com/" target="_blank">Github</a> account?  
4. <a href="https://git-scm.com/book/en/v2/Getting-Started-Installing-Git" target="_blank">Git?</a>  



# **Agenda**  

1. What is **robust and reproducible research**?  
2. How can you make **your research** more **robust and reproducible**?  
3. How to use version control with **git**  
4. How to use RMarkdown and why it may change your workflow.

# **Learning Goals**  
1. Walk away knowing what **robust and reproducible research** are.  
2. To know the changes you can make to your research to make it more **robust and reproducible.**  
3. To understand how to keep track of different versions of your work locally and remotely with **git** and **GitHub.**
4. To know how to create an RMarkdown document and understand it's uses for code sharing. 

***

## Resources used to build this lesson
- Vince Buffalo's <a href="http://www.amazon.com/Bioinformatics-Data-Skills-Reproducible-Research/dp/1449367372" target="_blank">Bioinformatics Data Skills</a> book and it's helpful <a href="https://github.com/vsbuffalo/bds-files" target="_blank">github page.</a>
    + Main source for this presentation.
- A course by Karl Broman at the University of Wisconsin-Madison on <a href="http://kbroman.org/Tools4RR/" target="_blank">Reproducible Research.</a>  
- <a href="http://journals.plos.org/plosbiology/article?id=10.1371/journal.pbio.1001745" target="_blank">Best Practices for Scientific Computing</a> by Wilson et al., 2014.


*This tutorial was originally constructed as a part of Titus Brown's Next Generation Sequencing Data Analysis Workshop Week 3 that took place at Michigan State University's Kellogg Biological Station between August 24-28, 2015.*  

- Titus Brown's <a href="https://github.com/ngs-docs/angus" target="_blank">NGS Course</a>  
    + <a href="http://angus.readthedocs.org/en/2015/week3.html" target="_blank">Schedule of the NGS Course Week 3</a>  
    + A <a href="http://ivory.idyll.org/blog/tag/ngs-course.html" target="_blank">blog post from Titus</a> synthesizing the third week of the course.  
- Github for <a href="https://github.com/marschmi/NGS2015_RMarkdown_Reproducibility" target="_blank">this website</a>  

- The main page for the core lessons from the Software Carpentry Foundation can be found at <a href="http://software-carpentry.org/lessons/" target="_blank">http://software-carpentry.org/lessons/</a>.  
    + The `git` lesson here is heavily based on Software Carpentry's core curriculum on git entitled **"Version Control with Git"** and is maintained by Ivan Gonzalez and Daisie Huang.  
    + The main lesson link can be found at <a href="http://swcarpentry.github.io//git-novice/" target="_blank">http://swcarpentry.github.io//git-novice/</a>   



# We scientists have a few problems  
- The <a href="http://fivethirtyeight.com/datalab/as-a-major-retraction-shows-were-all-vulnerable-to-faked-data/" target="_blank">LaCour Scandal</a> of fabricated data published in *Science*.  
- Scientists in the United States spend <a href="http://journals.plos.org/plosbiology/article?id=10.1371/journal.pbio.1002165" target="_blank">$28 billion</a> each year on basic biomedical research that cannot be repeated successfully  
- A reproducibility study in psychology found that only <a href="http://www.nature.com/news/first-results-from-psychology-s-largest-reproducibility-test-1.17433" target="_blank">39 of 100 studies could be reproduced.</a>  
    + A quote: *“A lot of working scientists assume that if it’s published, it’s right... This makes it hard to dismiss that there are still a lot of false positives in the literature.”*  
    + <a href="http://www.theatlantic.com/health/archive/2015/08/psychology-studies-reliability-reproducability-nosek/402466/" target="_blank">An Atlantic Article by Ed Yong summarizing the project</a>  
- The Journal *Nature* on the <a href="http://www.nature.com/news/reproducibility-1.17552#/" target="_blank">issue of reproducibility</a>  
    + A comment from the journal *Nature*: "Nature and the Nature research journals will introduce editorial measures to address the problem by improving the consistency and quality of reporting in life-sciences articles... **we will give more space to methods sections. We will examine statistics more closely and encourage authors to be transparent, for example by including their raw data.**"  
    + Nature also released a <a href="http://www.nature.com/authors/policies/checklist.pdf" target="_blank">checklist</a> with an albeit *wimpy* computational check *(see #18)*. *This talk will help us **improve** this step.*  
    + In May 2016, Nature <a href="http://www.nature.com/news/1-500-scientists-lift-the-lid-on-reproducibility-1.19970" target="_blank">surveyed 1,500 scientists</a>  on their thoughts on reproducibility.  
- The Economist in 2013 published on <a href="http://www.economist.com/news/briefing/21588057-scientists-think-science-self-correcting-alarming-degree-it-not-trouble" target="_blank">Trouble at the lab</a>



# How to replicate this figure?
![](Figures/log2_dna_rna_phylum.png)


## Could I replicate *your* Figure 1?  
Could I replicate your Figure 1 from your last publication, grant proposal, or presentation?  

If not, what would **you and your co-authors** need to provide/do so **I** could replicate your figure 1?


# Our Goal: **Robust** and **Reproducible** research

## Robust Research   

"**Robust research** is about doing small things that stack the deck in your favor to prevent mistakes." *~Vince Buffalo*  

**Robust:** strong and healthy; vigorous (*adjective*)  

How can we make our research strong, healthy and vigorous?  

  - Prevent mistakes  
  - Make sure we test our models under various conditions to check that we obtain the same result 

##  Reproducible Research

**Reproduce:** produce again (*verb*)

**Reproducible:** able to be reproduced or copied (*adjective*)  

So, reproducible research may be repeated by other researchers with the same results. 

### The difficulty with genomic data.  
1. Genomics data is too large and high dimensional to easily inspect or visualize.  Usually, workflows involve multiple steps and it's not feasible to inspect every step.  
2. Unlike in the wet lab, we don't always know what to expect of our genomics data analysis.  
3. It's difficult to distinguish *good* from *bad* results.  
4. Scientific code is usually only run once to generate results for a publication, and is therefore more likely to contain (silent) bugs.  
    + **Silent errors** arise from code that may produce unknowingly incorrect output (rather than stop with an error message).


### What are the ingredients to robust and reproducible research?  

- **Work must be well documented!  Methods, code, and data must be made available to others!**  
- Adopt a cautious attitude and *check everything*.    
    + Vince Buffalo's golden rule of bioinformatics:  "Never ever trust your tools (or data)"  
    + "Garbage in, garbage out" - an analysis is only as good as the data going in.  
    + Let the data prove that it is high quality.
- **Take the time to develop fequently used scripts into tools.**  
    + Then have your lab mates or collaborators test them and try to break them.  
- **Collaborate!**  
    + Do paired-programming with your labmates and collaborators.  
    + Hack-a-thons! 



### What's the benefit for **_you?_**  
It takes a lot of effort to be robust and reproducible.  However, *it will make your life (and science) easier!*  

- Most likely, you will have to re-run your analysis more than once.  
- In the future, you or a collaborator may have to re-visit part of the project.  
- You can make modularized parts of the project into re-useable tools for the future.  
- Reproducibility makes you easier to work and collaborate with.  


***

# 5 Steps for Robust Research  

1. Write code for humans, write data for computers 
2. Make incremental changes.
3. Make assertions and be loud, in code and in your methods  
4. Use existing libraries (packages) whenever possible  
5. Prevent catastrophe and help reproducibility by making your data **read-only** 


## 1a. Write code for humans

**Code readability is very important.**  

- Code should be broken down into small chunks that may be re-used.  
    + Do not re-write code to do the same task over and over again.  
        + Do not repeat yourself!  (Who wants to read that?)  
            + If you need to, make it a tool/function.  
- Do not require readers to have to think of multiple facts at once.  
- Make names/variables consistent, distinctive and meaningful.  
- Adopt a <a href="http://adv-r.had.co.nz/Style.html" target="_blank">style</a> and format and keep it consistent.  
- Be a concise and clear commenter.  
    
If your code is more readable, then:  

- Your project is more reproducible.  
- It's easier to find and correct bugs.  
- You will be your friend in the future when you revisit the code.


## 1b. Write data for computers

**Let your computer do the work for you**  
Format your data so its easily read by your computer, not by you or other humans.  

- Code written for people to read requires cleaning and tidying to be processed by a computer.  
- Name data files in a consistent way.  
    + Automating tasks will be easier, which will prevent you from making trivial mistakes.

## 2. Make incremental changes.  
- Work in small steps with frequent feedback.  
    + Have a friend or labmate test your code and try to break it.  
    + Challenge your PI to test your code!
- Use version control!  
- Put all manual changes under version control, too! 


## 3. Be a "Defensive Programmer" - Make Assertions  
Add tests within your code to make sure your code is doing what it is supposed to do.  

Assertions are statments that something holds true.  Assertions:  
1. Ensure that if something goes wrong, the program will stop.  
2. They also explain what the program is doing.

- In R you can use `stopifnot()`  
    + The `testthat` package is made for this!  Check it out the <a href="http://journal.r-project.org/archive/2011-1/RJournal_2011-1_Wickham.pdf" target="_blank">testthat package here</a>  
- In python you can use `assert()`

## 4. Use existing libraries (packages) whenever possible  
- Do not try to re-invent the wheel while your performing your data anaylsis.  
- Use functions that have already been written and tested for you.

## 5. Prevent catastrophe and help reproducibility by making your data **read-only**
Read-only is important because:  

- Modifying data can corrupt your results.    
- It's easy to lose track of how you have changed a file when you modify it in place.  


***

# 6 Steps for reproducible research  

1. Encapsulate the full project into one directory that is supported with version control.  
2. Release your code and data.  
3. Document everything and use code as documentation!
4. Make figures, tables, and statistics the results of scripts.  
5. Write code that uses relative paths.  
6. Always set your seed.  


## 1. Encapsulate the full project into one directory that is supported with version control.  
The **Reproducible-Science-Curriculum** <a href="https://github.com/Reproducible-Science-Curriculum/rr-init" target="_blank">Github repo for Reproducible Research Project Initialization</a> is a great place to start a reproducible research project.  

## 2. Release your code and data
It is simple.  Without your code and data, your research is not reproducible.

## 3. Document everything!   
**Bottom line:  Adopt a computing notebook that is as good as a wet-lab notebook**.

To fully reproduce a study, each step of analysis must be described in much more detail than can be included in a publication.

Include a record of your steps, where files are, where they came from, and what they contain.  

Include `session_info()` in your document, preferably at the bottom. Session info lists the version of R that you’re using plus all of the packages you’ve loaded. 

## In your computing notebook:  

- Document your methods and workflows  
- Document the origin of all data in your project directory  
- Document **when** and **how** you downloaded the data  
- Record **data** version info   
- Record **software** version info with `session_info()`

For example, all the above information could be stored in a *README* file 


## 4. Make figures, tables, and statistics the results of scripts.

Using `inline code` can make the creation of tables much easier if the data changes!

## 5. Write code that uses relative paths.

Do not rely on hard-coded absolute paths (i.e. /Users/marschmi/Data/seq-data.csv or even ~/Data/seq-data.csv).  

Relative paths (i.e. Data/seq-data.csv) or command line arguments are better alternatives.

## 6. Always Set your seed  

If there is any randomizations of data or simulations, use `set.seed()` in the first code chunk.

<a href="http://kbroman.org/knitr_knutshell/pages/reproducible.html" target="_blank">Karl Broman</a> suggests to open R and type runif(1, 0, 10^8) and then paste the resulting large number into `set.seed()` in the first code chunk. If you do this, then the random aspects of your analysis should be repeated the same way.




***

#### How can you revise your work flow?  

> 1. How do you currently keep track of versions of the same document for **(1) data analysis** and **(2) writing a paper/grant proposal**?  
> 2. When working with a collaborator simultaneously, how do you keep track of versions of the same document?

***


# A scenario  
Months ago, you submitted a scientific paper to a journal for publication and you’ve finally received your reviews back. The reviewers give your paper *minor revisions* and suggest that you **modify one of the first steps** in your data analysis and therefore re-create **every figure.** 

The deadline for the reviews is quickly approaching and you do not have much time.  How do you stack the cards in your favor?



# Why version control?

1. **Nothing that is committed to version control is ever lost.** Since all old versions of files are saved, it’s always possible to go back in time to see exactly who wrote what on a particular day, or what version of a program was used to generate a particular set of results. 

#### This prevented me from losing my analysis two separate times when my computer crashed!

2. As we have this record of who made what changes when, **we know who to ask if we have questions later on**, and, if needed it, **revert to a previous version,** much like the “undo” feature in an editor.  
3. When several people collaborate in the same project, it’s possible to accidentally overlook or overwrite someone’s changes: **the version control system automatically notifies users whenever there’s a conflict between one person’s work and another’s.**

Teams are not the only ones to benefit from version control: **lone researchers can benefit immensely**. Keeping a record of what was changed, when, and why is extremely useful for all researchers if they ever need to come back to the project later on (e.g., a year later, when memory has faded).  

**Do you want to be your own friend in a year?**

Version control is the lab notebook of the digital world: it’s what professionals use to keep track of what they’ve done and to collaborate with other people. Every large software development project relies on it, and most programmers use it for their small jobs as well. And it isn’t just for software: books, papers, small data sets, and anything that changes over time or needs to be shared can and should be stored in a version control system


Examples from my own research: <a href="https://github.com/marschmi" target="_blank">https://github.com/marschmi</a>  

- A <a href="https://twitter.com/micro_marian/status/674294091300134912" target="_blank">victory tweet</a> from my first dissertation chapter. 


> Go to the original Software Carpentry lesson on **automated version control**: <a href="http://swcarpentry.github.io/git-novice/01-basics/" target="_blank">http://swcarpentry.github.io/git-novice/01-basics/</a>  



# Configuring Git  

> **Open up the unix shell, what happens when you run:**  
> 1. `git config --list`  
> 2. `git config`

> Now, let's set up Git by going to <a href="http://swcarpentry.github.io/git-novice/02-setup/" target="_blank">http://swcarpentry.github.io/git-novice/02-setup/</a>


# Create a Local Repository

**Learning Goals**  

- What is a **local** repository?  
- Create a local **Git** repository.  
- Check the status of a repository.


A **local** repository means that we are creating respository on our own computer.  Our computer is local - It especially likes attending the weekly farmers market and supporting local businesses.  

> 1. In the shell, navigate to your **home directory** and create a new directory called `git_repos`.
> 2. `cd` into the `git_repos` folder.  
> 3. In the **`git_repos`** folder, make another new directory called `earth_523`.  
> 4. `cd` into `earth_523`.  
> 5. Type `ls -aF`.  
> 6. What files do you see?
> 7. Now, **initialize the repository** by typing `git init`.  
> 8. What files do you see now that **`earth_523`** is a repository under version control?  
> 9. To check that everything is set up correctly by asking git to tell us the status of our project, type `git status`.  


# Tracking Changes  

**Learning Goals**  

- Go through the modify-add-commit cycle for single and multiple files.  
- Explain where information is stored at each stage of Git commit workflow.


> 1. `nano README.md` (or `notepadd README.md` or `npp README.md`)  
> 2. Write down the author, date  
> 3. Click <a href="https://en.support.wordpress.com/markdown-quick-reference/" target="_blank">here</a> for help with markdown language syntax.  
> 4. `git status`  

So far the changes are "untracked" with git.  Now we need to tell git to keep track of the changes we have made - in other words, it's time for the first add and commit!

> 5. `git add README.md`  

Git insists that we add files to the set we want to commit before actually committing anything because **we may not want to commit everything at once**. For example, suppose we’re adding a few citations to our supervisor’s work to our thesis. We might want to commit those additions, and the corresponding addition to the bibliography, but not commit the work we’re doing on the conclusion (which we haven’t finished yet).

To allow for this, Git has a special **staging area** where it keeps track of things that have been added to the current change set but not yet committed.

## **The Staging area**  
If you think of Git as taking snapshots of changes over the life of a project:  

- `git add` specifies what will go in a snapshot (putting things in the staging area), and  
- `git commit` then actually takes the snapshot, and makes a permanent record of it (as a commit).  

If you don’t have anything staged when you type `git commit`, git will prompt you to use `git commit -a` or `git commit --all`, which is kind of like gathering everyone for the picture! However, it’s almost always better to explicitly add things to the staging area, because you might commit changes you forgot you made. (Going back to snapshots, you might get the extra with incomplete makeup walking on the stage for the snapshot because you used `-a`!) Try to stage things manually, or you might find yourself searching for `git undo commit` more than you would like!

![](Figures/staging_area.png)


Let’s watch as our changes to a file move from our editor to the staging area and into long-term storage.



> 6. `git status`  

Git now knows that it’s supposed to keep track of `README.md`, but it hasn’t recorded these changes as a commit yet. To get it to do that, we need to run one more command:

> 7. `git commit -m "Created README.md to keep track of documentation of this repository."`  

When we run `git commit`, Git takes everything we have told it to save by using `git add` and stores a copy permanently inside the special **.git** directory. This permanent copy is called a commit (or revision) and its short identifier is `f22b25e` (Your commit will have another unique identifier.)

We use the `-m` flag (for “message”) to record a short, descriptive, and specific comment that will help us remember later on what we did and why. If we just run `git commit` without the `-m` option, Git will launch nano (or whatever other editor we configured as core.editor) so that we can write a longer message.

Good commit messages start with a brief (<50 characters) summary of changes made in the commit. If you want to go into more detail, add a blank line between the summary line and your additional notes.

![](Figures/xkcd_gitcommit.png)

If we run git status now:

> 8. `git status`.  Now, git tells us everything is up to date.  
> 9. Open the readme and write down the purpose of this repository  
> 10. `git status`

> 11. `git diff`:  This shows us the differences between the current state of the file and the most recently saved version:

The output is cryptic because it is actually a series of commands for tools like editors and patch telling them how to reconstruct one file given the other. If we break it down into pieces:

1. The first line tells us that git is producing output similar to the Unix diff command comparing the old and new versions of the file.  

2. The second line tells exactly which versions of the file git is comparing; df0654a and 315bf3a are unique computer-generated labels for those versions.  

3. The third and fourth lines once again show the name of the file being changed.  

4. The remaining lines are the most interesting, they show us the actual differences and the lines on which they occur. In particular, the + markers in the first column show where we have added lines.  

After reviewing our change, it’s time to commit it:  

> 12. `git add`  
> 13. `git status`  
> 14. `git commit -m "Added purpose of this repo to readme file"`  
> 15. `git status`  

> 16. If we want to know what we’ve done recently, we can ask git to show us the project’s history using `git log``  

`git log`  lists all commits made to a repository in reverse chronological order. The listing for each commit includes the commit’s full identifier (which starts with the same characters as the short identifier printed by the git commit command earlier), the commit’s author, when it was created, and the log message Git was given when the commit was created.


> 17.  Make another change and go through: 

a. `git add`  
b. `git status`  
c. `git commit -m "your message"`  
d. `git status`  




To recap, when we want to add changes to our repository, we first need to add the changed files to the staging area (git add) and then commit the staged changes to the repository (git commit):  

![](Figures/git_workflow.png)

> 18. `git remote -v`  
> 19. Does anything happen?



# Remote Repositories on GitHub  

**Learning Goals**  

- Explain what **remote** repositories are and why they are useful.  
- Clone a remote repository.  
- Push to or pull from a remote repository.  


Version control really comes into its own when we begin to collaborate with other people. We already have most of the machinery we need to do this; the only thing missing is to copy changes from one repository to another.

Systems like Git allow us to move work between any two repositories. In practice, though, it’s easiest to use one copy as a central hub, and to keep it on the web rather than on someone’s laptop. Most programmers use hosting services like GitHub, BitBucket or GitLab.

Let’s start by sharing the changes we’ve made to our current project with the world.  

> 1. Log in to GitHub.  
> 2. Click on "Repositories", and then click on the ![](Figures/new.png) icon in the top right corner to create a new repository called `earth_523` (**Note**: This name should be the same exact name as the folder on your computer):  

![](Figures/remote_repo.png)

As soon as the repository is created, GitHub displays a page with a URL and some information on how to configure your local repository:

![](Figures/remote_created.png)

This effectively does the following on GitHub’s servers:

`mkdir earth_523`  
`cd earth_523`  
`git init`


Our local repository still contains our earlier work on `README.md`, but the remote repository on GitHub doesn’t contain any files yet:

![](Figures/local_vs_remote.png)


The next step is to connect the two repositories. We do this by making the GitHub repository a remote for the local repository. The home page of the repository on GitHub includes the string we need to identify it:



> 4. Click on the ‘HTTPS’ link to change the protocol from SSH to HTTPS.



> **HTTPS vs SSH**  
> We use HTTPS here because it does not require additional configuration. After the workshop you may want to set up SSH access, which is a bit more secure, by following the great tutorial from <a href="https://help.github.com/articles/generating-ssh-keys/" target="_blank">GitHub</a>.





> 5. Copy that **HTTPS** URL from the browser, go into the local `SWC_R` repository.  
> 6. Run this command: `git remote add origin https://github.com/marschmi/earth_523.git`  

Make sure to use the URL for your repository rather than marschmi’s.

We can check that the command has worked by running `git remote -v:`

> 7. `git remote -v`  

The name `origin` is a local nickname for your remote repository: we could use something else if we wanted to, but `origin` is by far the most common choice.

Once the nickname `origin` is set up, this command will push the changes from our local repository to the repository on GitHub:

> 8. `git push -u origin master`  

- `origin`: a remote name of the repo  
- `master`: a branch name


***  

**Proxy**  
If the network you are connected to uses a proxy there is an chance that your last command failed with “Could not resolve hostname” as the error message. To solve this issue you need to tell Git about the proxy:

`git config --global http.proxy http://user:password@proxy.url`  
`git config --global https.proxy http://user:password@proxy.url`  

When you connect to another network that doesn’t use a proxy you will need to tell Git to disable the proxy using:

`git config --global --unset http.proxy`  
`git config --global --unset https.proxy`  

**Password Managers**  
If your operating system has a password manager configured, git push will try to use it when it needs your username and password. If you want to type your username and password at the terminal instead of using a password manager, type:

`unset SSH_ASKPASS`  

You may want to add this command at the end of your ~/.bashrc to make it the default behavior.

***

Our local and remote repositories are now in this state:

![](Figures/current_repo.png) 


We can pull changes from the remote repository to the local one as well:

> 9. `git pull origin master`

Pulling has no effect in this case because the two repositories are already synchronized. If someone else had pushed some changes to the repository on GitHub, though, this command would download them to our local repository.



# Git:  Key Words
A helpful resource describing version control with git basics from Software Carpentry <a href="http://swcarpentry.github.io//git-novice/reference.html#version-control" target="_blank">can be found here.</a>  

- **Version Control**  
- **Repository**  
  - **Local** vs **Remote**
- **Commit**  
- **Merge**  
- **origin**: a local nickname for your remote repository
- **master**: a nickname for your local repository
- `git config`  
- `git status`  
- `git add`  
- `git commit`  
- `git log`  
- `git diff`:  Allows us to look at older versions of the file compared to the current (non-staged) version of the file  
    - `git diff HEAD~2 filename.R`: Takes us back 2 versions ago
- `git push`:  Push changes from the local repository up to the remote repository.  
- `git pull`: Pull changes from the remote repository down to the local repository.

When adding a local to a new remote repo:
- `git remote add origin  ___(url)___`
- `git remote -v`: to check if the URL is correct
- `git push -u origin master`



# RMarkdown within RStudio  

# RMarkdown 
    
    
## What is R Markdown?   
* RMarkdown is a variant of Markdown that has embedded R code chunks to be used with `knitr` to make it easy to create reproducible web-based reports.  
      + **Markdown:**  A system for writing simple, readable text that is easily converted to html. 
          + Allows you to write using an easy-to-read, easy-to-write plain text format.              
*  Rmd -> md -> html (docx, pdf)  
*  Can include both text and code to execute  
      
    
## Why R Markdown?
A convenient tool for reproducible and dynamic reports with R!       

- Execute code with `knitr`.   
- Easy to learn syntax.  
- Include LaTeX equations.  
- Don't need to worry about page breaks or figure placement.  
- Consolidate your code and write up into a single file:  
    + Slideshows, pdfs, html documents, word files  
- It's **so easy** to use with version control with Git!   

## Simple Workflow

![](Figures/rmd_workflow.jpeg)


### How to Open an Rmd File
![](Figures/new.jpeg)  

![](Figures/newRMD.jpeg)



#### Choose Output
**YAML Header:**  A set of key value pairs at the start of your file.  Begin and end the header with a line of three dashes (- - -)

***R Studio template writes the YAML header for you***  

output: html_document  
output: pdf_document  
output: word_document  
output: beamer_presentation (beamer slideshow - pdf)  
output: ioslides_presentation (ioslides presentation - html)  

**For example:**  Here's the YAML header for this webpage with a table of contents.
```
---
title: "Introductory Version Control with Git"
subtitle: "Earth 523 - Metagenomics"
author: "Marian L. Schmidt, @micro_marian, marschmi@umich.edu"
date: "February 2nd, 2017"
output:
  html_document:
    code_folding: show
    highlight: haddock
    keep_md: yes
    theme: united
    toc: yes
    toc_float:
      collapsed: no
      smooth_scroll: yes
      toc_depth: 2
---
```

#### Markdown basics 
Markdown is a simple formatting language that is easy to use

- Create lists with `*` or `+` sign   
      + like this
      + and this  
      + **A very important note:**  The end of a line is marked by two spaces and an enter!!  Otherwise your list will look ugly like the one below: 
- Use one or two asterisk marks to provide emphasis such as `*`*italics*`*` and `**`**bold**`**`.  Can even include tables:    

First Header  | Second Header
------------- | -------------
Content Cell  | Content Cell
Content Cell  | Content Cell


## Helpful Cheatsheets  

Go to `Help` --> "Cheatsheets"  


# R Code Chunks 

```
Code blocks display with fixed-width font
```


```r
#quick summary
library(ggplot2)
min(diamonds$price)
```

```
## [1] 326
```

```r
mean(diamonds$price)
```

```
## [1] 3932.8
```

```r
max(diamonds$price)
```

```
## [1] 18823
```


#### More R Code Chunks 
![](Figures/chunk_example.jpeg)


+ You can name the code chunk.  

+ echo = TRUE:  The code **will** be displayed.   

+ eval = TRUE: Yes, execute the code.

#### R Code Chunk Arguments
![](Figures/knitr_arguments.jpeg)

#### R Code Chunks:  Displaying Plots 
![](Figures/figure.jpeg)

<img src="earth523_Feb02_files/figure-html/figure-1.png" style="display: block; margin: auto;" />


### Global Chunk Options

You may want to use the same set of chunk options throughout a document and you don't want to retype those options in every chunk.  

**Global chunk options are for you!**



![](Figures/global.jpeg)



### Inline R Code  

You can evaluate expressions inline by enclosing the expression within a single back-tick qualified with `r`.  

Inline code is underappreciated!  

Last night, I saw 7 shooting stars!  


![](Figures/shootingstars.jpeg)



### Rendering document
1.  Run `rmarkdown::render("<filepath>")`  
2.  Click the very cute **knit HTML** button at the top of the RStudio scripts pane  

When you render, R will:  

- Execute each embedded code chunk and insert the results into your report.  

- Build a new version of your report in the output file type.  

- Open a preview of the output file in the viewer pane.  

-  Save the output file in your working directory.  

*** 




## Resources  
### Resources for Reproducible Research  
- Vince Buffalo's <a href="http://www.amazon.com/Bioinformatics-Data-Skills-Reproducible-Research/dp/1449367372" target="_blank">Bioinformatics Data Skills</a> book and it's helpful <a href="https://github.com/vsbuffalo/bds-files" target="_blank">github page.</a> 
    + Main source for this presentation.
- A course by Karl Broman at the University of Wisconsin-Madison on <a href="http://kbroman.org/Tools4RR/" target="_blank">Reproducible Research.</a>  
- Reproducible-Science-Curriculum <a href="https://github.com/Reproducible-Science-Curriculum/rr-init" target="_blank">Github repo for Reproducible Research Project Initialization</a>  
- <a href="http://ropensci.github.io/reproducibility-guide/" target="_blank">ROpenSci Reproducibility Research</a> guidelines  
- Publications:  
    + <a href="http://journals.plos.org/plosbiology/article?id=10.1371/journal.pbio.1001745" target="_blank">Best Practices for Scientific Computing</a> by Wilson et al., 2014.  
    + <a href="http://journals.plos.org/ploscompbiol/article?id=10.1371/journal.pcbi.1000424" target="_blank">A Quick Guide to Organizing Computational Biology Projects</a> by Noble, 2009.  
    + <a href="http://www.sciencemag.org/content/334/6060/1226.abstract" target="_blank">Reproducible Research in Computational Science</a> by Peng, 2011.  
- <a href="https://www.stat.wisc.edu/reproducible" target="_blank">Statistics Department Resources from the University of Wisconsin</a>  
- "Baby steps for the open-curious" from <a href="https://practicaldatamanagement.wordpress.com/2014/10/23/baby-steps-for-the-open-curious/" target="_blank">Christie Bahlai</a>  


### Resources for Rmarkdown, RStudio and R  
- Yihui Xie's <a href="http://www.amazon.com/Dynamic-Documents-knitr-Chapman-Series/dp/1482203537" target="_blank">Dynamic Documents with R and Knitr</a> and it's <a href="https://github.com/yihui/knitr-book/" target="_blank">github page.</a>  
- Resources from Jennifer Bryan's  <a href="http://stat545-ubc.github.io/git00_index.html" target="_blank">Stats 545</a>.  
- <a href="https://www.rstudio.com/wp-content/uploads/2015/03/rmarkdown-reference.pdf" target="_blank">RMarkdown Quick Reference Guide</a>  
- Christopher Gandrud's <a href="http://www.amazon.com/Reproducible-Research-Studio-Chapman-Series/dp/1466572841" target="_blank">Reproducible Research with R and RStudio</a> and it's <a href="https://github.com/christophergandrud/Rep-Res-Book" target="_blank">github page</a>  
- <a href="http://rmarkdown.rstudio.com/" target="_blank">RStudio RMarkdown Documentation</a>  
- <a href="http://www.rstudio.com/wp-content/uploads/2015/02/rmarkdown-cheatsheet.pdf" target="_blank">Rmd Cheatsheet</a>
- <a href="http://cran.r-project.org/web/packages/knitr/vignettes/knitr-refcard.pdf" target="_blank">Knitr Reference Card</a>
- <a href="http://www.cookbook-r.com/Graphs/" target="_blank">R Cookbook for ggplot</a>  
- A <a href="http://rpubs.com/marschmi/RMarkdown" target="_blank">tutorial on RMarkdown</a>  that I wrote.
  
  
### Other Resources  
- <a href="https://software-carpentry.org/" target="_blank">Software Carpentry Foundation</a>  
- <a href="http://datacarpentry.github.io/" target="_blank">Data Carpentry</a>  


***




