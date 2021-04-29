Dr. Soumyo Maity, CS02-CS03, 29 April 2021

Assignment 1 :Security Engineering
================
## Objective

* How a code repository works concurrently with version control (handson git)
* How a SAST tool works (Handson SonarQube)
* How to inetegrate a SAST tool with build server (Handson devSECops)

## Requirements
* A Bitbucket account (invitation sent to everyone)
* A linux shell, or a mac terminal or a windows cmd/powershell
* install git
* Access SonarQube Server
* Install SonarScanner agent to your local machine 

## Background Studies

### Git
Git is an _Opensource Distributed Version Control System_. Now that’s a lot of words to define something.
This basically means that Git is a content tracker. So Git can be used to store content — it is mostly used to store code due to the other features it provides.

Let us break the definition down,
**Opensource**: Yes, it is opensource and created by [Linus Torvalds](https://en.wikipedia.org/wiki/Linus_Torvalds), the same geek who created Linux. In fact, the word Linux came from his name as Linus.

**Distributed**: Git has a remote repository which is stored in a server and a local repository which is stored in the computer of each developer. This means that the code is not just stored in a central server, but the full copy of the code is present in all the developers’ computers. Git is a Distributed Version Control System since the code is present in every developer’s computer. I will explain the concept of remote and local repositories later in this article.

**Version Control System**: The code (or other contents) which is stored in Git keeps changing as more code is added. Also, many developers can add code in parallel. So Version Control System helps in handling this by maintaining a history of what changes have happened. Also, Git provides features like branches and merges, which we will be covering later.


In older days SVN, Perforce etc were used widely. After introduction of Git, most of the developers prefer it and we see widespread adoption of this. 

Now enough of explanation given. Please get your hands dirty and 
* Install Git : [Here is the link](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) that will guide you through.
  
* Check few Git Commands : [Few commands](https://www.freecodecamp.org/news/10-important-git-commands-that-every-developer-should-know/) that every software professional should know.
  
* Know about BitBucket : Bitbucket is a Git-based source code repository hosting service owned by Atlassian. Bitbucket offers both commercial plans and free accounts with an unlimited number of private repositories. You can do all the git operations on these repositories, and also you can integrate build tools to build the codes. Here is a [detailed tutorial](https://www.atlassian.com/git/tutorials/learn-git-with-bitbucket-cloud) to learn git with bitbucket. 
* Get started withBitBucket : You have received a mail to create a BitBucket account. Please follow the instruction.  
 
### SAST

As we have seen in our last class that there is a bunch of security scanners that analyzes the source codes and finds security bugs (or vulnerabilities) in those codes. We call this family of security tools a Static Application Security Testing tool (SAST) or static analysis. Find security vulnerabilities in the source code secure your organization’s applications from being susceptible to attacks. SAST usually scans an application before the code is compiled. It’s also known as white box testing.

 SAST takes place very early in the software development life cycle (SDLC) as it does not require a working application and can take place without code being executed. It helps developers identify vulnerabilities in the initial stages of development and quickly resolve issues without breaking builds or passing on vulnerabilities to the final release of the application.

SAST tools give developers real-time feedback as they code, helping them fix issues before they pass the code to the next phase of the SDLC. This prevents security-related issues from being considered an afterthought. SAST tools also provide graphical representations of the issues found, from source to sink. These help you navigate the code easier. Some tools point out the exact location of vulnerabilities and highlight the risky code. Tools can also provide in-depth guidance on how to fix issues and the best place in the code to fix them, without requiring deep security domain expertise.

Developers can also create the customized reports they need with SAST tools; these reports can be exported offline and tracked using dashboards. Tracking all the security issues reported by the tool in an organized way can help developers remediate these issues promptly and release applications with minimal problems. This process contributes to the creation of a secure SDLC.

It’s important to note that SAST tools must be run on the application on a regular basis, such as during daily/monthly builds, every time code is checked in, or during a code release.

Here in our assignment we will use [SonarQube](https://www.sonarqube.org/features/security/) which is free for community usage. Apart from Sonarqube, there are many other commercial SAST tools that are used by the software manufacturers. Fortify, CheckMarx, Veracode, Coverity etc. are such tools. 

We have set up a SonarQube server at XX.XX.XX.XX
(Kindly check with Rahul for accessing this machine)




### Assignments:
This assignment has three parts.
#### Part 1: 

I have created a repository at https://bitbucket.org/smymty/assignment1/. I added few PhP codes in this repository. 

Your job is,

* Clone this repository to your local machine

* Create a new branch with branch name, \<your first name>_\<your last name>

* There is a file named `sample.html` in your downloaded (or cloned) repository. Open that file, 
  
```html
1  <!DOCTYPE html>
2  <html>
3    <body>
4
5      <h1>Assignment 1</h1>
6      <h2>Who did this assignment?</h2>
7         <p> Soumyo Maity <p>
8
9     </body>
10  </html>
```

Add your name after line number 7, below my name, within a `<p>...</p>` tag, like 

```html
8        <p> Your_First_Name Your_Last_Name> </p>
```

* Checkout, Commit and Push to the original repository in BitBucket. 

* You should find a new branch is created with your changes in the code. 

* Create a [Pull Request](https://docs.github.com/en/github/collaborating-with-issues-and-pull-requests/about-pull-requests#)

* Being the curator of this repository, I can merge all these changes together into the master branch. I will show that in the class. 

#### Part 2:

OWASP WebGoatPHP is a port of OWASP WebGoat to PHP and MySQL/SQLite databases. The goal is to create an interactive teaching environment for web application security by offering lessons in the form of challenges. In each challenge the user must exploit the vulnerability to demonstrate their understanding.

WebGoatPHP supports four different modes i.e single mode, workshop mode, contest mode and secure coding mode.
