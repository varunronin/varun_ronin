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

> If you hate that boring CLI/terminal used by the geeks, please try to love it. You have to do most of the things here from that evil black screen. Believe me, that will make you more confident at the end.  

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

### CI/CD Pipeline and DevOps

If you’re new to the field of software development, you’ve likely come across a lot of terms and phrases. It can be somewhat confusing and even a bit overwhelming as you’re just entering the world of programming. Few of these terms are CI/CD, Pipelines, DevOps etc. But What are they?

In software engineering, CI/CD or CICD generally refers to the combined practices of continuous integration and either continuous delivery or continuous deployment.CI/CD bridges the gaps between development and operation activities and teams by enforcing automation in building, testing and deployment of applications. Modern day DevOps practices involve continuous development, continuous testing, continuous integration, continuous deployment and continuous monitoring of software applications throughout its development life cycle. The CI/CD practice or CI/CD pipeline forms the backbone of modern day DevOps operations.

You can refere to a [nice turial](https://www.redhat.com/en/topics/devops/what-is-ci-cd) from RedHat 

DevOps is a combination of the two words “development” and “operations.” Patrick Debois, a DevOps expert, came up with the term “DevOps” in 2009 and it stuck ever since. Some people say that it was around this time that there was a shift in IT culture, and DevOps represents this shift. DevOps is an umbrella term that describes the operation of a team collaborating throughout an entire programming production process - from the design through the development stages. It’s a combination of tools and philosophies that increase a team’s capability to produce results at high efficiency. 

DevOps programmers typically use conventional infrastructure management and software development processes. When it comes to software development, DevOps tends to take an Agile approach.

Here is a very [nice tutorial](https://azure.microsoft.com/en-in/overview/devops-tutorial/) from microsoft on DevOps.

**Note:*
In a simpler note, in older days, the following steps were followd during a development,

1. devopers used to write codes in their own machine. Then they used to sent the codes to a central repository, and a curator used to control that repository. Version control softwares like SVN, perforce were there. 
2. Then there was a build team. They took the codes from the repository, downloaded them to a build server. After that, they used to compile the entire source code (or the stack) with all the associated dependencies. 
3. Then comes the testers. Testers from QA team used to test those codes with automated and manual test-cases. 
4. At the end, IT teams used to deploy those built and tested applications for the customers. 

You must be remembering those days... and most of the software development process used to work that way, just a few years back. But, not anynmore!

Now, all these 4 steps are done with automation. Step 1 is done by Git. Step 2 is automated with CI. Step 4 is automated using CD. Step 3 is atken care of, both by CI and CD. So, we are calling it together as CI/CD. 
Now all these steps are individually automated as well as  automated as together. We are calling the fully automated process of step 1 to step 4 as devops. As it a sequencial automated process, we are calling it a pipeline. And with this, we are eliminating different roles of developers, builders, testers, deployers and expecting everybody in the team will know and contribute in all these processes. That is the devOps culture. 

> if you have touch your system during normal operation, you have a bug
> -- Google Phylosophy


## Assignments:

This assignment has three parts.

### Part 1: 

I have created a repository at `https://bitbucket.org/smymty/assignment1/`. I added few PhP codes in this repository. 

Your job is,

* Clone this repository to your local machine

* Create a new branch with branch name, `<your first name>_<your last name>`

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
8        <p> Your_First_Name Your_Last_Name </p>
```

* Checkout, Commit and Push to the original repository in BitBucket. 

* You should find a new branch is created with your changes in the code. 

* Create a [Pull Request](https://docs.github.com/en/github/collaborating-with-issues-and-pull-requests/about-pull-requests#)

* Being the curator of this repository, I can merge all these changes together into the master branch. I will show that in the class. 

### Part 2:


Running SonarQube or any other SAST tool is simple. It has two component, 

1. a *server* hosted at some shared location

2. an *agent* installed at the local machine (developers local machine or the build server)

We have set up a SonarQube server at http://XX.XX.XX.XX:9000 (Kindly check with [Rahul Mohan](mailto:rahulm.cs@reva.edu.in) for accessing this machine). Username and password will be sent to all of you. Create a project with projectname `<your first name>_<your last name>`.
Generate token

The local agent is called SonarScanner. It has to be installed at your local machine. Download and configure/install the agent as described in the official [SonarScanner Documentation](https://docs.sonarqube.org/latest/analysis/scan/sonarscanner/).

Download links, 

* [windows 64-bit](https://binaries.sonarsource.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-4.6.1.2450-windows.zip)
* [Linux 64-bit](https://binaries.sonarsource.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-4.6.1.2450-linux.zip)
* [Mac OSX 64-bit](https://binaries.sonarsource.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-4.6.1.2450-macosx.zip)

Your job is, to analyze the repository that you cloned in Part 1 with SonarQube. Follow the steps,

1. log in to the SonarQube server
2. Click the Create new project button.
3. Give your project a Project key and a Display name and click the *Set Up* button.
4. Under *Provide a token*, select *Generate a token*. Give your token a name, click the Generate button, and click Continue.
5. Select your project's main language under Run analysis on your project, and follow the instructions to analyze your project. 
6. Download and execute the SonarScanner on your cloned repository 
7. **Optional:** If you're a pro developer, you can use Maven or Gradle. The Scanner is automatically downloaded in that case. 8. 
After successfully analyzing your code, you'll see your first analysis on SonarQube server


### Part 3:

Here, we will automate the entire scanning process with the build process and make it a part of DevOps. And integrating security engineering with DevOps is called DevSecOps. We are starting with one SAST tool. We can inetegrate an array of such security scanning tools to make it a fully functional DevSecOps.

Follow, the steps [described here](https://docs.sonarqube.org/latest/analysis/bitbucket-cloud-integration/) to integrate sonareqube with BitBucket cloud. 