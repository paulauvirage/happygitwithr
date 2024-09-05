--- 
title: "Happy Git and GitHub for the useR"
author: "Jenny Bryan, the STAT 545 TAs, Jim Hester"
site: bookdown::bookdown_site
documentclass: book
bibliography: [book.bib, packages.bib]
biblio-style: apalike
link-citations: yes
github-repo: jennybc/happy-git-with-r
description: "Using Git and GitHub with R, Rstudio, and R Markdown"
twitter-handle: jennybryan
url: 'https\://happygitwithr.com/'
cover-image: img/watch-me-diff-watch-me-rebase-smaller.png
---

# Let's Git started {-}

<div class="figure">
<img src="img/watch-me-diff-watch-me-rebase-smaller.png" width="669" height="400" alt="Cover image" />
<p class="caption">Still from <a href="https://www.youtube.com/watch?v=uBWrpVrazzA">Heaven King video</a></p>
</div>

Happy Git provides opinionated instructions on how to:

  * Install Git and get it working smoothly with GitHub, in the shell and in the [RStudio IDE](https://www.rstudio.com/products/rstudio/).
  * Develop a few key workflows that cover your most common tasks.
  * Integrate Git and GitHub into your daily work with R and [R Markdown](https://rmarkdown.rstudio.com).
  
The target reader is someone who uses R for data analysis or who works on R packages, although some of the content may be useful to those working in adjacent areas.

The first two parts, [Installation](#install-intro) and [Connect Git, GitHub, RStudio](#connect-intro), provide a "batteries included" quick start to verify your setup.

In [Early GitHub Wins](#usage-intro), we rack up some early success with the basic workflows that are necessary to get your work onto GitHub. We also show the special synergy between R/R Markdown/RStudio and GitHub, which provides a powerful demonstration of why all this setup is worthwhile.

The use of Git/GitHub in data science has a slightly different vibe from that of pure software development, due to differences in the user's context and objective. Happy Git aims to complement existing, general Git resources by highlighting the most rewarding usage patterns for data science. This perspective on the Git landscape is presented in [Basic Git Concepts](#git-intro) and [Daily Workflows](#workflows-intro). 

## License {-}

<a rel="license" href="http://creativecommons.org/licenses/by-nc/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-nc/4.0/88x31.png" /></a><br /><span xmlns:dct="http://purl.org/dc/terms/" property="dct:title">Happy Git and GitHub for the useR</span> by <a xmlns:cc="http://creativecommons.org/ns#" href="https://github.com/jennybc/happy-git-with-r" property="cc:attributionName" rel="cc:attributionURL">Jennifer Bryan</a> is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-nc/4.0/">Creative Commons Attribution-NonCommercial 4.0 International License</a>.



<!--chapter:end:index.Rmd-->

# Why Git? Why GitHub? {#big-picture}

Why would a data analyst use hosted version control?

*This intro has grown into a stand-alone article that is arguably a better introduction at this point. Until I merge it back in, consider reading the article instead: "Excuse me, do you have a moment to talk about version control?" <https://dx.doi.org/10.7287%2Fpeerj.preprints.3159v2>.*

## Why Git?

[Git](http://git-scm.com) is a __version control system__. Its original purpose was to help groups of developers work collaboratively on big software projects. Git manages the evolution of a set of files -- called a __repository__ -- in a sane, highly structured way. If you have no idea what I'm talking about, think of it as the "Track Changes" features from Microsoft Word on steroids.

Git has been re-purposed by the data science community. In addition to using it for source code, we use it to manage the motley collection of files that make up typical data analytical projects, which often consist of data, figures, reports, and, yes, source code.

A solo data analyst, working on a single computer, will benefit from adopting version control. But not nearly enough to justify the pain of installation and workflow upheaval. There are much easier ways to get versioned back ups of your files, if that's all you're worried about.

In my opinion, **for new users**, the pros of Git only outweigh the cons when you factor in the overhead of communicating and collaborating with other people. Who among us does not need to do that? Your life is much easier if this is baked into your workflow, as opposed to being a separate process that you dread or neglect.

## Why GitHub?

This is where hosting services like [GitHub](https://github.com), [Bitbucket](https://bitbucket.org), and [GitLab](https://about.gitlab.com) come in. They provide a home for your Git-based projects on the internet.  If you have no idea what I'm talking about, think of it as DropBox but much, much better. The remote host acts as a distribution channel or clearinghouse for your Git-managed project. It allows other people to see your stuff, sync up with you, and perhaps even make changes. These hosting providers improve upon traditional Unix Git servers with well-designed web-based interfaces.

Even for private solo projects, it's a good idea to push your work to a remote location for peace of mind. Why? Because it's fairly easy to screw up your local Git repository, especially when you're new at this. The good news is that often only the Git infrastructure is borked up. Your files are just fine! Which makes your Git pickle all the more frustrating. There are official Git solutions to these problems, but they might require expertise and patience you can't access at 3 a.m. If you've recently pushed your work to GitHub, it's easy to grab a fresh copy, patch things up with the changes that only exist locally, and get on with your life.

We target [GitHub](https://github.com) -- not [Bitbucket](https://bitbucket.org) or [GitLab](https://about.gitlab.com) -- for the sake of specificity. However, all the big-picture principles and even some mechanics will carry over to these alternative hosting platforms.

Don't get too caught up on public versus private at this point. There are many ways to get private repositories from the major providers for low or no cost. Just get started and figure out if and how Git/GitHub is going to work for you! If you outgrow this arrangement, you can throw some combination of technical savvy and money at the problem. You can either pay for a higher level of service or self-host one of these platforms.

## Is it going to hurt?

Yes.

You have to install Git, get local Git talking to GitHub, and make sure RStudio can talk to local Git (and, therefore, GitHub). This is one-time or once-per-computer pain.

For new or existing projects, you will:

  * Dedicate a directory (a.k.a "folder") to it.
  * Make it an RStudio Project.
  * Make it a Git repository.
  * Go about your usual business. But instead of only *saving* individual files, periodically you make a **commit**, which takes a multi-file snapshot of the entire project.
    - Have you ever versioned a file [by adding your initials or the date](http://www.phdcomics.com/comics/archive.php?comicid=1531)? That is effectively a **commit**, albeit only for a single file: it is a version that is significant to you and that you might want to inspect or revert to later.
  * Push commits to GitHub periodically.
    - This is like sharing a document with colleagues on DropBox or sending it out as an email attachment. It signals you're ready to make your work visible to others and invite comment or edits.
  
This is a change to your normal, daily workflow. It feels weird at first but quickly becomes second nature. FWIW, [STAT 545](http://stat545.com) students are required to submit all coursework via GitHub. This is a major topic in class and office hours for the first two weeks. Then we practically never discuss it again.

More bad news. The [STAT 545](http://stat545.com) pain is short-lived because students primarily work in their own repositories. Do you use GitHub to work with other people or to coordinate your own work from multiple computers? If so, after you recover from the initial setup, Git will crush you again with **merge conflicts**. And this is not one-time pain, this could be a dull ache for a long time. The best remedy is prevention, but also understanding how to back out of tricky situations and tackle them on your own terms.

The rest of this site is dedicated to walking you through the necessary setup and creating your first few Git projects. We conclude with prompts that guide you through some of the more advanced usage that makes all of this initial pain worthwhile.

## What is the payoff?

**Exposure**: If someone needs to see your work or if you want them to try out your code, they can easily get it from GitHub. If they use Git, they can clone or fork your repository. If they don't use Git, they can still browse your project on GitHub like a normal website and even grab everything by downloading a zip archive.

**Be a keener!** If you care deeply about someone else's project, such as an R package you use heavily, you can track its development on GitHub. You can watch the repository to get notified of major activity. You can fork it to keep your own copy. You can modify your fork to add features or fix bugs and send them back to the owner as a proposed change.

**Collaboration**: If you need to collaborate on data analysis or code development, then everyone should use Git. Use GitHub as your clearinghouse: individuals work independently, then send work back to GitHub for reconciliation and transmission to the rest of the team. The advantage of Git/GitHub is highlighted by comparing these two ways of collaborating on a document:

  * **Edit, save, attach.** In this workflow, everyone has one (or more!) copies of the document and they circulate via email attachment. Which one is "master"? Is it even possible to say? How do different versions relate to each other? How should versions be reconciled? If you want to see the current best version, how do you get it? All of this usually gets sorted out by social contract and a fairly manual process.
  * **Google Doc.** In this workflow, there is only one copy of the document and it lives in the cloud. Anyone can access the most recent version on demand. Anyone can edit or comment or propose a change and this is immediately available to everyone else. Anyone can see who's been editing the document and, if disaster strikes, can revert to a previous version. A great deal of ambiguity and annoying reconciliation work has been designed away.

Managing a project via Git/GitHub is much more like the Google Doc scenario and enjoys many of the same advantages. It is definitely more complicated than collaborating on a Google Doc, but this puts you in the right mindset.

## Who can do what?

A public repository is readable by the world. The owner can grant higher levels of permission to others, such as the ability to push commits.

A private repository is invisible to the world. The owner can grant read, write (push), or admin access to others.

There is also a formal notion of an organization, which can be useful for managing repository permissions for entire teams of people.

## Special features of GitHub

*this is perhaps too detailed ... full stop? or does it belong elsewhere?*

In addition to a well-designed user interface, GitHub offers two especially important features:

  * **Issues.** Remember how we're high-jacking software development tools? Well, this is the bug tracker. It's a list of things ... bugs, feature requests, to dos, whatever.
    - Issues are tightly integrated with email and therefore allow you to copy/embed important conversations in the associated repo.
    - Issues can be assigned to people (e.g., to dos) and tagged ("bug" or "progress-report").
    - Issues are tightly integrated with commits and therefore allow you to record *that the changes in this commit solve that problem which was discussed in that issue*.
    - As a new user of GitHub, one of the most productive things you can do is to use GitHub issues to provide a clear bug report or feature request for a package you use.
 * **Pull requests.** Git allows a project to have multiple, independent branches of development, with the notion that some should eventually be merged back into the main development branch. These are technical Git terms but hopefully also make sense on their own. A pull request is a formal proposal that says: "Here are some changes I would like to make." It might be linked to a specific issue: "Related to #14." or "Fixes #56". GitHub facilitates and preserves the discussion of the proposal, holistically and line-by-line.

## What's special about using R with Git and GitHub?

  * The active R package development community on GitHub. Read about R-specific GitHub resources and searching [here](#search).
  * Specific workflows make it rewarding to share source code, rendered reports, and entire projects. Read more about [R Markdown](#rmd-test-drive), [R scripts](#r-test-drive), and [R-heavy projects](#repo-browsability).
  * Git- and GitHub-related features of the [RStudio IDE](https://www.rstudio.com/products/rstudio-desktop/). This is covered throughout.

## Audience and pre-reqs

The target audience for this site is someone who analyzes data, probably with R, though some of the content may be useful to analysts using other languages. R package development with Git(Hub) is absolutely in scope, but it is not an explicit focus or requirement.

The site is aimed at intermediate to advanced R users, who are comfortable writing R scripts and managing R projects. You should have a good grasp of files and directories and be generally knowledgeable about where things live on your computer.

Although we will show alternatives for most Git operations, we will inevitably spend some time in the shell and we assume some prior experience. For example, you should know how to open up a shell, navigate to a certain directory, and list the files there. You should be comfortable using shell commands to view/move/rename files and to work with your command history.

## What this is NOT

We aim to teach novices about Git on a strict "need to know" basis. Git was built to manage development of the Linux kernel, which is probably very different from what you do. Most people need a small subset of Git's functionality and that will be our focus. If you want a full-blown exposition of Git as a directed acyclic graph or a treatise on the Git-Flow branching strategy, you will be sad.

<!--chapter:end:overview.Rmd-->

# Contributors {#contrib}

Jenny Bryan ([jennybryan.org](https://jennybryan.org)), Software Engineer at [Posit](https://posit.co/) on the [tidyverse](https://www.tidyverse.org)/[r-lib](https://github.com/r-lib/) team. Main author and content wrangler.

The development and delivery of this material has also benefited greatly from contributions by:

  * Dean Attali ([deanattali.com](http://deanattali.com)), Shiny consultant and [STAT 545](http://stat545.com) TA alum.
  * Bernhard Konrad, Software Engineer at Google and [STAT 545](http://stat545.com) TA alum.
  * Shaun Jackman ([sjackman.ca](http://sjackman.ca)), Bioinformatics Ph.D. student at UBC, lead maintainer of [Linuxbrew](http://linuxbrew.sh), and [STAT 545](http://stat545.com) TA alum.
  * Jim Hester ([jimhester.com](https://www.jimhester.com)), Software Engineer at [Posit](https://posit.co/) on the [tidyverse](https://www.tidyverse.org)/[r-lib](https://github.com/r-lib/) team.
  * A growing number of [GitHub contributors](https://github.com/jennybc/happy-git-with-r/graphs/contributors)

<!--chapter:end:contributors.Rmd-->

# Workshops

These materials can be used for independent study, but they have also been used to support:

  * in-person workshops (see below)
  * [STAT 545](http://stat545.com) at UBC
  * [UBC Master of Data Science](http://masterdatascience.science.ubc.ca)

## Pre-workshop set-up

Optional reading on the big picture motivation: [Why Git? Why GitHub?](#big-picture)

**It is vital that you attempt to set up your system in advance. You cannot show up at the workshop with no preparation and keep up!**

Try this. Best case scenario is about 1 - 2 hours. If you hit a wall, we will help:

  * [Register a free GitHub account](#github-acct).
  * [Install or update R and RStudio](#install-r-rstudio).
  * [Install Git](#install-git).
  * [Introduce yourself to Git](#hello-git).
  * [Configure a personal access token](#https-pat) or [set up SSH keys](#ssh-keys).
  * [Prove local Git can talk to GitHub](#push-pull-github).
  * [Prove RStudio can find local Git](#rstudio-git-github) and, therefore, can talk to GitHub.
    - FYI: this is where our hands-on activities usually start. We walk through a similar activity together, with narrative, and build from there.
  * Contemplate if you'd like to [install an optional Git client](#git-client), now or in future.

Troubleshooting:

  * Sometimes RStudio [needs a little help finding Git](#rstudio-see-git).
  * General troubleshooting: [RStudio, Git, GitHub Hell](#troubleshooting).

These are battle-tested instructions, so most will succeed. We believe in you! If you have trouble, reach out for help and stick with it. Where to get help:

  * If you are enrolled in an upcoming workshop, find it below to get specifics on pre-workshop support.
  * We *might* be able to respond to a GitHub issue [here](https://github.com/jennybc/happy-git-with-r/issues).
  * If there is a clear R/RStudio angle, post on <https://forum.posit.co/>.
  * General advice: search with Google and on <https://stackoverflow.com>, see also <https://github.community>.

## posit::conf 2023

1-day workshop: What They Forgot to Teach You About R  
Will have half-day coverage of Git/GitHub
Sep 17, [`posit.co/conference`](https://posit.co/conference/) Workshop Day, Chicago

Registered workshop participants should use [this thread](https://forum.posit.co/t/what-they-forgot-to-teach-you-about-r-workshop-rstudio-conf-2022/138999) on forum.posit.co to discuss system prep woes.

## Previous workshops

  * rstudio::conf 2022
   - 2-day workshop: What They Forgot to Teach You About R  
   - ~25% of content was Git/GitHub
   - July 25-26, 2022, Washington, D.C.
  * RaukR: Advanced R for Bioinformatics Summer School
    - June 13, 2022, online
  * rstudio::conf 2020
    - 2-day workshop: What They Forgot to Teach You About R  
    - ~25% of content was Git/GitHub + R/Rmd/RStudio  
    - January 27-28, 2020, San Francisco, CA
  * UBC Master of Data Science Program
    - Guest lecture on daily Git/GitHub workflows
    - January 9, 2020
  * RaukR: Advanced R for Bioinformatics Summer School
    - June 10-20, 2019, Visby, Sweden
  * rstudio::conf 2019
    - 2-day workshop: What They Forgot to Teach You About R  
    - ~25% of content was Git/GitHub + R/Rmd/RStudio  
    - Jan 15-16, 2019, Austin, TX
  * Seattle October 2018
    - 2-day workshop: [What They Forgot to Teach You About R](https://whattheyforgot.org/index.html#seattle-2018-october-4-5)  
    - 3 of 8 units on Git/GitHub + R/Rmd/RStudio  
    - Oct 4-5, 2018, The Westin Seattle
  * rstudio::conf 2018
    - 2-day workshop: What They Forgot to Teach You About R  
    - ~25% of content was Git/GitHub + R/Rmd/RStudio  
    - Jan 31 & Feb 1, 2018, San Diego, CA
  * CSAMA 2017: Statistical Data Analysis for Genome Biology
    - <http://www.huber.embl.de/csama2017/>  
    - June 11-16, 2017, Bressanone-Brixen, Italy  
  * satRday Cape Town 2017
    - <http://capetown2017.satrdays.org>  
    - February 16 - 18, 2017, Cape Town, South Africa
  * rstudio::conf 2017
    - <https://www.rstudio.com/conference/>  
    - January 13 - 14, 2017, Orlando, FL  
    - Saturday January 14, 10:15am to 12:30pm
  * CSAMA 2016: Statistical Data Analysis for Genome Biology
    - <http://www.huber.embl.de/csama2016/>  
    - July 10 - 15, 2016, Bressanone-Brixen, Italy  
  * useR! 2016 Stanford
    - <http://user2016.r-project.org>  
    - Monday, June 27, 2016  
    - [Using Git and GitHub with R, RStudio, and R Markdown](http://user2016.r-project.org/tutorials/01.html)

<!--chapter:end:workshops.Rmd-->

# (PART) Installation {-} 

# Half the battle {#install-intro .unnumbered}

Getting all the necessary software installed, configured, and playing nicely together is honestly half the battle when first adopting Git. Brace yourself for some pain. The upside is that you can give yourself a pat on the back once you get through this. And you WILL get through this.

You will find far more resources for how to *use Git* than for installation and configuration. Why? The experts ...

  * Have been doing this for years. It's simply not hard for them anymore.
  * Probably use some flavor of Unix. They may secretly (or not so secretly) take pride in neither using nor knowing Windows.
  * Get more satisfaction and reward for thinking and writing about Git concepts and workflows than Git installation.

In their defense, it's hard to write installation instructions. Failures can be specific to an individual OS or even individual computer. If you have some new problem and, especially, the corresponding solution, [we'd love to hear from you!](https://github.com/jennybc/happy-git-with-r/issues)

## Success and operating systems {-}

<style type="text/css">
#success-and-operating-systems table {
  width: auto;
}
</style>

Our installation instructions have been forged in the fires of [STAT 545](http://stat545.com), [STAT 540](https://stat540-ubc.github.io), and assorted workshops, over several years. We regularly hear from [grateful souls](https://twitter.com/ibddoctor/status/777610645617475584) [on the internet](https://twitter.com/millsGT49/status/647059167509921793) who also have success.

Here's data on the operating systems we encounter in STAT 545 and other workshops: overall the bulk are split sort of evenly between Mac and Windows (various flavours), with a dash of Linux. Except in a BioConductor context (CSAMA), which is dominated by Mac or Linux.

|             |     2014 |     2015 |     2016 | useR! 2016 | CSAMA 2016 | CSAMA 2017 | r::c 2018 | seattle 2018 |
|------------:|---------:|---------:|---------:|-----------:|-----------:|-----------:|----------:|-------------:|
|        Mac  | 16 (41%) | 38 (52%) | 37 (45%) |   28 (44%) |   25 (58%) |   23 (56%) |  51 (57%) |      16 (49%) |
| Windows 10* |   0 (0%) |  8 (11%) | 30 (36%) |   27 (43%) |    6 (14%) |    8 (20%) |  19 (21%) |      12 (36%) |
|  Windows 8  | 12 (31%) |  9 (12%) |  4  (5%) |            |            |    1 ( 2%) |   2  (2%) |               |
|  Windows 7  |  9 (23%) | 13 (18%) | 10 (12%) |            |            |    1 ( 2%) |  13 (14%) |       4 (12%) |
|      Linux  |   2 (5%) |   5 (7%) |  2  (2%) |    8 (13%) |   12 (28%) |    9 (20%) |   5  (6%) |       1  (3%) |

\* Windows 10 is the Windows catchall, when I don't have more specific info.

<!--chapter:end:install-intro.Rmd-->

# Register a GitHub account {#github-acct}

Register an account with GitHub. It's free!

  * <https://github.com>

## Username advice

You will be able to upgrade to a paid level of service, apply discounts, join organizations, etc. in the future, so don't fret about any of that now. **Except your username. You might want to give that some thought.**

A few tips, which sadly tend to contradict each other:

  * Incorporate your actual name! People like to know who they're dealing with. Also makes your username easier for people to guess or remember.
  * Reuse your username from other contexts, e.g., Twitter or Slack. But, of course, someone with no GitHub activity will probably be squatting on that.
  * Pick a username you will be comfortable revealing to your future boss.
  * Shorter is better than longer.
  * Be as unique as possible in as few characters as possible. In some settings GitHub auto-completes or suggests usernames.
  * Make it timeless. Don't highlight your current university, employer, or place of residence, e.g. JennyFromTheBlock.
  * Avoid words laden with special meaning in programming. In my first inept efforts to script around the GitHub API, I assigned lots of issues to [the guy with username `NA`](https://github.com/na) because my vector of GitHub usernames contained missing values. A variant of [Little Bobby Tables](https://xkcd.com/327/).
  * Avoid the use of upper vs. lower case to separate words. We highly recommend all lowercase. GitHub treats usernames in a case insensitive way, but using all lowercase is kinder to people doing downstream regular expression work with usernames, in various languages. A better strategy for word separation is to use a hyphen `-`.

You can change your username later, but better to get this right the first time.

  * <https://help.github.com/articles/changing-your-github-username/>
  * <https://help.github.com/articles/what-happens-when-i-change-my-username/>

## Free private repos

GitHub offers free unlimited private repositories for all users. These free private repositories support up to three external collaborators, making them a perfect place for your personal projects, for job applications, and testing things out before making your project open source.

Go ahead and register your free account NOW and then pursue any special offer that applies to you:

  * Students, faculty, and educational/research staff: [GitHub Education](https://education.github.com).
    - GitHub "Organizations" can be extremely useful for courses or research/lab groups, where you need some coordination across a set of repos and users.
  * Official nonprofit organizations and charities: [GitHub for Good](https://github.com/nonprofit)
  
## Pay for private repos

Anyone can pay to have private repos with support for unlimited collaborators. A personal plan with private repos supporting unlimited collaborators is $7 / month at the time of writing, and includes several [advanced features](https://help.github.com/articles/github-s-products/#github-pro). See the current plans and pricing here:

  * <https://github.com/pricing>

Go ahead and register your free account NOW. You can decide later if you'd like to upgrade to a paid plan.

<!--chapter:end:install-github-acct.Rmd-->

# Install or upgrade R and RStudio {#install-r-rstudio}



1. Install a pre-compiled binary of R for your OS from here:  
    <https://cloud.r-project.org>  
    Already have R installed? **Hold on: This is a great time to make sure your R installation is current.** Check your current version like so:
    
    ``` r
    R.version.string
    #> [1] "R version 4.4.1 (2024-06-14)"
    ```
2. Install RStudio Desktop for your OS from here:
    <https://posit.co/download/rstudio-desktop>
3. Update your R packages:
    
    ``` r
    update.packages(ask = FALSE, checkBuilt = TRUE)
    ```

## How to think about upgrading R and RStudio

**Get current, people.** You don't want to adopt new things on day one. But at some point, running old versions of software adds unnecessary difficulty.

In live workshops, there is a limit to how much we can help with ancient versions of R or RStudio. Also, frankly, there is a limit to our motivation. By definition, these problems are going away and we'd rather focus on edge cases with current versions, which affect lots of people.

Is your R version "old"? R had a *major* version change in April 2020, with the release of 4.0.0. It is a good idea to be on the current major version, meaning 4.something at this point, especially if you want to get the most out of a workshop.

Each major version is followed by several years of smaller releases (minor and patch releases). You can be more relaxed about upgrading minor versions, but you still want to stay reasonably current. As the 4.something series unfolds, I advise that you **never fall more than 1 minor version behind**.

Concrete example: let's say the released version of R is 4.7.1, which is totally fictional and well beyond the current version of R at the time of writing.
It's probably OK if you are still on 4.6.whatever, which is one minor version behind and is called "r-oldrel".
Being one minor version behind usually doesn't cause trouble.
Once you are 2 minor versions behind (4.5.whatever or earlier in this example), you will start to suffer.
In particular, you can no longer install pre-built binary add-on packages from CRAN.

Is your RStudio "old"?
You can expect to update RStudio much more often than R itself.
For example, I update RStudio every month or so, whereas I update R 1 or 2 times per year.

<!--chapter:end:install-r-rstudio.Rmd-->

# Install Git {#install-git}

You need Git, so you can use it at the command line and so RStudio can call it.

If there's any chance it's installed already, verify that, rejoice, and skip this step. (But consider *updating* an existing installation.)

Otherwise, find installation instructions below for your operating system.



## Git already installed?

Go to the shell (Appendix \@ref(shell)). Enter `which git` to request the path to your Git executable:


``` bash
which git
## /usr/bin/git
```

and `git --version` to see its version:
 

``` bash
git --version
## git version 2.43.0
```

If you are successful, that's great! You have Git already. No need to install! Move on.

If, instead, you see something more like `git: command not found`, keep reading.

macOS users might get an immediate offer to install command line developer tools. Yes, you should accept! Click "Install" and read more below.

## Windows  {#install-git-windows}

**Option 1** (*highly recommended*): Install [Git for Windows](https://git-for-windows.github.io/), also known as `msysgit` or "Git Bash", to get Git in addition to some other useful tools, such as the Bash shell. Yes, all those names are totally confusing, but you might encounter them elsewhere and I want you to be well-informed.

We like this because Git for Windows leaves the Git executable in a conventional location, which will help you and other programs, e.g. RStudio, find it and use it. This also supports a transition to more expert use, because the "Git Bash" shell will be useful as you venture outside of R/RStudio.

  *  **NOTE:** When asked about "Adjusting your PATH environment", make sure to select "Git from the command line and also from 3rd-party software". Otherwise, we believe it is good to accept the defaults.
  * Note that RStudio for Windows prefers for Git to be installed below `C:/Program Files` and this appears to be the default. This implies, for example, that the Git executable on my Windows system is found at `C:/Program Files/Git/bin/git.exe`. Unless you have specific reasons to otherwise, follow this convention.

This also leaves you with a Git client, though not a very good one. So check out Git clients we recommend (chapter \@ref(git-client)).

FYI, this appears to be equivalent to what you would download from here: <https://git-scm.com/download/>.

**Option 2** (*recommended*): Install [Git for Windows](https://git-for-windows.github.io/) via the [Chocolatey](https://chocolatey.org) package manager. If this means anything to you, Chocolatey is like [`apt-get`](https://en.wikipedia.org/wiki/APT_(Debian)) or [Homebrew](https://brew.sh), but for Windows instead of Debian/Ubuntu Linux or macOS. As far as I can tell, using Chocolatey to install Git for Windows gives the same result as installing it yourself (option 1).

This obviously requires that you already have [Chocolatey](https://chocolatey.org) installed or that you are up for installing it. It is not hard and the [instructions are here](https://chocolatey.org/install). This may be worthwhile if it seems likely you will be installing more open source software in the future.

After you install Chocolatey, in a shell (Appendix \@ref(shell)), do:

``` bash
choco install git.install
```

This installs the most current [Git (Install) X.Y.Z](https://chocolatey.org/packages/git.install) Chocolatey package. At the time of writing, that is "Git (Install) 2.33.1", but that version number will increment over time.

### Updating Git for Windows

If you already have Git for Windows, but it's not the latest version, it's a good idea to update.
You can [update like so from the command line](https://github.com/git-for-windows/git/wiki/FAQ#how-do-i-update-git-for-windows-upon-new-releases):

``` bash
git update-git-for-windows
```

## macOS

**Option 1** (*highly recommended*): Install the Xcode command line tools (**not all of Xcode**), which includes Git.

Go to the shell and enter one of these commands to elicit an offer to install developer command line tools:

``` bash
git --version
git config
```

Accept the offer! Click on "Install".

Here's another way to request this installation, more directly:

``` bash
xcode-select --install
```

We just happen to find this Git-based trigger apropos.

Note also that, after upgrading macOS, you might need to re-do the above and/or re-agree to the Xcode license agreement. We have seen this cause the RStudio Git pane to disappear on a system where it was previously working. Use commands like those above to tickle Xcode into prompting you for what it needs, then restart RStudio.

**Option 2** (*recommended*): Install Git from here: <http://git-scm.com/downloads>.

  * This arguably sets you up the best for the future. It will certainly get you the latest version of Git of all approaches described here.
  * The GitHub home for the macOS installer is here: <https://github.com/timcharper/git_osx_installer>.
    - At that link, you can find more info if something goes wrong or you are working on an old version of macOS.

**Option 3** (*recommended*): If you anticipate getting heavily into scientific computing, you're going to be installing and updating lots of software. You should check out [Homebrew](http://brew.sh), "the missing package manager for OS X". Among many other things, it can install Git for you. Once you have Homebrew installed, do this in the shell:

```
brew install git
```


## Linux

Install Git via your distro's package manager.

Ubuntu or Debian Linux:

```sh
sudo apt-get install git
```

Fedora or RedHat Linux:

```sh
sudo yum install git
```

A comprehensive list for various Linux and Unix package managers:

<https://git-scm.com/download/linux>

<!--chapter:end:install-git.Rmd-->

# Introduce yourself to Git {#hello-git}

In the shell (Appendix \@ref(shell)):

``` bash
git config --global user.name "Jane Doe"
git config --global user.email "jane@example.com"
git config --global --list
```

substituting your name and **the email associated with your GitHub account**.

The [usethis package](https://usethis.r-lib.org) offers an alternative approach. You can set your Git user name and email from within R:


``` r
## install if needed (do this exactly once):
## install.packages("usethis")

library(usethis)
use_git_config(user.name = "Jane Doe", user.email = "jane@example.org")
```

## More about `git config`

An easy way to get into a shell from RStudio is *Tools > Terminal* or *Tools > Shell*. More about the shell in the Appendix \@ref(shell).

Special Windows gotchas: If you are struggling on Windows, consider there are different types of shell and you might be in the wrong one. You want to be in a "Git Bash" shell, as opposed to Power Shell or the legacy `cmd.exe` command prompt. Read more in [the Appendix](#windows-shell-hell). This might also be a reason to do this configuration via the usethis package in R.

What user name should you give to Git? This does not have to be your GitHub user name, although it can be. Another good option is your actual first name and last name. If you commit from different machines, sometimes people work that info into the user name. Your commits will be labelled with this user name, so make it informative to potential collaborators and future you.

What email should you give to Git? This __must__ be the email associated with your GitHub account.

The first two commands used in the shell beginning with `git config --global` return nothing in the terminal. You can check that Git understood what you typed by looking at the output of the third from `git config --global --list`.

### Configure the Git editor {#git-editor}

Another Git option that many people eventually configure is the editor. At some point, you will fail to give Git what it wants in terms of a commit message and it will kick you into an editor. This can be distressing, if it's not your editor of choice and you don't even know how to save and quit. You can enforce your will with something along these lines:

``` bash
git config --global core.editor "emacs"
```

Substitute your preferred editor for `"emacs"` here. Software Carpentry's Git lesson has a comprehensive listing of the exact `git config` command needed for [many combinations of OS and editor](https://swcarpentry.github.io/git-novice/02-setup.html).

### Configure the default name for an initial branch

You may also want to configure the default name for the initial branch in a new repo.
Historically, this has been `master`, as that was baked into Git itself.
It's increasingly common to use `main` instead, but you have to opt-in to this.

In 2020, the `init.defaultBranch` setting was introduced so that this became user-configurable.
Shortly thereafter, major Git hosts like GitHub and GitLab made `main` the default initial branch name for repos created on their platforms and also provided considerable support for renaming existing default branches.

You can set your default initial branch name to `main` like so, in the shell:

``` bash
git config --global init.defaultBranch main
```

or from R (the default for `name` is `"main"`):


``` r
usethis::git_default_branch_configure()
```

<!--chapter:end:install-introduce-self-git.Rmd-->

# Install a Git client {#git-client}

This is optional but **highly recommended**.

Learning to use version control can be rough at first. I found the use of a GUI – as opposed to the command line – extremely helpful when I was getting started. I call this sort of helper application a Git client. It's really a Git(Hub) client because it also helps you interact with GitHub or other remotes.

A Git client is not required for live workshops and will not be explicitly taught, though you might see us using one of these clients.

## What is a Git client? Why would you want one?

"Git" is really just a collection of individual commands you execute in the shell (Appendix \@ref(shell)). This interface is not appealing for everyone. Some may prefer to do Git operations via a client with a graphical interface.

Git and your Git client are not the same thing, just like R and RStudio are not the same thing. A Git client and an [integrated development environment](https://en.wikipedia.org/wiki/Integrated_development_environment), such as RStudio, are not necessary to use Git or R, respectively. But they make the experience more pleasant because they reduce the amount of "command line bullshittery"[^1] and provide a richer visual representation of the current state.

[^1]: This evocative phrase originally appeared in a blog post by Philip Guo, which has subsequently been removed from the internet.

RStudio offers a very basic Git client via its Git pane. I use this often for simple operations, but you probably want another, more powerful one as well.

Fair warning: for some tasks, you must use the command line. But the more powerful your Git client is, the less often this happens. The visual overview given by your Git client can also be invaluable for understanding the current state of things, even when preparing calls to command line Git. 

Fantastic news: because all of the clients are just forming and executing Git commands on your behalf, you don't have to pick one.
You can literally do one operation from the command line, do another from RStudio, and another from GitKraken, one after the other, and it just works.
*Very rarely, both clients will scan the repo at the same time and you'll get an error message about `.git/index.lock`.
Try the operation again at least once before doing any further troubleshooting.*

## A picture is worth a thousand words

Here's a screenshot of GitKraken (see below) open to the repository for the R package [pkgdown](https://pkgdown.r-lib.org).
You get a nice graphical overview of the recent commit history, branches, and diffs, as well as a GUI that facilitates the most common Git operations.


\begin{center}\includegraphics[width=1\linewidth]{img/gitkraken-pkgdown-screenshot} \end{center}

In contrast, here's a shell session where I've used command line Git to access some of the same information.

```console
jenny@jennys-MacBook-Pro pkgdown % git log --oneline -n 10
cd888bed (HEAD -> master, upstream/master, upstream/HEAD, r-lib/master, r-lib/HEAD) Remove accidentally committed snapshot
ca01d386 Add a skip link (#1833)
1f07a145 Include section class in generated subsection divs
26e1dcf2 Restore code colouring
77503979 Working on docs (#1828)
3c805e1a Make anchor tweaking stricter
a6ae3ca4 use_tidy_description()
d43260fb Tweak authors order
41c855df Tweak details styling
7d3c484c Anchor & news tweaks (#1830)
```

Which do you prefer?

## No one is giving out Git Nerd merit badges

Work with Git in whatever way makes you most effective.
Feel free to revisit your approach over time or to use different approaches for different tasks or in different settings.
No one can tell whether you use the command line or a GUI when they look at your Git history or your GitHub repo.

I sometimes encounter people who feel it's "better" to use command line Git, but for very ill-defined reasons.
These people may feel like they *should* work in the shell, even if it leads to Git-avoidance, frequent mistakes, or limiting themselves to a small set of ~3 Git commands.
This is counterproductive.

I had two false starts with Git, where I failed to get proficient enough, quickly enough to truly incorporate version control into my daily work.
I found a visual Git client invaluable.
It made me willing to use Git multiple times per day, for a sustained period of time.
This helped me build the mental model necessary for more advanced Git operations like rebasing, cherry-picking, and resetting.

If your Git life happens on your own computer, there is no reason to deny yourself a GUI if that's what you like.
If you prefer working in the shell or if you frequently log into a remote server, then it makes sense to prioritize building Git skills at the command line.
Do whatever works for you, but don't do anything for the sake of purity or heroism.

## Recommended Git clients

  * [GitKraken](https://www.gitkraken.com) is a free, powerful Git(Hub) client that is my current favorite. It's especially exciting because it works on Windows, macOS, and Linux. This is great news, especially for long-suffering Linux users who previously had very few options. I used the free for version for years, which works great, but now I happily pay money for the pro version.

  * [SourceTree](https://www.sourcetreeapp.com) is another free client that I used to highly recommend. It was my first beloved Git client, but I eventually had to give it up, due to long-standing bugs / deficiencies that seemed like they would never be fixed ([macOS bug re: leaking file handles](http://openradar.appspot.com/radar?id=1387401), no ability to control font size). GitKraken feels much more actively developed and has completely supplanted SourceTree for me.
  
  * GitHub offers a free Git(Hub) client, [GitHub Desktop](https://desktop.github.com/), for Windows and macOS. Although we previously discouraged its use, GitHub's client has since gotten a thorough makeover that eliminates several of our concerns, so we're cautiously optimistic. GitHub Desktop is aimed at beginners who want the most useful features of Git front and center. The flipside is that it may not support some of the more advanced workflows exposed by the clients above and, consequently, may not develop your mental model of Git as thoroughly.

  * Browse [even more Git(Hub) clients](http://git-scm.com/downloads/guis).

<!--chapter:end:install-git-client.Rmd-->

# (PART) Connect Git, GitHub, RStudio {-} 

# Can you hear me now? {#connect-intro .unnumbered}

The next few chapters walk through some basic operations to confirm you have installed the necessary software and that the necessary connections are being made, between tools on your computer and between your computer and GitHub.

This has a lot of overlap with some basic workflows we revisit later, but the second time around (or in a live workshop), we'll spend more time explaining what's happening and why.

Unfortunately, we have to front-load a rather fiddly task, which is to decide whether to communicate with GitHub via HTTPS or SSH and setup some credentials accordingly.
In [Personal access token for HTTPS] we discuss how to choose between HTTPS and SSH and then walk through obtaining a personal access token, which is used with HTTPS.
Or, alternatively, we will help you [Set up keys for SSH].

Once we have our credentials sorted out, in [Connect to GitHub], we use Git in the shell to make sure you can clone a repo from GitHub and establish two-way communications, i.e. pull and push.

In [Connect RStudio to Git and GitHub] we confirm that RStudio can work with your Git installation to perform local operations and communicate with GitHub.

Hopefully you won't need it, but this part concludes with two troubleshooting chapters: [Detect Git from RStudio] and [RStudio, Git, GitHub Hell].

<!--chapter:end:connect-intro.Rmd-->

# Personal access token for HTTPS {#https-pat}

When we interact with a remote Git server, such as GitHub, we have to include credentials in the request.
This proves we are a specific GitHub user, who's allowed to do whatever we're asking to do.

Git can communicate with a remote server using one of two protocols, HTTPS or SSH, and the different protocols use different credentials.

Here we describe the credential setup for the HTTPS protocol, which is what we recommend if you have no burning reason to pick SSH.
With HTTPS, we will use a **personal access token (PAT)**.
Head over to chapter \@ref(ssh-keys) if you really want to set up SSH keys.

Let it be known that the password that you use to login to GitHub's website is NOT an acceptable credential when talking to GitHub as a Git server.
This was possible in the past (and may yet be true for other Git servers), but those days are over at GitHub.
You can learn more in their blog post [Token authentication requirements for Git operations](https://github.blog/2020-12-15-token-authentication-requirements-for-git-operations/).

Here's the error you'll see if you try to do that now:

```console
remote: Support for password authentication was removed on August 13, 2021. Please use a personal access token instead.
remote: Please see https://github.blog/2020-12-15-token-authentication-requirements-for-git-operations/ for more information.
fatal: Authentication failed for 'https://github.com/OWNER/REPO.git/'
```

The recommendation to use a personal access token (PAT) is exactly what we cover in this chapter.

## TL;DR

This is a very minimal account of getting and storing a PAT.
This might be all you need when you're first getting yourself set up.
You can always come back later and read other parts of this chapter.

Go to <https://github.com/settings/tokens> and click "Generate token".

Or, from R, do:


``` r
usethis::create_github_token()
```

Look over the scopes; I highly recommend selecting "repo", "user", and "workflow".
Recommended scopes will be pre-selected if you used `create_github_token()`.

Click "Generate token".

Copy the generated PAT to your clipboard.
Or leave that browser window open and available for a little while, so you can come back to copy the PAT.

Provide this PAT next time a Git operation asks for your password[^pat-not-password].

[^pat-not-password]: Yes, it's confusing that you might be prompted for a password, but you should enter your PAT.
GitHub no longer allows passwords in this context, but most basic Git tools still frame the authentication task with this language.

You could even get out ahead of this and store the PAT explicitly right now.
In R, call `gitcreds::gitcreds_set()` to get a prompt where you can paste your PAT:


``` sh
> gitcreds::gitcreds_set()

? Enter password or token: ghp_xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
-> Adding new credentials...
-> Removing credentials from cache...
-> Done.
```

You should be able to work with GitHub now, i.e. push and pull.
If you're still doing your initial setup, now is a great time to move on to [Connect to GitHub](#push-pull-github).

Read on to learn more about:

* [How to decide between the HTTPS and SSH protocols](#https-vs-ssh)
* [PAT scopes, names, and expiration](#get-a-pat)
* [PAT storage](#store-pat)
* [Troubleshooting](#pat-troubleshooting)

## HTTPS versus SSH {#https-vs-ssh}

I find HTTPS easier to get working quickly and **strongly recommend** it when you first start working with Git/GitHub.
HTTPS is what GitHub recommends, presumably for exactly the same reasons.
The "ease of use" argument in favor of HTTPS is especially true for Windows users.
I started with HTTPS, preferred SSH for a while, and have returned to HTTPS.
The main thing to know is that this is not an all-or-nothing decision and it's a relatively easy decision to revisit later.

Another advantage of HTTPS is that the PAT we'll set up for that can also be used with GitHub's REST API.
That might not mean anything to you (yet), but there are many R packages that call GitHub's API on your behalf (devtools+usethis, remotes, pak, gh, etc.).
Configuring your PAT kills two birds with one stone: this single credential can be used to authenticate to GitHub as a regular Git server and for its REST API.
If you authenticate via SSH for "regular" Git work, you will still have to set up a PAT for work that uses the REST API.


\begin{center}\includegraphics[width=0.8\linewidth]{img/pat-kills-both-birds} \end{center}

A properly configured PAT means all of this will "just work":

  * Remote HTTPS operations via command line Git and, therefore, via RStudio
  * Remote HTTPS operations via the gert R package and, therefore, usethis
  * GitHub API operations via the gh R package and, therefore, usethis

### URL determines the protocol {#url-determines-protocol}

Even though I'm suggesting that you adopt HTTPS as a lifestyle, it's good to know that you actually have very granular control over the protocol.
It is determined by the URL used to access a remote repo.
Feel free to skip this section if you are new to Git (we mention some concepts and commands that won't make much sense 'til you've used Git a little).

HTTPS remote URLs look like `https://github.com/<OWNER>/<REPO>.git`.  
SSH remote URLs look like `git@github.com:<OWNER>/<REPO>.git`.


\includegraphics[width=0.49\linewidth,height=0.49\textheight]{img/github-https-url} \includegraphics[width=0.49\linewidth,height=0.49\textheight]{img/github-ssh-url} 

When you execute a command such as `git push origin my-cool-feature-branch`, Git looks up the URL you've stored for the `origin` remote and uses the protocol implicit in the URL's format.
The protocol is a game time decision.

This implies that:  

* It's fine to use HTTPS for one remote in a repo and SSH for another.  
* It's fine to use HTTPS in one repo and SSH in another.  
* It's fine to interact with a GitHub repo via HTTPS from one computer and via SSH from another.  
* It's fine to adopt HTTPS for new work, even if some of your pre-existing repos use SSH.  

You just have to be aware that mixed use of HTTPS and SSH means you'll have to configure both sorts of credentials.  

Changing a specific remote from HTTPS to SSH (and back again) is a straightforward operation with `git remote set-url REMOTE_NAME DESIRED_URL`:

```console
~/rrr/happy-git-with-r % git remote -v
origin  https://github.com/jennybc/happy-git-with-r.git (fetch)
origin  https://github.com/jennybc/happy-git-with-r.git (push)

~/rrr/happy-git-with-r % git remote set-url origin git@github.com:jennybc/happy-git-with-r.git

~/rrr/happy-git-with-r % git remote -v
origin  git@github.com:jennybc/happy-git-with-r.git (fetch)
origin  git@github.com:jennybc/happy-git-with-r.git (push)

~/rrr/happy-git-with-r % git remote set-url origin https://github.com/jennybc/happy-git-with-r.git
```

We can do the same from R using functions in usethis:


``` r
usethis::git_remotes()
#> $origin
#> [1] "https://github.com/jennybc/happy-git-with-r.git"

usethis::use_git_remote(
  "origin",
  "git@github.com:jennybc/happy-git-with-r.git",
  overwrite = TRUE
)

usethis::git_remotes()
#> $origin
#> [1] "git@github.com:jennybc/happy-git-with-r.git"

usethis::use_git_remote(
  "origin",
  "https://github.com/jennybc/happy-git-with-r.git",
  overwrite = TRUE
)
```

## Generate a personal access token (PAT) {#get-a-pat}

On github.com, assuming you're signed in, you can manage your personal access tokens from <https://github.com/settings/tokens>, also reachable via *Settings > Developer settings > Personal access tokens*.
You could click on "Generate new token" here or, perhaps even better, you could call `usethis::create_github_token()` from R:


``` r
usethis::create_github_token()
```

The usethis approach takes you to a pre-filled form where we have pre-selected some recommended scopes, which you can look over and adjust before clicking "Generate token".
At the time of writing, the usethis-recommended scopes are "repo", "user", "gist", and "workflow".


\begin{center}\includegraphics[width=1\linewidth]{img/new-personal-access-token-screenshot} \end{center}

It is a very good idea to describe the token's purpose in the *Note* field, because one day you might have multiple PATs.
We recommend naming each token after its use case, such as the computer or project you are using it for, e.g. "personal-macbook-air" or "vm-for-project-xyz".
In the future, you will find yourself staring at this list of tokens, because inevitably you'll need to re-generate or delete one of them.
Make it easy to figure out which token you've come here to fiddle with.

GitHub encourages the use of perishable tokens, with a default *Expiration* period of 30 days.
Unless you have a specific reason to fight this, I recommend accepting this default.
I assume that GitHub's security folks have good reasons for their recommendation.
But, of course, you can adjust the *Expiration* behaviour as you see fit, including "No expiration".

Once you're happy with the token's *Note*, *Expiration*, and *Scopes*, click "Generate token".

You won't be able to see this token again, so don't close or navigate away from this browser window until you store the PAT locally.
Copy the PAT to the clipboard, anticipating what we'll do next: trigger a prompt that lets us store the PAT in the Git credential store.

Treat this PAT like a password!
Do not ever hard-wire your PAT into your code!
A PAT should always be retrieved implicitly, for example, from the Git credential store.
We're about to help you store the PAT in a safe place, where command line Git, RStudio, and R packages can discover it.

If you use a password management app, such as 1Password or LastPass (highly recommended!), you might want to also add this PAT (and its *Note*) to the entry for GitHub, where you're already storing your username and password.
Storing your PAT in the Git credential store is a semi-persistent convenience, sort of like a browser cache or "remember me" on a website[^remember-me-haha] and it's conceivable you will need to re-enter your PAT in the future.
You could decide to embrace the impermanence of your PAT and, if it somehow goes missing, you'll just [re-generate the PAT and re-store it](#regenerate-pat).
If you accept the default 30-day expiration period, this is a workflow you'll be using often anyway.
But if you create long-lasting tokens or want to feel free to play around with the functions for setting or clearing your Git credentials, it can be handy to have your own record of your PAT in a secure place, like 1Password or LastPass.

[^remember-me-haha]: Haha! We all know how well "remember me" works.

## Store your PAT {#store-pat}

At this point, I assume you've generated a PAT and have it available, in one or both of these ways:

  * In a secure, long-term system for storing secrets, like 1Password or LastPass
  * For the next few minutes, in a browser window or on the clipboard

There are a couple ways to get your PAT into the Git credential store:

  * Call an R function to explicitly store (or update) your credentials.
  * Do something in command line Git or RStudio that triggers a credential
    challenge.

### Call an R function to store your credentials

There are two R packages for accessing the Git credential store:

  * [gitcreds](https://r-lib.github.io/gitcreds/)
  * [credentials](https://docs.ropensci.org/credentials/)
    
It is likely that these packages will eventually combine into one and, even now, they are largely interoperable.
You don't need to follow the instructions for both packages -- pick one!

#### gitcreds package

If you don't have gitcreds installed, install via `install.packages("gitcreds")`.
If you've installed usethis, you will already have gitcreds, because usethis uses gh and gh uses gitcreds.

Call `gitcreds::gitcreds_set()`.
If you don't have a PAT stored already, it will prompt you to enter your PAT. Paste!


``` sh
> gitcreds::gitcreds_set()

? Enter password or token: ghp_xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
-> Adding new credentials...
-> Removing credentials from cache...
-> Done.
```

If you already have a stored credential, `gitcreds::gitcreds_set()` reveals this and will even let you inspect it.
This helps you decide whether to keep the existing credential or replace it.
When in doubt, embrace a new, known-to-be-good credential over an old one, of dubious origins.


``` sh
> gitcreds::gitcreds_set()

-> Your current credentials for 'https://github.com':

  protocol: https
  host    : github.com
  username: PersonalAccessToken
  password: <-- hidden -->

-> What would you like to do? 

1: Keep these credentials
2: Replace these credentials
3: See the password / token

Selection: 2

-> Removing current credentials...

? Enter new password or token: ghp_xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
-> Adding new credentials...
-> Removing credentials from cache...
-> Done.
```

You can check that you've stored a credential with `gitcreds_get()`:


``` r
gitcreds_get()
#> <gitcreds>
#>   protocol: https
#>   host    : github.com
#>   username: PersonalAccessToken
#>   password: <-- hidden -->
```

Other functions that can help you feel confident about your PAT setup include:


``` r
usethis::gh_token_help()

usethis::git_sitrep()

gh::gh_whoami()
```

#### credentials package

If you don't have credentials installed, install via `install.packages("credentials")`.
If you've installed usethis, you will already have credentials, because usethis uses gert and gert uses credentials.

Call `set_github_pat()`.
If you don't have a PAT stored already, it will prompt you to enter your PAT. Paste!


``` r
credentials::set_github_pat()
```

If successful, your initial (and subsequent) calls will look like this:


``` r
credentials::set_github_pat()
#> If prompted for GitHub credentials, enter your PAT in the password field
#> Using GITHUB_PAT from Jennifer (Jenny) Bryan (credential helper: osxkeychain)
```

Other functions that can help you feel confident about your PAT setup include:


``` r
usethis::gh_token_help()

usethis::git_sitrep()

gh::gh_whoami()
```

### Store credentials through organic Git use

*Before gitcreds and credentials existed (see above), we had to orchestrate a credential challenge by setting up (and then tearing down) a toy repo.
That still occurs naturally in the guided exercise in [Connect to GitHub].
But I strongly recommend managing your PAT more directly and explicitly with
`gitcreds::gitcreds_set()` and related functions in gitcreds.*

## HTTPS PAT problems and solutions {#pat-troubleshooting}

This section is for people who need to know even more about PAT management, because they're in a nonstandard situation or troubleshooting.

### Valid PAT gets stored, but later told the PAT is invalid

Let's say you generate a fresh PAT and successfully store it as described above.
Maybe you even use it successfully.
But later, you're told your PAT is invalid!
How can this be?

Here are some likely explanations:

1. Your PAT truly is invalid. By default, PATs have an expiration date now. One
   day you really will wake up and find the PAT has gone bad overnight and you
   need to re-generate and re-store it.
1. You have an invalid PAT stored *somewhere else*, that you've forgotten about,
   probably in `.Renviron`. This old, invalid PAT is preventing R packages from
   even discovering your new, valid PAT.

#### PAT has expired {#regenerate-pat}

You are going to be re-generating and re-storing your PAT on a schedule dictated by its expiration period.
By default, once per month.

When the PAT expires, return to <https://github.com/settings/tokens> and click on its *Note*.
(You do label your tokens nicely by use case, right? Right?)
At this point, you can optionally adjust scopes and then click "Regenerate token".
You can optionally modify its *Expiration* and then click "Regenerate token" (again).
As before, copy the PAT to the clipboard, call `gitcreds::gitcreds_set()`, and paste!

Hopefully it's becoming clear why each token's *Note* is so important.
The actual token may be changing, e.g., once a month, but its use case (and scopes) are much more persistent and stable.

#### Old `GITHUB_PAT` in `.Renviron`

These usethis functions will diagnose this problem:


``` r
usethis::gh_token_help()

usethis::git_sitrep()
```

In the past, it was common to store a PAT as the `GITHUB_PAT` environment variable in `.Renviron`.
But now, thanks to gitcreds and credentials, we can store and retrieve a PAT, from R, the same way as command line Git does.

If you have any doubt about your previous practices, open `.Renviron`, look for a line setting the `GITHUB_PAT` environment variable, and delete it. `usethis::edit_r_environ()` can be helpful for getting `.Renviron` open for editing.
Don't forget to restart R for this change to take effect.

### PAT doesn't persist on macOS or Windows

The credential helpers used by Git take advantage of official OS-provided credential stores, where possible, such as macOS Keychain and Windows Credential Manager.

If you're trying to follow the advice here and your PAT never persists, consider that you may need to update Git to get its more modern credential helpers.
This is absolutely an area of Git that has improved rapidly in recent years and the gitcreds and credentials package work best with recent versions of Git.
I have not needed to explicitly activate a credential helper on macOS or Windows with any recent version of Git.

Here's a command to reveal the current credential helper and what I see these days.

macOS

```console
$ git config --show-origin --get credential.helper
file:/Users/jenny/.gitconfig    osxkeychain
```

Windows

```console
$ git config --show-origin --get credential.helper
file:C:/Program Files/Git/mingw64/etc/gitconfig manager
```

If you want to know how more about how gitcreds and credentials are managing your PAT, learn about [`git credential <fill|approve|reject>`](https://git-scm.com/docs/git-credential).
For keeners, that documentation gives you the gory details on how credentials are stored and retrieved:

> Git has an internal interface for storing and retrieving credentials from system-specific helpers, as well as prompting the user for usernames and passwords. The `git-credential` command exposes this interface to scripts which may want to retrieve, store, or prompt for credentials in the same manner as Git.

On Windows, your Git credentials are probably being stored via Credential Manager.

On macOS, your Git credentials are probably being stored in the Keychain.

If you really want to poke around directly to explore or clean out your GitHub credentials, launch Credential Manager (Windows) or Keychain Access (macOS) and search for "github.com".

### PAT doesn't persist on Linux

The credential helpers used by Git take advantage of official OS-provided 
credential stores on macOS and Windows, but sadly there is no exact equivalent on Linux.

The easiest thing to do is to configure Git to "cache" your credentials (vs "store"), which is more time-limited.
Then set the cache timeout to some suitably long period of time.
Here, we set the timeout to ten million seconds or around 16 weeks, enough for a semester.

```console
git config --global credential.helper 'cache --timeout=10000000'
```

This still may not make your PAT available to R packages.
In this case, you may need to use the older, less secure approach of storing your PAT in `.Renviron`.
`usethis::edit_r_environ()` opens that file for editing.


``` r
usethis::edit_r_environ()
```

Add a line like this, but substitute your PAT:


``` sh
GITHUB_PAT=ghp_xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
```

Make sure this file ends in a newline!
Lack of a newline can lead to silent failure to load startup files, which can be tricky to debug.
Take care that this file is not accidentally pushed to the cloud, e.g. Google Drive or GitHub.

Restart R for changes in `.Renviron` to take effect.

<!--chapter:end:connect-https-pat.Rmd-->

# Set up keys for SSH {#ssh-keys}

When we interact with a remote Git server, such as GitHub, we have to include credentials in the request.
This proves we are a specific GitHub user, who's allowed to do whatever we're asking to do.

Git can communicate with a remote server using one of two protocols, HTTPS or SSH, and the different protocols use different credentials.

Here we describe the credential setup for the SSH protocol.
If you're not sure whether to use HTTPS or SSH, please read [HTTPS versus SSH](#https-vs-ssh).
From now on, we assume you've made an intentional choice to set up SSH keys.

## SSH keys

SSH keys provide a more secure way of logging into a server than using a password alone. While a password can eventually be cracked with a brute force attack, SSH keys are nearly impossible to decipher by brute force alone. Generating a key pair provides you with two long strings of characters: a public and a private key. You can place the public key on any server (like GitHub!), and then unlock it by connecting to it with a client that already has the private key (your computer!). When the two match up, the system unlocks without the need for a password. You can increase security even more by protecting the private key with a passphrase.

Adapted from instructions provided by [GitHub](https://help.github.com/categories/ssh/) and [Digital Ocean](https://www.digitalocean.com/community/tutorials/how-to-set-up-ssh-keys--2).

## SSH outline and advice

High level overview of what must happen:

  * Create a public-private SSH key pair. Literally, 2 special files, in a special place. Optionally, encrypt the private key with a passphrase (best practice).
  * Add the private key to your ssh-agent. If you protected it with a passphrase, you may have additional configuration.
  * Add your public key to your GitHub profile.

Advice:

  * If you are new to programming and the shell, you'll probably find HTTPS easier at first (chapter \@ref(https-pat)). You can always switch to SSH later. You can use one method from computer A and the other from computer B.
  * You should swap out your SSH keys periodically. Something like once a year.
  * It's best practice to protect your private key with a passphrase. This can make setup and usage harder, so if you're not up for that (yet), either don't use a passphrase or seriously consider using HTTPS instead.
  * Don't do weird gymnastics in order to have only one key pair, re-used over multiple computers. You should probably have one key per computer (I do this). Some people even have one key per computer, per service (I do not do this).
  * It is normal to associate multiple public keys with your GitHub account. For example, one public key for each computer you connect with.

## Do you already have keys?

You can check this from RStudio or from the shell.

Global advice: if you do have existing keys, but have no clue where they came from or why you created them, you should seriously consider creating a new SSH key pair. It's up to you to figure out whether/how to delete the old ones. But don't let that keep you from creating new keys and moving forward.

### From RStudio

Go to *Tools > Global Options...> Git/SVN*. If you see something like `~/.ssh/id_rsa` in the SSH RSA Key box, you definitely have existing keys.

Caveat: RStudio only looks for a key pair named `id_rsa` and `id_rsa.pub`.
This makes sense, because historically that has been the most common.

However, these days both GitHub and GitLab are encouraging users to generate SSH keys with the Ed25519 algorithm, which results in a key pair named `id_ed25519` and `id_ed25519.pub`.
At the time of writing, RStudio will not display such a key pair, which can be confusing.
Therefore, it's probably a good idea to also check for existing keys in the shell.

### From the shell

Go to the shell (appendix \@ref(shell)).

List existing keys:

```console
ls -al ~/.ssh/
```

If you are told `~/.ssh/` doesn't exist, you don't have SSH keys!

If you see a pair of files like `id_rsa.pub` and `id_rsa` or `id_ed25519` and `id_ed25519.pub`, you have a key pair already.
The typical pattern is `id_FOO.pub` (the public key) and `id_FOO` (the private key), where `FOO` reflects the key type.
If you're happy to stick with your existing keys, skip to the sections about adding a key to the ssh-agent and GitHub.

## Create an SSH key pair

### Option 1: Set up from RStudio

Go to *Tools > Global Options...> Git/SVN > Create RSA Key...*.

RStudio prompts you for a passphrase. It is optional, but also a best practice. Configuring your system for smooth operation with a passphrase-protected key introduces more moving parts.
If you're completely new at all this, skip the passphrase (or use HTTPS!) and implement it next time, when you are more comfortable with system configuration.
I did not use a passphrase at first, but I do now, and record it in a password manager.

Click "Create" and RStudio will generate an SSH key pair, stored in the files `~/.ssh/id_rsa` and `~/.ssh/id_rsa.pub`.

Note that RStudio currently only generates RSA keys, whereas the standard recommendation by GitHub and GitLab is to use Ed25519 keys.
If you want to comply with that advice, generate your keys in the shell for now.

### Option 2: Set up from the shell

Create the key pair like so, but substitute a comment that means something to you, especially if you'll have multiple SSH keys in your life.
Consider the email associated with your GitHub account or the name of your computer or some combination, e.g. `your_email@example.com` or `macbook-pro` or `jane-2020-macbook-pro`.

```console
ssh-keygen -t ed25519 -C "DESCRIPTIVE-COMMENT"
```

If it appears that your system is too old to support the Ed25519 algorithm, do this instead:

```console
ssh-keygen -t rsa -b 4096 -C "DESCRIPTIVE-COMMENT"
```

Accept the proposal to save the key in the default location.
Just press Enter here:

```console
Enter file in which to save the key (/Users/jenny/.ssh/id_ed25519):
```

You have the option to protect the key with a passphrase.
It is optional, but also a best practice.
Configuring your system for smooth operation with a passphrase-protected key introduces more moving parts.
If you're completely new at all this, skip the passphrase and implement it next time, when you are more comfortable with system configuration.
I did not use a passphrase at first, but I do now, and record it in a password manager.

```console
Enter passphrase (empty for no passphrase):
Enter same passphrase again: 
```

The process should complete now and should have looked like this:

```console
~ % ssh-keygen -t ed25519 -C "jenny-2020-mbp"        
Generating public/private ed25519 key pair.
Enter file in which to save the key (/Users/jenny/.ssh/id_ed25519): 
Enter passphrase (empty for no passphrase): 
Enter same passphrase again: 
Your identification has been saved in /Users/jenny/.ssh/id_ed25519.
Your public key has been saved in /Users/jenny/.ssh/id_ed25519.pub.
The key fingerprint is:
SHA256:XUEaY/elhcQJz3M9jx/SdC0zh10lCA7uNpqgkm5G/R0 jenny-2020-mbp
The key's randomart image is:
+--[ED25519 256]--+
|        . =o==oo*|
|       . + =.=+B+|
|        . o . @oB|
|       . . .  oO+|
|  . .   S .  ..o.|
| o o . E .    ...|
|+ . . + .       .|
|.+   . .         |
|o.               |
+----[SHA256]-----+
```

### Add key to ssh-agent

Tell your ssh-agent about the key and, especially, set it up to manage the passphrase, if you chose to set one.

Things get a little OS-specific around here.
When in doubt, consult [GitHub's instructions for SSH](https://docs.github.com/en/authentication/connecting-to-github-with-ssh), which is kept current for Mac, Windows, and Linux.
It also accounts for more unusual situations than I can.

#### Mac OS

Make sure ssh-agent is enabled. Here's what success look like (the `pid` will vary):

```console
~ % eval "$(ssh-agent -s)"
Agent pid 15360
```

Sometimes this fails like so:

```console
~ % eval "$(ssh-agent -s)"
mkdtemp: private socket dir: No such file or directory
```

A similar failure might be reported as "Permission denied".
You should try again, but as the superuser.
Don't forget to use `exit` to go back to your normal user account, when you are done!

```console
~ % sudo su
Password:
sh-3.2# eval "$(ssh-agent -s)"
Agent pid 15385
sh-3.2# exit
exit
```

Add your key to the ssh agent.
If you set a passphrase, you'll be challenged for it here.
Give it.
The `-K` option stores your passphrase in the keychain.

```console
~ % ssh-add -K ~/.ssh/id_ed25519
Enter passphrase for /Users/jenny/.ssh/id_ed25519: 
Identity added: /Users/jenny/.ssh/id_ed25519 (jenny-2020-mbp)
```

If you're on macOS Sierra 10.12.2 and higher, you need to do one more thing.
Create a file `~/.ssh/config` with these contents:

```bash
Host *
  AddKeysToAgent yes
  UseKeychain yes
  IdentityFile ~/.ssh/id_ed25519
```

You can omit the line about `UseKeychain` if you didn't use a passphrase.
But if you did, this should store your passphrase *persistently* in the keychain.
Otherwise, you will have to enter it every time you log in.
Useful StackOverflow thread: [How can I permanently add my SSH private key to Keychain so it is automatically available to ssh?](https://apple.stackexchange.com/questions/48502/how-can-i-permanently-add-my-ssh-private-key-to-keychain-so-it-is-automatically).

#### Windows

In a Git Bash shell, make sure ssh-agent is running:

```console
$ eval $(ssh-agent -s)
Agent pid 59566
```

Add your key, substituting the correct name for your key.

```console
$ ssh-add ~/.ssh/id_ed25519
```

#### Linux

In a shell, make sure ssh-agent is running:

```console
$ eval "$(ssh-agent -s)"
Agent pid 59566
```

Add your key, substituting the correct name for your key.

```console
ssh-add ~/.ssh/id_ed25519
```

## Provide public key to GitHub

Now we store a copy of your public key on GitHub.

### RStudio to clipboard

Go to *Tools > Global Options...> Git/SVN*.
If your key pair is named like `id_rsa.pub` and `id_rsa`, RStudio will see it and offer to "View public key".
Do that and accept the offer to copy to your clipboard.

If your key pair is named differently, such as `id_ed25519.pub` and `id_ed25519`, you'll have to copy the public key another way.

### Shell to clipboard

Copy the public key onto your clipboard.
For example, open `~/.ssh/id_ed25519.pub` in an editor and copy the contents to your clipboard.
Or do one of the following at the command line:

  * Mac OS: `pbcopy < ~/.ssh/id_ed25519.pub`
  * Windows: `clip < ~/.ssh/id_ed25519.pub`
  * Linux: `xclip -sel clip < ~/.ssh/id_ed25519.pub`

Linux: if needed, install `xclip` via `apt-get` or `yum`. For example, `sudo apt-get install xclip`.

### On GitHub

Now we register the public key with GitHub.
Click on your profile pic in upper right corner and go to *Settings > SSH and GPG keys*.
Click "New SSH key".
Paste your public key in the "Key" box.
Give it an informative title, presumably repeating the descriptive comment you used above, during key creation.
Click "Add SSH key".

In theory, we're done!
You can use [`ssh -T git@github.com`](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/testing-your-ssh-connection) to test your connection to GitHub.
If you're not sure what to make of the output, see the link for details.
Of course, the best test is to work through the realistic usage examples elsewhere in this guide.

## Troubleshooting {#ssh-troubleshooting}

### HTTPS URL when you meant to use SSH

If you think you have SSH set up correctly and yet you are still challenged for credentials, consider this: for the repo in question, have you possibly set up GitHub, probably called `origin`, as an HTTPS remote, instead of SSH?

How to see the remote URL(s) associated with the current repo in the shell:

```console
git remote -v
```

An SSH remote will look like this:

```console
git@github.com:USERNAME/REPOSITORY.git
```

whereas an HTTPS remote will look like this:

```console
https://github.com/USERNAME/REPOSITORY.git
```

You can fix this with `git remote set-url`, which is demonstrated in [URL determines the protocol](#url-determines-protocol).

### git2r -- or some other tool -- can't find SSH keys on Windows

Have you seen this error message?

```console
Error in .local(object, ...) : 
  Error in 'git2r_push': error authenticating: failed connecting agent
```

We've seen it when working with Git/GitHub from R via the [git2r](https://cran.r-project.org/web/packages/git2r/index.html) package.

The root cause is confusion about the location of `.ssh/` on Windows.
R's idea of your home directory on Windows often differs from the default location of config files for Git and ssh, such as `.ssh/`.
On *nix systems, these generally coincide and there's no problem.

Two important directories on Windows are the user's HOME and USERPROFILE.
R usually associates `~` with HOME, but Git and ssh often consult USERPROFILE for their config files.
On my Windows 10 VM, I see:


``` r
normalizePath("~")
#> [1] "C:\\Users\\JennyVM\\Documents"

as.list(Sys.getenv(
  c("HOME", "USERPROFILE")
))
#> $HOME
#> [1] "C:/Users/JennyVM/Documents"
#> 
#> $USERPROFILE
#> [1] "C:\\Users\\JennyVM"

list.files(
  Sys.getenv("USERPROFILE"),
  pattern = "ssh|git",
  include.dirs = TRUE,
  all.files = TRUE
)
#> [1] ".gitconfig" ".ssh"
```

Two workarounds:

  * Tell git2r explicitly where to find your public and private key and pass the resulting `cred` object to your git2r calls.
  
    
    ``` r
    cred <- git2r::cred_ssh_key(
      publickey = "~/../.ssh/id_rsa.pub",
      privatekey = "~/../.ssh/id_rsa"
    )
    ```
  * [Create a symbolic link](https://www.howtogeek.com/howto/16226/complete-guide-to-symbolic-links-symlinks-on-windows-or-linux/) so that `.ssh/` in R's home directory points to your actual `.ssh/` directory. Example contributed by Ian Lyttle on Windows 7 using Command Prompt:
  
    ```console
    MKLINK /D "C:\Users\username\Documents\.ssh" "C:\Users\username\.ssh"
    ```
    
Finally, if git2r seems unable to get your SSH passphrase from ssh-agent, install the getPass package:


``` r
install.packages("getPass")
```

and git2r should launch a popup where you can enter your passphrase.
Thanks to Ian Lyttle for this tip.

This link provides a great explanation of the uncertainty about where `.ssh/` and user's `.gitconfig` are located on Windows: [git on Windows - location of configuration files](https://www.onwebsecurity.com/configuration/git-on-windows-location-of-global-configuration-file.html).
Bottom line: place your config and keys where your main tool expects them to be and create symbolic links to help other tools find this stuff.

### Other

Other things to double-check:

  * Did you add the SSH to your ssh-agent?
  * Did you configure Mac OS Sierra or High Sierra to persistently store your passphrase in the keychain?
  * Did you add the public key to GitHub?

<!--chapter:end:connect-ssh-keys.Rmd-->

# Connect to GitHub {#push-pull-github}

Objective: make sure that you can pull from and push to GitHub from your computer.

I do not explain all the shell (Appendix \@ref(shell)) and Git commands in detail.
This is a black box diagnostic / configuration exercise.
In later chapters and in live workshops, we revisit these operations with much more narrative and discussion of alternative workflows.

I assume you've decided whether to use HTTPS (see chapter \@ref(https-pat)) or SSH (see chapter \@ref(ssh-keys)) and you've prepared your credential. 

## Make a repo on GitHub


Go to <https://github.com> and make sure you are logged in.

Near "Repositories", click the big green "New" button.
Or, if you are on your own profile page, click on "Repositories", then click the big green "New" button.

How to fill this in:

* Repository template: No template.
* Repository name: `myrepo` or whatever you wish (we'll delete this soon).
* Description: "Repository for testing my Git/GitHub setup" or similar. It's nice to have something here, so you'll see it appear in the README.
* Public.
* Initialize this repository with: Add a README file.

Click the big green button that says "Create repository".

Now click the big green button that says "<> Code".

Copy a clone URL to your clipboard.
If you're taking our default advice, copy the HTTPS URL.
But if you're opting for SSH, then make sure to copy the SSH URL.


\begin{center}\includegraphics[width=0.6\linewidth]{img/github-https-or-ssh-url-annotated} \end{center}

## Clone the repo to your local computer {#git-clone-command-line}

We have a few ways to do this.
Here we use command line Git.
In section \@ref(new-github-first), we show other methods that you might prefer in daily life:
using usethis or the RStudio IDE.

Go to the shell (Appendix \@ref(shell)).

Take charge of -- or at least notice! -- what directory you're in.
`pwd` displays the working directory.
`cd` is the command to change directory.
Personally, I would do this sort of thing in `~/tmp`.

Clone `myrepo` from GitHub to your computer.
Use the URL we just copied from GitHub.
This URL should have **your GitHub username** and the name of **your practice repo**.
If your shell (Appendix \@ref(shell)) cooperates, you should be able to paste the whole `https://....` bit that we copied above.
But some shells are not (immediately) clipboard aware.
In that sad case, you must type it. **Accurately.**

```console
git clone https://github.com/YOUR-USERNAME/YOUR-REPOSITORY.git
```
        
This should look something like this:

```console
~/tmp % git clone https://github.com/jennybc/myrepo.git
Cloning into 'myrepo'...
remote: Enumerating objects: 3, done.
remote: Counting objects: 100% (3/3), done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
Receiving objects: 100% (3/3), done.
```

Make this new repo your working directory, list its files, display the README, and get some information on its connection to GitHub:

```console
cd myrepo
ls
head README.md
git remote show origin
```

This should look something like this:

``` bash
~/tmp % cd myrepo

~/tmp/myrepo % ls
README.md

~/tmp/myrepo % head README.md 
# myrepo
checking stuff for Happy Git

~/tmp/myrepo % git remote show origin
* remote origin
  Fetch URL: https://github.com/jennybc/myrepo.git
  Push  URL: https://github.com/jennybc/myrepo.git
  HEAD branch: main
  Remote branch:
    main tracked
  Local branch configured for 'git pull':
    main merges with remote main
  Local ref configured for 'git push':
    main pushes to main (up to date)
```

## Make a local change, commit, and push

Add a line to README and verify that Git notices the change:

```console
echo "A line I wrote on my local computer  " >> README.md
git status
```

This should look something like this:

```console
~/tmp/myrepo % echo "A line I wrote on my local computer" >> README.md

~/tmp/myrepo % git status
On branch main
Your branch is up to date with 'origin/main'.

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   README.md

no changes added to commit (use "git add" and/or "git commit -a")
```

Stage ("add") and commit this change and push to your remote repo on GitHub.

If you're a new GitHub user and using HTTPS, you might be challenged for your username and password.
Even though GitHub no longer allows username/password authentication, many general Git tools still frame the authentication task with this vocabulary.
By all means, provide your GitHub username when prompted.
However, the most critical piece is to **provide your PAT as the password**.
Do not enter your web password.
Enter your PAT.
If you already stored your PAT with `gitcreds::gitcreds_set()`, it should be discovered automatically and you will not see a credential challenge.

```console
git add README.md
git commit -m "A commit from my local computer"
git push
```

This should look something like this:

```console
~/tmp/myrepo % git add README.md

~/tmp/myrepo % git commit -m "A commit from my local computer"
[main e92528c] A commit from my local computer
 1 file changed, 1 insertion(+)
 
~/tmp/myrepo % git push
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 12 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 327 bytes | 327.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
To https://github.com/jennybc/myrepo.git
   31dcaef..e92528c  main -> main
```

Do you see an error like this?

```console
~/tmp/myrepo % git push                                                     
remote: Support for password authentication was removed on August 13, 2021. Please use a personal access token instead.
remote: Please see https://github.blog/2020-12-15-token-authentication-requirements-for-git-operations/ for more information.
fatal: Authentication failed for 'https://github.com/jennybc/myrepo.git/'
```

This means you have provided your GitHub _web password_, instead of your _personal access token_ (PAT).
Go back to chapter \@ref(https-pat) to get a PAT.
Try `git push` again and hopefully you'll get another prompt, allowing you to correct things and provide your PAT.

If you ever feel you need to overwrite a bad credential with a new one, the easiest way to do this is to call `gitcreds::gitcreds_set()` from R.

### Windows and line endings

On Windows, you might see a message about `LF will be replaced by CRLF`. This is normal and does not require any action on your part.
Windows handles line endings differently from other operating systems, but the default setup for Git for Windows is appropriate for most people and situations.

Here's a command to reveal the current line ending configuration and some typical output **on Windows**:

```console
$ git config --show-origin --get core.autocrlf
file:"C:\\ProgramData/Git/config"      true
```

If your value shows as `false`, you can set it to `true` with this command:

```console
$ git config --global core.autocrlf true
```

`true` is the current default setting for `core.autocrlf` for [Git for Windows](#install-git-windows), our recommended method for installing Git on Windows.
The need to set this explicitly in your global user config suggests you should consider reinstalling or updating Git for Windows.

## Confirm the local change propagated to the GitHub remote

Go back to the browser.
I assume we're still viewing your new GitHub repo.

Refresh.

You should see the new "A line I wrote on my local computer" in the README.

If you click on "commits," you should see one with the message "A commit from my local computer."

If you have made it this far, you and your test repo are ready to graduate to using Git and GitHub with RStudio (chapter \@ref(rstudio-git-github)).

## Clean up

If you're ready to conclude this test of your Git installation and GitHub configuration, we can clean up the test repository now.

**Local** When you're ready to clean up, you can delete the local repo any way you like. It's just a regular directory on your computer.

Here's how to do that in the shell, if current working directory is `myrepo`:

```console
cd ..
rm -rf myrepo/
```

**GitHub** In the browser, go to your repo's landing page on GitHub.
Click on "Settings".

Scroll down, click on "delete repository," and do as it asks.

<!--chapter:end:connect-git-github.Rmd-->

# Connect RStudio to Git and GitHub {#rstudio-git-github}

Here we verify that RStudio can issue Git commands on your behalf. 
Assuming that you've gotten local Git to talk to GitHub, this means you'll also be able to pull from and push to GitHub from RStudio.

In later chapters and in live workshops, we revisit these operations with much more explanation.

If you succeed here, your set up is DONE.

## Prerequisites

We assume the following: 

  * You've registered a free GitHub account (chapter \@ref(github-acct)).
  * You've installed/updated R and RStudio (chapter \@ref(install-r-rstudio)).
  * You've installed Git (chapter \@ref(install-git)).
  * You've introduced yourself to Git (chapter \@ref(hello-git)).
  * You've confirmed that you can push to / pull from GitHub from the command line (chapter \@ref(push-pull-github)).
  
You will also need a test repository on GitHub.
If you don't have a suitable test repository on GitHub, follow the instructions in the next section.

If you just completed the previous chapter, [Connect to GitHub], that repo will be perfect!
However, I encourage you to delete the *local* repository, so you can experience how we use RStudio to clone it and get a local copy.
This is a actually a workflow we refer to elsewhere (see \@ref(burn) as "burn it all down".
It's a deeply pragmatic coping strategy if your local Git repo is goofed up, but the version on GitHub is pretty current.

Delete the folder corresponding to the **local repo** any way you like.
It's just a regular directory on your computer.
Here's how to do that in the shell, if current working directory is `myrepo`:

```console
cd ..
rm -rf myrepo/
```

## Make a repo on GitHub


Go to <https://github.com> and make sure you are logged in.

Near "Repositories", click the big green "New" button.
Or, if you are on your own profile page, click on "Repositories", then click the big green "New" button.

How to fill this in:

* Repository template: No template.
* Repository name: `myrepo` or whatever you wish (we'll delete this soon).
* Description: "Repository for testing my Git/GitHub setup" or similar. It's nice to have something here, so you'll see it appear in the README.
* Public.
* Initialize this repository with: Add a README file.

Click the big green button that says "Create repository".

Now click the big green button that says "<> Code".

Copy a clone URL to your clipboard.
If you're taking our default advice, copy the HTTPS URL.
But if you're opting for SSH, then make sure to copy the SSH URL.


\begin{center}\includegraphics[width=0.6\linewidth]{img/github-https-or-ssh-url-annotated} \end{center}

## Clone the test GitHub repository to your computer via RStudio

In RStudio, start a new Project:

  * *File > New Project > Version Control > Git*. In "Repository URL", paste the URL of your new GitHub repository. It will be something like this `https://github.com/jennybc/myrepo.git`.
    - Do you NOT see an option to get the Project from Version Control? Restart RStudio and try again. Still no luck? Go to chapter \@ref(rstudio-see-git) for tips on how to help RStudio find Git.
  * Accept the default project directory name, e.g. `myrepo`, which coincides with the GitHub repo name.
  * Take charge of -- or at least notice! -- where the Project will be saved locally. A common rookie mistake is to have no idea where you are saving files or what your working directory is. Pay attention. Be intentional. Personally, I would do this in `~/tmp`.
  * I suggest you check "Open in new session", as that's what you'll usually do in real life.
  * Click "Create Project".

You should find yourself in a new local RStudio Project that represents your test repo on GitHub.
This should download the `README.md` file from GitHub.
Look in RStudio's file browser pane for the `README.md` file.

## Make local changes, save, commit

From RStudio, modify the `README.md` file, e.g., by adding the line "This is a line from RStudio". Save your changes.

Commit these changes to your local repo. How?

From RStudio:

  * Click the "Git" tab in upper right pane.
  * Check "Staged" box for `README.md`.
  * If you're not already in the Git pop-up, click "Commit".
  * Type a message in "Commit message", such as "Commit from RStudio".
  * Click "Commit".

## Push your local changes online to GitHub
  
Click the green "Push" button to send your local changes to GitHub.

You should not experience a credential challenge, since one of the pre-requisites was successfully pushing to GitHub from the command line (chapter \@ref(push-pull-github)).
RStudio's Git pane just exposes a specific subset of command line Git and therefore once your credentials work in the shell, they should work in RStudio.
If you do experience a credential challenge, that suggests you should have a look at the troubleshooting suggestions for your chosen protocol, either [HTTPS](#pat-troubleshooting) or [SSH](#ssh-troubleshooting).

## Confirm the local change propagated to the GitHub remote

Go back to the browser.
I assume we're still viewing your new GitHub repo.

Refresh.

You should see the new "This is a line from RStudio" in the README.

If you click on "commits", you should see one with the message "Commit from RStudio".

If you have made it this far, you are DONE with set up.
Congratulations!

## Clean up

Quit the RStudio instance that's open to your test Project / Git repo.

Delete the local repo any way you like.
It's just a regular directory on your computer.

Here's how to do that in the shell, if current working directory is `myrepo`:

```console
cd ..
rm -rf myrepo/
```

In the browser, go to your repo's landing page on GitHub.
Click on "Settings".

Scroll down, click on "delete repository," and do as it asks.

<!--chapter:end:connect-rstudio-git-github.Rmd-->

# Detect Git from RStudio {#rstudio-see-git}

If you want RStudio to help with your Git and GitHub work, it must be able to find the Git executable.

This usually "just works", so this page is aimed at people who have reason to suspect they have a problem.

This is something you set up once-per-computer.

## Do you have a problem?

Let's check if RStudio can find the Git executable.

  * *File > New Project...* Do you see an option to create from Version Control? If yes, good.
  * Select *New Directory* > *Empty Project*. Do you see a checkbox "Create a git repository"? If yes, good, CHECK IT.

Keep reading if things don't go so well or you want to know more.

## Find Git yourself

RStudio can only act as a GUI front-end for Git if Git has been successfully installed (chapter \@ref(install-git)) **AND RStudio can find it**.

A basic test for successful installation of Git is to simply enter `git` in the shell (Appendix \@ref(shell)).
If you get a complaint about Git not being found, it means installation was unsuccessful or that it is not being found, i.e. it is not on your `PATH`.

If you are not sure where the Git executable lives, try this in a shell:
  
* `which git` (Mac, Linux, Git Bash shell on Windows)

* `where git` (Windows command prompt, i.e. `cmd.exe`)

## Tell RStudio where to find Git

If Git appears to be installed and findable, launch RStudio.
Quit and re-launch RStudio if there's **any doubt in your mind** about whether you opened RStudio before or after installing Git.
Don't make me stop this car and restart RStudio for you in office hours.
DO IT.

From RStudio, go to *Tools > Global Options > Git/SVN* and make sure that the box *Git executable* points to your Git executable.

On macOS and Linux, the path usually looks something like this:

```console
/usr/bin/git
```

If you need to set this on macOS, it can sometimes be hard to navigate to the necessary directory, once you've clicked "Browse" and are working with a Finder-type window.
The keyboard shortcut "command + shift + g" will summon "Go To Folder", where you will be able to type or paste any path you want.

On Windows, this path should look something like this:

``` bash
C:/Program Files/Git/bin/git.exe
```

and here is a screenshot on Windows:


\begin{center}\includegraphics[width=1\linewidth]{img/windows-rstudio-git-executable-screenshot} \end{center}

**WARNING**: On Windows, do __NOT__ use `C:/Program Files/Git/cmd/git.exe`. `bin` in the path is GOOD YES!
`cmd` in the path is BAD NO!

**WARNING**: On Windows, do __NOT__ set this to `git-bash.exe`.
Something that ends in `git.exe` is GOOD YES! `git-bash.exe` is BAD NO!
  
**Restart RStudio if you make any changes here.**
Don't make me stop this car again and restart RStudio for you in office hours.
DO IT.

Re-do the steps at the top of the page to see if RStudio and Git are communicating now.

No joy?

  * I've seen this help: With your Project open, go to `Tools > Project Options...`. If available, click on "Git/SVN" and select "Git" in the Version control system dropdown menu. Answer "yes" to the "Confirm New Git Repository" pop up. Answer "yes" to the "Confirm Restart RStudio" pop up.

  * If you installed Git via GitHub for Windows, it is possible the Git executable is really well hidden. Get help or use one of [our recommended methods of installing Git](#install-git).

  * Your `PATH` is probably not set up correctly and/or you should re-install Git and control/notice where it's going. Read more in \@ref(troubleshooting).

  * Get our help.

<!--chapter:end:connect-can-rstudio-use-git.Rmd-->

# RStudio, Git, GitHub Hell {#troubleshooting}

Problems we have seen and possible solutions.

If you experience some new problem and, especially, find the corresponding solution, [we'd love to hear from you!](https://github.com/jennybc/happy-git-with-r/issues)

## I think I have installed Git but damn if I can find it

When you install Git, try to control or record where it is being installed!
Make a mental or physical note of these things.

You may be able to find Git after the fact with these commands in the shell (Appendix \@ref(shell)):

* `which git` (Mac, Linux, or anything running a bash shell)

* `where git` (Windows, when not in a bash shell)

It is not entirely crazy to just re-install Git, using a method that leaves it in a more conventional location, and to pay very close attention to where it's being installed.
Live and learn.

## RStudio Git pane disappears on Mac OS

Sometimes the RStudio Git pane disappears on a system where it was previously working.
This usually happens to people who installed Git by installing the Xcode command line tools.
It is usually a sign that you need to re-agree to the Xcode license agreement. This is necessary after a Mac OS upgrade, re-installing Xcode, or even quiet Xcode upgrades that sometimes seem to happen without the user's knowledge.

In the shell, you could execute `git status` and you might see a message along these lines:

```console
Agreeing to the Xcode/iOS license requires admin privileges, please run “sudo xcodebuild -license” and then retry this command.
```

If you get such clear instructions, by all means do what it says, i.e. run `sudo xcodebuild -license`, to re-agree to the license.

In any case, you need to tickle the Xcode command line tools to prompt you for whatever it needs. Here are other commands that, depending on the situation, might trigger the necessary prompts:

```console
xcode-select --install
```

or

```console
git config --global --list
```

Then **restart RStudio**.

## Dysfunctional PATH

Some cases of RStudio *not* automatically detecting the Git executable stem from problems with `PATH`.
This is the set of directories where your computer will look for executables, such as Git (today) or `make`.
Certain methods of Git installation, especially on Windows and/or older OSes, have a higher tendency to put Git in an unconventional location or to fail to add the relevant directory to `PATH`.

How to see your `PATH`?

In the shell:

```console
echo $PATH
```

Take a good hard look at this.
See the point above about finding your Git executable or re-installing it while you are **wide awake**.
Is the Git executable's parent directory in your `PATH`?
No?
**Fix that.**

At this point I recommend that you do a Google search to find instructions on how to modify `PATH` on your specific operating system.

## Push/Pull buttons greyed out in RStudio

Are you sure your local repository is associated with a remote repository, e.g. a GitHub repo?
In a shell with working directory set to the local Git repo, enter this command:
  
```console
~/tmp/myrepo % git remote -v                                           
origin  git@github.com:jennybc/myrepo.git (fetch)
origin  git@github.com:jennybc/myrepo.git (push)
```
We want to see that fetch and push are set to remote URLs that point to the remote repo.

If you discover you still need to set a remote, get the HTTPS or SSH URL, as appropriate, for your GitHub repo.
This is easy to get onto your clipboard from the repo's GitHub page.
Do this in the shell:
  
```console
git remote add origin https://github.com/jennybc/myrepo.git
```

Download all the files from the online GitHub repository and deal with any 
conflicts (substituting `master` for `main`, if relevant).
  
```console
git pull origin main
```

Call `git remote -v` again.
Once you are satisfied that your GitHub remote is set properly, you can move on to the next step.

Are you sure the current branch is *tracking* a branch on the remote?
In that same shell, in your repo, do this:

```console
~/tmp/myrepo % git branch -vv
* main 2899c91 [origin/main] A commit from my local computer
```

The above shows successful confirmation that the local `main` branch is tracking `origin/main`, i.e. the `main` branch on GitHub.
If you don't see the `[origin/main]` bit, that is a problem.
By the way, `git branch -r` and `git remote show origin` are two more commands that are helpful for examining your remote setup.

When connecting a local repo to a new GitHub repo, a lot of people remember to add the GitHub remote, but forget to also cement this tracking relationship for any relevant branches.

If you discover your local `main` branch is not yet tracking `main` on GitHub, fix that like so:
  
```console
git push --set-upstream origin main
```

This is equivalent to `git push -u origin main` but conveys more about what you are doing.

Call `git branch -vv` or `git branch -r` or `git remote show origin` again to confirm that the `main` branch on GitHub is the tracking branch for the local `main` branch.

## I have no idea if my local repo and my remote repo are connected.

See the above section on "Push/Pull buttons greyed out in RStudio."

## Push rejected, i.e. fail at the Git/GitHub level

You might have changes on the remote AND on your local repo.
Just because you don't remember making any edits in the browser doesn't mean you didn't.
Humor me.

Pull first.
Resolve any conflicts.
Then try your push again.

## RStudio is not making certain files available for staging/committing

Do you have a space in your directory or file names? [A space in a file name is a space in your soul.](https://twitter.com/aaronquinlan/status/711593127551733761)
Get rid of it.

Is your Git repo / RStudio Project inside a folder that ... eventually rolls up to Google Drive, DropBox, Microsoft OneDrive, or a network drive?
If yes, I recommend you move the repo / Project into a plain old directory that lives directly on your computer and that is not managed by, e.g., Google Drive.

If you cannot deal with the two root causes identified above, then it is possible that a more powerful Git client (chapter \@ref(git-client)) will be able to cope with these situations.
But I make no promises.
You should also try Git operations from the command line.

## I hear you have some Git repo inside your Git repo

Do not create a Git repository inside another Git repository. Just don't.

If you have a genuine need for this, which is really rare, the proper way to do it is via [submodules](http://git-scm.com/book/en/v2/Git-Tools-Submodules).

In STAT 545, we certainly do not need to do this and when we've seen it, it's been a mistake.
This has resulted in the unexpected and complete loss of the inner Git repository.
To be sure, there was more going on here (cough, GitHub Desktop client), but non-standard usage of Git repos makes it much easier to make costly mistakes.

<!--chapter:end:connect-troubleshooting.Rmd-->

# (PART) Early GitHub Wins {-} 

# Get started with GitHub {#usage-intro .unnumbered}

Now that we've verified your Git/GitHub/RStudio setup, we can demo the workflows you'll use to get your work onto GitHub:

  * [New project, GitHub first] is the easiest way to get a working project.
  * [Existing project, GitHub first] is a deeply pragmatic way to get pre-existing work onto GitHub.
  * [Existing project, GitHub last] is the more proper way to connect existing local work to a remote on GitHub, especially if there's already a Git history.
  
This part concludes with two R-specific workflows that show off how well [R Markdown (the format)](https://rmarkdown.rstudio.com) and [rmarkdown (the package)](https://cran.r-project.org/package=rmarkdown) work with GitHub:

  * [Test drive R Markdown]
  * [Render an R script]

<!--chapter:end:usage-intro.Rmd-->

# New project, GitHub first {#new-github-first}

We create a new Project, with the preferred "GitHub first, then RStudio" sequence.
Why do we prefer this?
Because this method of copying the Project from GitHub to your computer also sets up the local Git repository for immediate pulling and pushing.
Under the hood, we are doing `git clone`.

You've actually done this before during set up (chapter \@ref(rstudio-git-github)).
We're doing it again, *with feeling*.

The workflow is pretty similar for other repository managers like GitLab or Bitbucket.
We will specify below when you may need to do something differently.

## Make a repo on GitHub


Go to <https://github.com> and make sure you are logged in.

Near "Repositories", click the big green "New" button.
Or, if you are on your own profile page, click on "Repositories", then click the big green "New" button.

How to fill this in:

* Repository template: No template.
* Repository name: `myrepo` or whatever you wish to name your new project. Approach this similar to a variable name, in code: descriptive but brief, no whitespace. Letters, digits, `-`, `.`, or `_` are allowed.
* Description: "Analysis of the stuff" or any short description of the project. Write this for humans.
* Public.
* Initialize this repository with: Add a README file.

Click the big green button that says "Create repository".

Now click the big green button that says "<> Code".

Copy a clone URL to your clipboard.
If you're taking our default advice, copy the HTTPS URL.
But if you're opting for SSH, then make sure to copy the SSH URL.


\begin{center}\includegraphics[width=0.6\linewidth]{img/github-https-or-ssh-url-annotated} \end{center}

### GitLab

Log in at <https://gitlab.com>.
Click on the "+" button in the top-right corner, and then on "New project".

- Project name: `myrepo` (or whatever you wish)  
- Public
- YES Initialize repository with a README

Click the big green button "Create project."

Copy the HTTPS or SSH clone URL to your clipboard via the blue "Clone" button.

### Bitbucket

Log in at <https://bitbucket.org>.
On the left-side pane, click on the "+" button, and then on "Repository" under "Create". 

- Repository name: `myrepo` (or whatever you wish)
- Access level: Uncheck to make the repository public.
- Include a README?: Select either "Yes, with a tutorial (for beginners)" or "Yes, with a template"
- Version control system: Git

Click the big blue button "Create repository."

Copy the HTTPS or SSH clone URL that appears when you click on the blue "Clone" button.
Make sure you remove the `git clone ...` that shows up at the beginning.

## New RStudio Project via git clone {#new-rstudio-project-via-git}


\begin{center}\includegraphics[width=0.6\linewidth]{img/new-project-github-first} \end{center}

I present two ways to do this:

* `usethis::create_from_github()`
* Via the RStudio IDE

*(Recall that we showed how to do this with command line Git in chapter \@ref(push-pull-github).)*

When you are cloning your own GitHub repository, the two methods are equivalent.
In other scenarios, especially fork-and-clone (chapter \@ref(fork-and-clone)), I think `usethis::create_from_github()` is superior, because it does additional, recommended setup.

Pick **one** of these methods below.

### `usethis::create_from_github()`

You can execute this command in any R session.
If you use RStudio, then do this in the R console of any RStudio instance.

``` r
usethis::create_from_github(
  "https://github.com/YOU/YOUR_REPO.git",
  destdir = "~/path/to/where/you/want/the/local/repo/"
)
```

The first argument is `repo_spec` and it accepts the GitHub repo specification in various forms.
In particular, you can use the URL we just copied from GitHub.

The `destdir` argument specifies the parent directory where you want the new folder (and local Git repo) to live.
If you don't specify `destdir`, usethis defaults to some very conspicuous place, like your desktop.
If you like to keep Git repos in a certain folder on your computer, you can personalize this default by setting the `usethis.destdir` option in your `.Rprofile`.

We're accepting the default behaviour of two other arguments, `rstudio` and `open`, because that's what most people will want.
For example, for an RStudio user, `create_from_github()` does this:

  * Creates a new local directory in `destdir`, which is all of these things:
    - a directory or folder on your computer
    - a Git repository, linked to a remote GitHub repository
    - an RStudio Project
  * Opens a new RStudio instance in the new Project
  * **In the absence of other constraints, I suggest that all of your R projects have exactly this set-up.**

### RStudio IDE

In RStudio, start a new Project:

  * *File > New Project > Version Control > Git*. In the "repository URL" paste
    the URL of your new GitHub repository. It will be something like this
    `https://github.com/jennybc/myrepo.git`.
  * Be intentional about where you create this Project.
  * I suggest you "Open in new session".
  * Click "Create Project" to create a new directory, which will be all of these things:
    - a directory or "folder" on your computer
    - a Git repository, linked to a remote GitHub repository
    - an RStudio Project
  * **In the absence of other constraints, I suggest that all of your R projects have exactly this set-up.**

This should download the `README.md` file that we created on GitHub in the previous step.
Look in RStudio's file browser pane for the `README.md` file.

Behind the scenes, RStudio has done this for you:

```console
git clone https://github.com/jennybc/myrepo.git
```

### Have a look around

Regardless of whether you used usethis or RStudio, you should now be working in the new Git repo.
The implicit `git clone` should download the `README.md` file that we created on GitHub in the previous step.
Look in RStudio's file browser pane for the `README.md` file.

There's a big advantage to the "GitHub first, then RStudio" workflow: the remote GitHub repo is configured as the `origin` remote for your local repo and your local `main` branch is now tracking the `main` on GitHub.
This is a technical but important point about Git.
The practical implication is that you are now set up to push and pull.
No need to fanny around setting up Git remotes and tracking branches on the command line.

We're about to confirm we are setup for pulling and pushing.

\begin{figure}
\includegraphics[width=0.6\linewidth]{img/github-pull-push} \caption{Pull and push.}(\#fig:github-pull-push)
\end{figure}


### Optional: peek under the hood

Completely optional activity: use command line Git to see what we're talking about above, i.e. the remote and tracking branch setup.

`git remote -v` or `git remote --verbose` shows the remotes you have setup.
Here's how that looks for someone using HTTPS with GitHub and calling it `origin`:

```console
~/tmp/myrepo % git remote -v
origin  https://github.com/jennybc/myrepo.git (fetch)
origin  https://github.com/jennybc/myrepo.git (push)
```

`git branch -vv` prints info about the current branch (`-vv` for "very verbose", I guess).
In particular, we can see that local `main` is tracking the `main` branch on `origin`, a.k.a. `origin/main`.

```console
~/tmp/myrepo % git branch -vv
* main 2899c91 [origin/main] A commit from my local computer
```

Finally, `git remote show origin` gives yet another view on useful remote and branch information:

```console
~/tmp/myrepo % git remote show origin    
* remote origin
  Fetch URL: https://github.com/jennybc/myrepo.git
  Push  URL: https://github.com/jennybc/myrepo.git
  HEAD branch: main
  Remote branch:
    main tracked
  Local branch configured for 'git pull':
    main merges with remote main
  Local ref configured for 'git push':
    main pushes to main (up to date)
```

`git clone`, which RStudio did for us, sets all of this up automatically.
This is why "GitHub first, then RStudio" is the preferred way to start projects early in your Git/GitHub life.

## Make local changes, save, commit

**Do this every time you finish a valuable chunk of work, probably many times a day.**

From RStudio, modify the `README.md` file, e.g., by adding the line "This is a line from RStudio".
Save your changes.

Commit these changes to your local repo. How?

  * Click the "Git" tab in upper right pane
  * Check "Staged" box for any files whose existence or modifications you want to commit.
    - To see more detail on what's changed in file since the last commit, click on "Diff" for a Git pop-up
  * If you're not already in the Git pop-up, click "Commit"
  * Type a message in "Commit message", such as "Commit from RStudio".
  * Click "Commit"

## Push your local changes to GitHub

**Do this a few times a day, but possibly less often than you commit.**

You have new work in your local Git repository, but the changes are not online yet.

This will seem counterintuitive, but first let's stop and pull from GitHub.

Why?
Establish this habit for the future!
If you make changes to the repo in the browser or from another machine or (one day) a collaborator has pushed, you will be happier if you pull those changes in before you attempt to push.
  
Click the blue "Pull" button in the "Git" tab in RStudio.
I doubt anything will happen, i.e. you'll get the message "Already up-to-date."
This is just to establish a habit.

Click the green "Push" button to send your local changes to GitHub.
RStudio will report something along these lines:

```console
>>> /usr/bin/git push origin HEAD:refs/heads/main
To https://github.com/jennybc/myrepo.git
   2899c91..b34cade  HEAD -> main
```

## Confirm the local change propagated to the GitHub remote

Go back to the browser.
I assume we're still viewing your new GitHub repo.

Refresh.

You should see the new "This is a line from RStudio" in the README.

If you click on "commits," you should see one with the message "Commit from RStudio".

## Make a change on GitHub

Click on README.md in the file listing on GitHub.

In the upper right corner, click on the pencil for "Edit this file".

Add a line to this file, such as "Line added from GitHub."

Edit the commit message in "Commit changes" or accept the default.

Click the big green button "Commit changes."

### GitLab

Click on README.md in the file listing on GitLab.

In the upper right corner, click on "Edit".

Add a line to this file, such as "Line added from GitLab."

Edit the commit message in "Commit changes" or accept the default.

Click the big green button "Commit changes."

### Bitbucket

Click on README.md in the file listing on Bitbucket.

In the upper right corner, click on "Edit".

Add a line to this file, such as "Line added from Bitbucket."

Click on the blue "Commit" button. A pop-up will show up. Edit the commit message or accept the default.

Click the blue "Commit" button.

## Pull from GitHub

Back in RStudio locally ...

Inspect your README.md.
It should NOT have the line "Line added from GitHub".
It should be as you left it.
Verify that.

Click the blue Pull button.

Look at README.md again.
You should now see the new line there.

## The end

Now just "lather, rinse, repeat".
Do work somewhere: locally or on GitHub.
Commit it.
Push it or pull it, depending on where you did the work, but get local and remote "synced up".
Repeat.

Note that in general (and especially in future when collaborating with other developers) you will usually need to pull changes from the remote (GitHub) before pushing the local changes you have made.
For this reason, it's a good idea to try and get into the habit of pulling before you attempt to push.

<!--chapter:end:usage-new-project-github-first.Rmd-->

# Existing project, GitHub first {#existing-github-first}

This is a novice-friendly workflow for bringing an existing R project into the RStudio and Git/GitHub universe.

We do this in a slightly goofy way, in order to avoid using Git at the command line.
You won't want to work this way forever, but it's perfectly fine as you're getting started!
At first, the main goal is to accumulate some experience and momentum.
There is nothing goofy about the GitHub repo that this creates, it is completely standard.
Transition to a more elegant process when you're ready.

We assume you've got your existing R project isolated in a directory on your computer.
If that's not already true, make it so.
Create a directory and marshal all the existing data and R scripts there.
It doesn't really matter where you do this, but note where the project currently lives.

## Make a repo on GitHub


Go to <https://github.com> and make sure you are logged in.

Near "Repositories", click the big green "New" button.
Or, if you are on your own profile page, click on "Repositories", then click the big green "New" button.

How to fill this in:

* Repository template: No template.
* Repository name: `myrepo` or a similarly short name for this existing project. Approach this similar to a variable name, in code: descriptive but brief, no whitespace. Letters, digits, `-`, `.`, or `_` are allowed.
* Description: "Analysis of the stuff" or any short description of the project. Write this for humans.
* Public.
* Initialize this repository with: Add a README file.

Click the big green button that says "Create repository".

Now click the big green button that says "<> Code".

Copy a clone URL to your clipboard.
If you're taking our default advice, copy the HTTPS URL.
But if you're opting for SSH, then make sure to copy the SSH URL.


\begin{center}\includegraphics[width=0.6\linewidth]{img/github-https-or-ssh-url-annotated} \end{center}

## New RStudio Project via git clone {#git-clone-usethis-rstudio}


\begin{center}\includegraphics[width=0.6\linewidth]{img/new-project-github-first} \end{center}

I present two ways to do this:

* `usethis::create_from_github()`
* Via the RStudio IDE

*(Recall that we showed how to do this with command line Git in chapter \@ref(push-pull-github).)*

When you are cloning your own GitHub repository, the two methods are equivalent.
In other scenarios, especially fork-and-clone (chapter \@ref(fork-and-clone)), I think `usethis::create_from_github()` is superior, because it does additional, recommended setup.

Pick **one** of these methods below.

### `usethis::create_from_github()`

You can execute this command in any R session.
If you use RStudio, then do this in the R console of any RStudio instance.

``` r
usethis::create_from_github(
  "https://github.com/YOU/YOUR_REPO.git",
  destdir = "~/path/to/where/you/want/the/local/repo/"
)
```

The first argument is `repo_spec` and it accepts the GitHub repo specification in various forms.
In particular, you can use the URL we just copied from GitHub.

The `destdir` argument specifies the parent directory where you want the new folder (and local Git repo) to live.
If you don't specify `destdir`, usethis defaults to some very conspicuous place, like your desktop.
If you like to keep Git repos in a certain folder on your computer, you can personalize this default by setting the `usethis.destdir` option in your `.Rprofile`.

We're accepting the default behaviour of two other arguments, `rstudio` and `open`, because that's what most people will want.
For example, for an RStudio user, `create_from_github()` does this:

  * Creates a new local directory in `destdir`, which is all of these things:
    - a directory or folder on your computer
    - a Git repository, linked to a remote GitHub repository
    - an RStudio Project
  * Opens a new RStudio instance in the new Project
  * **In the absence of other constraints, I suggest that all of your R projects have exactly this set-up.**

### RStudio IDE

In RStudio, start a new Project:

  * *File > New Project > Version Control > Git*. In the "repository URL" paste
    the URL of your new GitHub repository. It will be something like this
    `https://github.com/jennybc/myrepo.git`.
  * Be intentional about where you create this Project.
  * I suggest you "Open in new session".
  * Click "Create Project" to create a new directory, which will be all of these things:
    - a directory or "folder" on your computer
    - a Git repository, linked to a remote GitHub repository
    - an RStudio Project
  * **In the absence of other constraints, I suggest that all of your R projects have exactly this set-up.**

This should download the `README.md` file that we created on GitHub in the previous step.
Look in RStudio's file browser pane for the `README.md` file.

Behind the scenes, RStudio has done this for you:

```console
git clone https://github.com/jennybc/myrepo.git
```

## Bring your existing project over

Using your favorite method of moving or copying files, copy the files that constitute your existing project into the directory for this new project.

In RStudio, consult the Git pane and the file browser.

  * Are you seeing all the files? They should be here if your move/copy was successful.
  * Are they showing up in the Git pane with questions marks? They should be appearing as new untracked files.
  
## Stage and commit

Commit your files to this repo. How?

  * Click the "Git" tab in upper right pane
  * Check the "Staged" box for all files that you want to commit.
    - Default: stage it.
    - When to reconsider: this will all go to GitHub. Consider if that is
      appropriate for each file. **You can absolutely keep a file locally,
      without committing it to the Git repo and sending to GitHub**. Just let it
      sit there in your Git pane, without being staged. No harm will be done. If
      this is a long-term situation, list the file in `.gitignore`.
  * If you're not already in the Git pop-up, click "Commit"
  * Type a message in "Commit message", such as "Init project XYZ".
  * Click "Commit"

## Push your local changes to GitHub

Click the green "Push" button to send your local changes to GitHub.
RStudio will display something like:

```console
>>> /usr/bin/git push origin HEAD:refs/heads/main
To https://github.com/jennybc/myrepo.git
   3a2171f..6d58539  HEAD -> main
```

## Confirm the local change propagated to the GitHub remote

Go back to the browser.
I assume we're still viewing your new GitHub repo.

Refresh.

You should see all the project files you committed there.

If you click on "commits," you should see one with the message you used, e.g. "Init project XYZ".

## The end

Now just "lather, rinse, repeat".
Do work somewhere: locally or on GitHub.
Commit it.
Push it or pull it, depending on where you did the work, but get local and remote "synced up".
Repeat.

Note that in general (and especially in future when collaborating with other developers) you will usually need to pull changes from the remote (GitHub) before pushing the local changes you have made.
For this reason, it's a good idea to try and get into the habit of pulling before you attempt to push.

<!--chapter:end:usage-existing-project-github-first.Rmd-->

# Existing project, GitHub last {#existing-github-last}

This an explicit workflow for connecting an existing local R project to GitHub, when for some reason you cannot or don't want to do a "GitHub first" workflow (see chapters \@ref(new-github-first) and \@ref(existing-github-first)).

When does this come up?
Example: it's an existing project that is already a Git repo with a history you care about.
Then you have to do this properly.

This may be less desirable for a novice because there are more opportunities to get confused and make a mistake.
But this workflow is not that hard, even with command line Git, and is even easier if you use conveniences from the [usethis](https://cran.r-project.org/package=usethis) package or the RStudio IDE.
All of these are covered below.

## Prepare the local project

We assume you've got your existing R project isolated in a directory on your computer.
If that's not already true, make it so.
Create a directory and marshal all the existing data and R scripts there.
It doesn't really matter where you do this, but note where the project currently lives.

I encourage you to make this project into an RStudio project, although it is not absolutely required.
If you opt-out of this, the instructions using command line Git or usethis will still work for you, outside of RStudio.

### Make or verify an RStudio Project

If the project is not already an RStudio Project, make it so:

  * Within RStudio you can do: *File > New Project > Existing Directory* and, if you wish, "Open in new session".
  * Alternatively, from R, call `usethis::create_project("path/to/your/project")`, substituting the path to your existing project directory.

If your project is already an RStudio Project, launch it.

### Make or verify a Git repo

You should be in RStudio now, in your project.

Is it already a Git repository?
The presence of the Git pane should tip you off.
If yes, you're done.

If not, you have several options:

  * In the R Console, call `usethis::use_git()`.
  * In RStudio, go to *Tools > Project Options ... > Git/SVN*. Under "Version control system", select "Git". Confirm New Git Repository? Yes!
  * In the shell, with working directory set to the project's directory, do `git init`.

If you used usethis or RStudio to initialize the Git repo, the Project should re-launch in RStudio.
Do that yourself if you did `git init`.
RStudio should now have a Git pane.

## Stage and commit

If your local project was already a Git repo and was up-to-date, move on. Otherwise, you probably need to stage and commit.

* Click the "Git" tab in upper right pane
* Check "Staged" box for all files you want to commit.
  - Default: stage everything
  - When to do otherwise: this will all go to GitHub. So consider if that is
    appropriate for each file. **You can absolutely keep a file locally,
    without committing it to the Git repo and sending to GitHub**. Just let it
    sit there in your Git pane, without being staged. No harm will be done. If
    this is a long-term situation, list the file in `.gitignore`.
* If you're not already in the Git pop-up, click "Commit"
* Type a message in "Commit message".
* Click "Commit"

## Create and connect a GitHub repo

We'll show a few methods for creating a new GitHub repo and connecting it to your local repo.
Pick one.

### Create and connect a GitHub repo with usethis

To use usethis for this task, you must have configured a personal access token (PAT).
This will already by configured for anyone using HTTPS as their protocol, because they are already using the PAT to authenticate for other Git operations.
But if you are an SSH person, you will need to configure a PAT, which is explained in chapter \@ref(https-pat).
It is fine to have both a PAT and SSH keys.

In your project, in the R Console, call:


``` r
usethis::use_github()
#> ✓ Creating GitHub repository 'jennybc/myrepo'
#> ✓ Setting remote 'origin' to 'https://github.com/jennybc/myrepo.git'
#> ✓ Pushing 'main' branch to GitHub and setting 'origin/main' as upstream branch
#> ✓ Opening URL 'https://github.com/jennybc/myrepo'
```
    

\begin{center}\includegraphics[width=0.6\linewidth]{img/use_github} \end{center}
    
`usethis::use_github()` does the following:
    
* Creates a new repo on GitHub.
* Configures that new repo as the `origin` remote for the local repo.
* Sets up your local default branch (e.g. `main`) to track same on `origin` and
  does an initial push.
* Opens the new repo in your browser.

### Create and connect a GitHub repo without usethis

First, you need to create a new repo on GitHub.


Go to <https://github.com> and make sure you are logged in.

Near "Repositories", click the big green "New" button.
Or, if you are on your own profile page, click on "Repositories", then click the big green "New" button.

How to fill this in:

* Repository template: No template.
* Repository name: Ideally this will be the name of your local project's directory (and RStudio Project). Why confuse yourself? But it must be a valid GitHub repo name, which means only letters, digits, `-`, `.`, or `_` are allowed. For future projects, think about this in advance, i.e. make sure each project's local name is also a valid GitHub repo name.
* Description: "Analysis of the stuff" or any short description of the project. Write this for humans.
* Public.
* **DO NOT initialize this repository with anything**.

Click the big green button that says "Create repository".

Now click the big green button that says "<> Code".

Copy a clone URL to your clipboard.
If you're taking our default advice, copy the HTTPS URL.
But if you're opting for SSH, then make sure to copy the SSH URL.


\begin{center}\includegraphics[width=0.6\linewidth]{img/github-https-or-ssh-url-annotated} \end{center}

#### Connect local repo to GitHub repo with RStudio

Click on the "two purple boxes and a white square" in the Git pane.
Click "Add remote".
Paste the GitHub repo's URL here and pick a remote name, almost certainly `origin`.
Now "Add".

We should be back in the "New Branch" dialog (if not, click on the "two purple boxes and a white square" in the Git pane again).
I assume you're on the `main` branch and want it to track `main` on GitHub (or whatever default branch you are using).
Enter `main` as the branch name and make sure "Sync branch with remote" is checked.
Click "Create" (yes, even though the branch already exists).
In the next dialog, choose "overwrite".

#### Connect local repo to GitHub repo with the command line

In a shell, do this, substituting your URL:

```console
git remote add origin https://github.com/jennybc/myrepo.git
```

Push and cement the tracking relationship between your local `main` branch and `main` on GitHub (or whatever your default branch is named):

```console
git push --set-upstream origin main
```

## Confirm the local files propagated to the GitHub remote

Go back to the browser.
I assume we're still viewing your new GitHub repo.

Refresh.

You should see all the project files you committed there.

If this project already had a Git history, it should be reflected on GitHub.

## The end

Now just "lather, rinse, repeat".
Do work somewhere: locally or on GitHub.
Commit it.
Push it or pull it, depending on where you did the work, but get local and remote "synced up".
Repeat.

Note that in general (and especially in future when collaborating with other developers) you will usually need to pull changes from the remote (GitHub) before pushing the local changes you have made.
For this reason, it's a good idea to try and get into the habit of pulling before you attempt to push.

<!--chapter:end:usage-existing-project-github-last.Rmd-->

# Test drive R Markdown {#rmd-test-drive}

We will author an R Markdown document and render it to HTML.
We discuss how to keep the intermediate Markdown file, the figures, and what to commit to Git and push to GitHub.
If GitHub is the primary venue, we render directly to GitHub-flavored markdown and never create HTML.

Here is the official R Markdown documentation: <http://rmarkdown.rstudio.com>

## Hello World

We'll practice with RStudio's boilerplate R Markdown document.

Launch RStudio in a Project that is a Git repo that is connected to a GitHub repo.

We are modelling "walk before you run" here.
It is best to increase complexity in small increments.
We test our system's ability to render the ["hello world"](http://en.wikipedia.org/wiki/%22Hello,_world!%22_program) of R Markdown documents before we muddy the waters with our own, probably buggy, documents.

Do this: *File > New File > R Markdown ...*

* Give it an informative title. This will appear in the document but does not
  necessarily have anything to do with the file's name. But the title and
  filename should be related! Why confuse yourself? The title is for human
  eyeballs, so it can contain spaces and punctuation. The filename is for humans
  and computers, so it should have similar words in it but no spaces and no
  punctuation.
* Accept the default Author or edit if you wish.
* Accept the default output format of HTML.
* Click OK.

Save this document to a reasonable filename and location.
The filename should end in `.Rmd` or `.rmd`.
Save in the top-level of this RStudio project and Git repository, that is also current working directory.
Trust me on this and do this for a while.

You might want to commit at this point.
That will help you see exactly what's happening with your files, because this will appear as a "diff" in the Git pane.
Making change very visible is one of the big benefits of using Git.

Click on "Knit HTML" or do *File > Knit Document*.
RStudio should display a preview of the resulting HTML.
Also look at the file browser.
You should see the original R Markdown document, i.e. `foo.Rmd` AND the resulting HTML `foo.html`.

Congratulations, you've just made your first reproducible report with R Markdown.

This is another good time to commit changes.

## Push to GitHub

Push the current state to GitHub.

Go visit it in the browser.

Do you see the new files?
An R Markdown document and the associated HTML?
Visit both in the browser.
Verify this:

* Rmd is quite readable. But the output is obviously not there.
* HTML is ugly.

## Output format

Do you really want HTML?
Do you only want HTML?
Are you absolutely sure?
If so, you can skip this step!

The magical process that turns your R Markdown to HTML is like so:

```
foo.Rmd --> foo.md --> foo.html
```
Note the intermediate markdown, `foo.md`.
By default RStudio discards this, but you might want to hold on to that markdown file!

Why?
GitHub gives very special treatment to markdown files.
They are rendered in an almost HTML-like way.
This is great because it preserves all the charms of plain text, but gives you a pseudo-webpage for free when you visit the file in the browser.
In contrast, HTML is rendered as plain text on GitHub and you'll have to take special measures to see it the way you want.

In many cases, you *only want the markdown*.
In that case, we switch the output format to `github_document`.
This means rendering look like this:

```
foo.Rmd --> foo.md
```

where `foo.md` is GitHub-flavored markdown.
If you still want the HTML *but also the intermediate markdown*, there's a way to request that too.

This point we're making about the importance of `.md` files is why so many R packages have a `NEWS.md` file and `README.md`, often generated from `README.Rmd`.

**Output format** is one of the many things we can control in the YAML frontmatter of `.Rmd` documents, i.e. the text at the top of your file between leading and trailing lines of `---`.

You can make some YAML changes via the RStudio IDE: click on the "gear" in the top bar of the source editor, near the "Knit HTML" button.
Select "Output options" and go to the Advanced tab and check "Keep markdown source file."
Your YAML should now look more like this:

``` yaml
---
title: "Something fascinating"
author: "Jenny Bryan"
date: "2024-09-04"
output:
  html_document:
    keep_md: true
---
```

You should have gained the line `keep_md: true`.
You can also simply edit the file yourself to achieve this.
The IDE only exposes a small fraction of what's possible to configure in the YAML.

In fact, a hand-edit is necessary if you want to keep only markdown and get GitHub-flavored markdown.
In that case, make your YAML look like this:

``` yaml
---
title: "Something fascinating"
author: "Jenny Bryan"
date: "2024-09-04"
output: github_document
---
```

Save!

You might want to commit at this point.

Render via "Knit HTML" button.

Now revisit the file browser.
In addition to `foo.Rmd`, you should now see `foo.md`.
If there are R chunks that make figures, the usage of markdown output formats will also cause those figure files to be left behind in a sensibly named sub-directory, such as `foo_files`.

If you commit and push `foo.md` and everything inside `foo_files`, then anyone with permission to view your GitHub repo can see a decent-looking version of your report.

If your output format is `html_document`, you should still see `foo.html`.
If your output format is `github_document` and you see `foo.html`, that's leftover from earlier experiments.
Delete that.
It will only confuse you later.

You might want to commit here.

## Push to GitHub

Push the current state to GitHub.

Go visit it in the browser.

Do you see the modifications and new file(s)?
Your `.Rmd` should be modified, i.e. you should see the changes you made to the YAML frontmatter.
And you should have gained, at least, the associated markdown file, `foo.md`.

* Visit the markdown file and compare to our previous HTML.
* Do you see how the markdown is much more directly useful on GitHub?
  Internalize this lesson.

## Put your stamp on it

Select everything but the YAML frontmatter and ... delete it!

Write a single sentence.

Insert an empty R chunk, via the "Chunk" menu in upper right of source editor or with the corresponding keyboard shortcut.

````
```{r, eval=TRUE}
## insert your brilliant WORKING code here
```
````

Insert 1 to 3 lines of functioning code that's relevant to you or the project where you're experimenting.
"Walk through" and run those lines using the "Run" button or the corresponding keyboard shortcut.
You MUST make sure your code actually works!

Satisfied? Save!

You might want to commit here.

Now render the whole document via "Knit HTML." Voilà!

You might want to commit here.
And push.
And admire your evolving progress on GitHub.

## Develop your report

In this incremental manner, develop your report.
Add code to this chunk.
Refine it.
Add new chunks.
Go wild!
But keep running the code "manually" to make sure it actually works.

If the code doesn't work with you babysitting it, I can guarantee you it will fail, in a more spectacular and cryptic way, when run at arms-length via "Knit HTML" or `rmarkdown::render()`.

Clean out your workspace and restart R and re-run everything periodically, if things get weird.
There are lots of chunk menu items and keyboard shortcuts to accelerate this workflow.
Render the whole document often to catch errors when they're easy to pinpoint and fix.
Save often and commit every time you reach a point that you'd like as a "fall back" position.

You'll develop your own mojo soon, but this should give you your first successful R Markdown experience.

## Publish your report

If you've been making HTML, you can put that up on the web somewhere, email it to your collaborator, whatever.

No matter what, technically you can publish this report merely by pushing a rendered version to GitHub.
However, certain practices make this effort at publishing more satisfying for your audience.

Here are two behaviors I find very frustrating:

* "Here is my code. Behold." This is when someone only pushes their source, i.e.
  R Markdown or R code, AND they really want other people to appreciate their
  "product". The implicit assumption is that the target audience will download
  all of the data and code and execute it locally.
* "Here is my HTML. Behold." This is when someone accepts the default HTML-only
  output. Remember, HTML files on GitHub are not readable by humans. Therefore,
  the implicit assumption is that the target audience will download the repo
  and point their browser at this HTML file, in order to see it.
  HTML on GitHub? It's not readable by humans.

Sometimes it's just very unrealistic to expect your audience to take the extra steps described above.
Often, with a very small change on your end, you can create an artefact on GitHub that your target audience can immediately appreciate.
  
Creating, committing, and pushing markdown (i.e., `.md` files) is a very functional, lighweight publishing strategy.
Use `output: github_document` or, if output is `html_document`, add `keep_md: true`.
In both cases, it is critical to also commit and push everything inside `foo_files`, i.e. any figures that have been created.
Now people can visit and consume your work on GitHub, like any other webpage.

This is (sort of) another example of a generally worthy principle, which is keeping things machine- and human-readable, whenever possible.
By making `foo.Rmd` available, others can see and run your __actual code__.
By also sharing `foo.md` and/or `foo.html`, others can casually browse your end product and decide if they want to obtain and run the code.

## HTML on GitHub

HTML files, such as `foo.html`, are not immediately useful on GitHub (though your local versions are easily viewable).
Visit one and you'll see the raw HTML.
Yuck.
But there are ways to get a preview: such as <http://htmlpreview.github.io>. Expect much pain with HTML files inside private repos (hence the recommendations above to emphasize markdown).
When it becomes vital for the whole world to see proper HTML in its full glory, it's time to use a more sophisticated web publishing strategy.

I have more [general ideas](#workflows-browsability) about how to make a GitHub repo function as a website.

## Troubleshooting {#rmd-troubleshooting}

__Make sure RStudio and the rmarkdown package (and its dependencies) are up-to-date.__
In case of catastrophic failure to render the boilerplate R Markdown document, consider that your software may be too old.
Details on the system used to render this document and how to check your setup:

* rmarkdown version 2.28.
  Use `packageVersion("rmarkdown")` to check yours.
* R version 4.4.1 (2024-06-14). Use `R.version.string` to check yours.
* RStudio IDE 2021.9.0.341 ("Ghost Orchid" Preview).
  Use *RStudio > About RStudio* or `RStudio.Version()$version` to check yours.

__Get rid of your `.Rprofile`__, at least temporarily.
I have found that a "mature" `.Rprofile` that has accumulated haphazardly over the years can cause trouble.
Specifically, if you've got anything in there relating to knitr, markdown, rmarkdown, or RStudio itself, it may be preventing the installation or usage of the most recent goodies.
Comment the whole file out or rename it to something else and relaunch or even re-install RStudio.

__"I have ignored your advice and dumped a bunch of code in at once. Now my Rmd does not render."__
If you can't figure out what's wrong by reading the error messages, pick one:

* Back out of these changes, get back to a functional state (possibly with no
  code), and restore them gradually. Run your code interactively to make sure it
  works. Render the entire document frequently. Commit after each successful
  addition! When you re-introduce the broken code, now it will be part of a
  small change and the root problem will be much easier to pinpoint and fix.
* Tell knitr to soldier on, even in the presence of errors. Some problems are
  easier to diagnose if you can execute specific R statements during rendering
  and leave more evidence behind for forensic examination.
  - Insert this chunk near the top of your `.Rmd` document:
  
    ````
    ```{r setup, include = FALSE, cache = FALSE}
    knitr::opts_chunk$set(error = TRUE)
    ```
    ````

  - If it's undesirable to globally accept errors, you can still specify
    `error = TRUE` for a specific chunk like so:

    ````
    ```{r wing-and-a-prayer, error = TRUE}
    ## your sketchy code goes here ;)
    ```
    ````
    
* Adapt the ["git bisect" strategy](http://webchick.net/node/99):
  - Put `knitr::knit_exit()` somewhere early in your `.Rmd` document, either in
    inline R code or in a chunk.
    Keep moving it earlier until things work.
    Now move it down in the document.
    Eventually you'll be able to narrow down the location of your broken code
    well enough to find the line(s) and fix it.

__Check your working directory.__
It's going to break your heart as you learn how often your mistakes are really mundane and basic.
Ask me how I know.
When things go wrong consider:

* What is the working directory?
* Is that file I want to read/write actually where I think it is?

Drop these commands into R chunks to check the above:

* `getwd()` will display working directory at __run time__.
  If you monkeyed around with working directory with, e.g., the mouse, maybe
  it's set to one place for your interactive development and another when
  "Knit HTML" takes over?
* `list.files()` will list the files in working directory.
  Is the file you want even there?

__Don't try to change working directory within an R Markdown document__.
Just don't.
See [knitr FAQ #5](https://yihui.name/knitr/faq/).
That is all.

__Don't be in a hurry to create a complicated sub-directory structure.__
RStudio/knitr/rmarkdown (which bring you the "Knit HTML" button) are rather opinionated about the working directory being set to the `.Rmd` file's location and about all files living together in one big happy directory.
This can all be worked around.
For example, I [recommend the here package](https://github.com/jennybc/here_here#readme) for building file paths, once you require sub-directories.
But don't do this until you really need it.

<!--chapter:end:usage-rmd-and-github.Rmd-->

# Render an R script {#r-test-drive}

An under-appreciated fact is that much of what you can do with R Markdown, you can also do with an R script.

If you're in analysis mode and want a report as a side effect, write an R script.
If you're writing a report with a lot of R code in it, write `.Rmd`.
In either case, render to markdown and/or HTML to communicate with other human beings.

* In R markdown, prose is top-level and code is tucked into chunks.
* In R scripts, code is top-level and prose is tucked into comments.
  You will use `#'` to request that certain comments appear as top-level prose
  in the rendered output.

You will continue to specify things like the output format via YAML at the top of the file.
This will need to be commented with `#'`.

## Morph R Markdown into a renderable R script

Get yourself a working R Markdown file, such as the one you made in your [Rmd test drive](#rmd-test-drive).
Or use the boilerplate `.Rmd` document RStudio makes with *File > New File > R Markdown ...*.

Save the file as `foo.R`, as opposed to `foo.Rmd`.
Yes, for a brief moment, you will have R Markdown saved as an R script, but that won't be true for long.

Transform the R markdown to R:

* Anything that's not R code?
  Like the YAML and the prose?
  Protect it with roxygen-style comments: start each line with `#'`.
* Anything that is R code?
  Let it exist "as is" as top-level code.
  That means you'll need to change the syntax of R chunk headers like so:
  
    Before: ` ```{r setup, include = FALSE}`  
    After: `#+ r setup, include = FALSE`

    Replace the leading backticks and opening curly brace with `#+`.  
    Delete the trailing curly brace.  
    Delete the 3 backticks that end each chunk.

Render the R script through one of these methods:

* Click on the "notebook" icon in RStudio to "Compile Report".
* In RStudio, do *File > Knit Document*.
* In R, do `rmarkdown::render("foo.R")`.

You'll get a markdown and/or HTML report, just as with R Markdown.

If you're having trouble making all the necessary changes and you're frustrated, see below for an example you can copy and paste.

All the workflow tips from the [Rmd test drive](#rmd-test-drive) apply here:
when you script an analysis, render it to markdown, commit the `.R`, the `.md`, any associated figures, and push to GitHub.
Collaborators can see your code, but also browse around the results without having to download and execute the code.
This makes the current state of your analysis accessible to someone who does not even run R or who wants to take a quick look at things from a cell phone or while on vacation.

## Write a render-ready R script

Instead of morphing an R Markdown file, let's create a render-ready R script directly.

Create a new R script and copy/paste this code into it.







``` r
#' Here's some prose in a very special comment. Let's summarize the built-in
#' dataset `VADeaths`.
# here is a regular code comment, that will remain as such
summary(VADeaths)

#' Here's some more prose. I can use usual markdown syntax to make things
#' **bold** or *italics*. Let's use an example from the `dotchart()` help to
#' make a Cleveland dot plot from the `VADeaths` data. I even bother to name
#' this chunk, so the resulting PNG has a decent name.
#+ dotchart
dotchart(VADeaths, main = "Death Rates in Virginia - 1940")
```

Render the R script through one of these methods:

  * Click on the "notebook" icon in RStudio to "Compile Report".
  * In RStudio, do *File > Knit Document*.
  * In R, do `rmarkdown::render("YOURSCRIPT.R")`.

Revel in your attractive looking report with almost zero effort!
Seriously, all you had to do was think about when to use special comments `#'` in order to promote that to nicely rendered text.

Drawing on the workflow tips in [Rmd test drive](#rmd-test-drive), let's add some YAML frontmatter, properly commented with `#'`, and request `github_document` as the output format.
Here's the whole script again:




``` r
#' ---
#' title: "R scripts can be rendered!"
#' output: github_document
#' ---
#'
#' Here's some prose in a very special comment. Let's summarize the built-in
#' dataset `VADeaths`.
# here is a regular code comment, that will remain as such
summary(VADeaths)

#' Here's some more prose. I can use usual markdown syntax to make things
#' **bold** or *italics*. Let's use an example from the `dotchart()` help to
#' make a Cleveland dot plot from the `VADeaths` data. I even bother to name
#' this chunk, so the resulting PNG has a decent name.
#+ dotchart
dotchart(VADeaths, main = "Death Rates in Virginia - 1940")
```

Behind the scenes here we have used `rmarkdown::render()` to render this script and you can go [visit it on GitHub](https://github.com/jennybc/happy-git-with-r/blob/master/render-r-script-demo.md).



<!--chapter:end:usage-r-script-and-github.Rmd-->

# (PART) Git fundamentals {-} 

# Some Git basics {#git-intro .unnumbered}

We've told you shockingly little about Git so far! This is by design.

We find that actual usage, in the course of your work, is the most effective way to build up a useful mental model for Git. In live workshops, we strive to introduce the most important basic ideas in the context of our guided activities. Self-learners can achieve the same by working through the "batteries included" guides earlier in the previous sections.

However, building on this early success, now is the perfect time to explicitly define some Git vocabulary. We also want to help you link Git concepts to data science tasks and projects.

This part collects anything we've written about core Git concepts. It is a work in progress and is conceived as a complement to the many excellent [external resources for Git](#resources), which we have no desire to re-invent.

<!--chapter:end:git-intro.Rmd-->

# Repo, commit, diff, tag {#git-basics}

## Repos or repositories

Git is a version control system whose original purpose was to help groups of
developers work collaboratively on big software projects. Git manages the
evolution of a set of files -- called a __repository__ or __repo__ -- in a highly structured way. Historically, these files would have consisted of source code and the instructions for how to build an application from its source.

Git has been re-purposed by the data science community [@Ram2013;
@git-for-humans; @ten-simple-rules-git]. We use it to manage the motley collection of files that make up typical data analytical projects, which consist of data, figures, reports, and, yes, some source code.

For new or existing projects, we recommend that you:

  * Dedicate a local directory or folder to it.
  * Make it an RStudio Project. *Optional but recommended; obviously only applies to projects involving R and users of RStudio.*
  * Make it a Git repository.
  
This setup happens once per project and can happen at project inception or at any later point. Chances are your existing projects each already live in a dedicated directory. Making such a directory an RStudio Project and Git repository boils down to allowing those applications to leave notes for themselves in hidden files or directories. The project is still a regular directory on your computer, that you can locate, name, move, and generally interact with as you wish. You don't have to handle it with special gloves!

The daily workflow is probably not dramatically different from what you do currently. You work in the usual way, writing R scripts or authoring reports in LaTeX or R Markdown. But instead of only *saving* individual files, periodically you make a __commit__, which takes a snapshot of all the files in the entire project. If you have ever versioned a file [by adding your initials or the date](http://www.phdcomics.com/comics/archive.php?comicid=1531), you have effectively made a commit, albeit only for a single file. It is a version that is significant to you and that you might want to inspect or revert to later. Periodically, you push commits to GitHub. This is like sharing a document with colleagues on DropBox or sending it out as an email attachment. By pushing to GitHub, you make your work and all your accumulated progress accessible to others.
  
This is a moderate change to your normal, daily workflow. It feels weird at first, but quickly becomes second nature. In [STAT 545](http://stat545.com) students are required to submit all coursework via GitHub, starting in week one. Most have never seen Git before and do not identify as programmers. It is a major topic in class and office hours for the first two weeks. Then we practically never discuss it again.

## Commits, diffs, and tags

We now connect the fundamental concepts of Git to the data science workflow:

  * repository
  * commit
  * diff

Recall that a repository or repo is just a directory of files that Git manages holistically. A commit functions like a snapshot of all the files in the repo, at a specific moment. Under the hood, that is not exactly how Git implements things. Although mental models don't have to be accurate in order to be useful, in this case it helps to align the two.

\begin{figure}
\includegraphics[width=1\linewidth]{img/commit-diff-sha-tag} \caption{\label{fig:commit-diff-sha-tag}Partial commit history for our iris example, highlighting diffs, commit messages, SHAs, and tags.}(\#fig:commit-diff-sha-tag)
\end{figure}

Figure \@ref(fig:commit-diff-sha-tag) is a look at a fictional analysis of the iris data, focusing on the evolution of a script, `iris.R`. Consider version A of this file and a modified version, version B. Assume that version A was part of one Git commit and version B was part of the next commit. The set of differences between A and B is called a "diff" and Git users contemplate diffs a lot. Diff inspection is how you re-explain to yourself how version A differs from version B. Diff inspection is not limited to adjacent commits. You can inspect the diffs between any two commits.

In fact, Git's notion of any specific version of `iris.R` is as an accumulation of diffs. If you go back far enough, you find the commit where the file was created in the first place. Every later version is stored by Git as that initial version, plus all the intervening diffs in the history that affect the file. We'll set these internal details aside now, but understanding the importance of these deltas will make Git's operations less baffling in the long run.

So, by looking at diffs, it's easy to see how two snapshots differ, but what about the why?

Every time you make a commit you must also write a short __commit message__. Ideally, this conveys the motivation for the change. Remember, the diff will show the content. When you revisit a project after a break or need to digest recent changes made by a colleague, looking at the __history__, by reading commit messages and skimming through diffs, is an extremely efficient way to get up to speed. Figure \@ref(fig:commit-diff-sha-tag) shows the messages associated with the last three commits.

Every commit needs some sort of nickname, so you can identify it. Git does this automatically, assigning each commit what is called a SHA, a seemingly random string of 40 letters and numbers (it is not, in fact, random but is a SHA-1 checksum hash of the commit). Though you will be exposed to these, you don't have to handle them directly very often and, when you do, usually the first 7 characters suffice. The commit messages in Figure \@ref(fig:commit-diff-sha-tag)  are prefixed by such truncated SHAs. You can also designate certain snapshots as special with a __tag__, which is a name of your choosing. In a software project, it is typical to tag a release with its version, e.g., "v1.0.3". For a manuscript or analytical project, you might tag the version submitted to a journal or transmitted to external collaborators. Figure \@ref(fig:commit-diff-sha-tag) shows a tag, "draft-01", associated with the last commit.

<!--chapter:end:git-basics.Rmd-->

# Git commands {#git-commands}

A collection of some of the Git commands that have been largely going on under the hood.
We've emphasized early workflows that are possible in RStudio.
But all of this and much more can be done from the command line.
This list is here mostly so we can consult it during live workshops if needed.

*Unless you use the [GitHub API](https://developer.github.com/v3/), most of the GitHub bits really have to be done from the browser.*

New local git repo from a repo on GitHub:

```console
git clone https://github.com/jennybc/happy-git-with-r.git
```

Check the remote was cloned successfully:

```console
git remote --verbose
```

Stage local changes, commit:

```console
git add foo.txt
git commit --message "A commit message"
```

Check on the state of the Git world:

```console
git status
git log
git log --oneline
```

Compare versions:

```console
git diff
```

Add a remote to existing local repo:

```console
git remote add origin https://github.com/jennybc/happy-git-with-r
git remote --verbose
git remote show origin
```

Push local `main` to GitHub `main` and have local `main` track `main` on GitHub:

```console
git push --set-upstream origin main
# shorter form
git push -u origin main
# you only need to set upstream tracking once!
```

Regular push:

```console
git push 
# the above usually implies (and certainly does in our tutorial)
git push origin main
# git push [remote-name] [branch-name]
```

Pull commits from GitHub:

```console
git pull
```

Pull commits and don't let it put you in a merge conflict pickle:

```console
git pull --ff-only
```

Fetch commits

```console
git fetch
```

Switch to a branch

```console
git checkout [branch-name]
```

Checking remote and branch tracking

```console
git remote -v
git remote show origin
git branch -vv
```

<!--chapter:end:git-commands.Rmd-->

# Branches {#git-branches}

Branching means that you take a detour from the main stream of development and
do work without changing the main stream.
It allows one or many people to work in parallel without overwriting each other's work.
It allows a someone working solo to work incrementally on an experimental idea, without jeopardizing the state of the main product.

Branching in Git is very lightweight, which means creating a branch and
switching between branches is nearly instantaneous.
This means Git encourages workflows which create small branches for exploration or new features, often merging them back together quickly.

## Create a new branch

You can create a new branch with `git branch`, then checkout the branch with `git checkout`.
To distinguish it from the main stream of development, presumably on `main`, we'll call this a "feature branch".

```console
git branch issue-5
git checkout issue-5
```

You can also use the shortcut `git checkout -b issue-5` to create and checkout the branch all at once.

Once you have switched to a branch, you can commit to it as usual.

## Switching branches

You use `git checkout` to switch between branches.

But what do you do if you are working on a branch and need to switch,
but the work on the current branch is not complete?
One option is the [Git stash](https://git-scm.com/book/en/v2/ch00/_git_stashing), but generally a better option is to safeguard the current state with a temporary commit.
Here I use "WIP" as the commit message to indicate work in progress.

```console
git commit --all -m "WIP"
git checkout main
```

Then when you come back to the branch and continue your work, you
need to undo the temporary commit by [resetting](#reset) your state.
Specifically, we want a mixed reset.
This is "working directory safe", i.e. it does not affect the state of any files.
But it does peel off the temporary WIP commit.
Below, the reference `HEAD^` says to roll the commit state back to the parent of the current commit (`HEAD`).

```console
git checkout issue-5
git reset HEAD^
```

If this is difficult to remember, or to roll the commit state back to a different previous state, the reference can also be given as the SHA of a specific commit, which you can see via `git log`.
This is where I think a graphical Git client can be invaluable, as you can generally right click on the target commit, then select the desired type of reset (e.g., soft, mixed, or hard).
This is exactly the type of intermediate-to-advanced Git usage that often feels more approachable in a graphical client.

## Merging a branch

Once you have done your work and committed it to the feature branch, you can switch back to `main` and merge the feature branch.

```console
git checkout main
git merge issue-5
```

## Dealing with conflicts

Most of the time, the merge will go smoothly.
However if both the branches you are merging changed the same part of the same file you will get a merge conflict.

```console
git merge issue-5
# Auto-merging index.html
# CONFLICT (content): Merge conflict in index.html
# Automatic merge failed; fix conflicts and then commit the result.
```

The first thing to do is **NOT PANIC**.
Merge conflicts are not the end of the world and most are relatively small and straightforward to resolve.

The first step to solving a merge conflict is determining which files are in
conflict, which you can do with `git status`:

```shell
git status
# On branch main
# You have unmerged paths.
#   (fix conflicts and run "git commit")
# 
# Unmerged paths:
#   (use "git add <file>..." to mark resolution)
# 
#     both modified:      index.html
# 
# no changes added to commit (use "git add" and/or "git commit -a")
```

So this shows only `index.html` is unmerged and needs to be resolved.
We can then open the file to see what lines are in conflict.

```html
<<<<<<< HEAD:index.html
<div id="footer">contact : email.support@github.com</div>
=======
<div id="footer">
 please contact us at support@github.com
</div>
>>>>>>> issue-5:index.html
```

In this conflict, the lines between `<<<<<< HEAD:index.html` and `======` are
the content from the branch you are currently on.
The lines between `=======` and `>>>>>>> issue-5:index.html` are from the feature branch we are merging.

To resolve the conflict, edit this section until it reflects the state you want in the merged result.
Pick one version or the other or create a hybrid.
Also remove the conflict markers `<<<<<<`, `======` and `>>>>>>`.

```html
<div id="footer">
please contact us at email.support@github.com
</div>
```

Now run `git add index.html` and `git commit` to finalize the merge.
CONFLICTS RESOLVED.

### Bailing out

If, during the merge, you get confused about the state of things or make a
mistake, use `git merge --abort` to abort the merge and go back to the state
prior to running `git merge`.
Then you can try to complete the merge again.

Git Basic Branching and Merging:

<https://git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging>

<!--chapter:end:git-branches.Rmd-->

# Remotes {#git-remotes}

Remote repositories are versions of your project that are hosted on the
Internet or another network.
A single project can have 1, 2, or even hundreds of remotes.
You pull others' changes from remotes and push your changes to remotes.



## Listing what remotes exist

`git remote` lists the names of available remotes, but usually it is more
useful to see what URLs each note corresponds to (with `-v`).

#```{bash}
#git remote -v
#```

## Adding a new remote

`git clone` automatically adds a new remote, so often you do not need to do
this manually initially.
However, after the initial clone, it is often useful to add additional remotes.

Use `git remote add` to add a new remote:

```console
git remote add happygit https://github.com/jennybc/happy-git-with-r.git
```

Note: when you add a remote you give it a nickname (here `happygit`), which you can use in git commands in place of the entire URL.

```console
git fetch happygit
```

Sidebar on nicknames: there is a strong convention to use `origin` as the nickname of your main remote.
At this point, it is common for the main remote of a repo to be hosted on GitHub (or GitLab or Bitbucket).
It is tempting to use a more descriptive nickname (such as `github`), but you might find that following convention is worth it.
It makes your setup easier for others to understand and for you to transfer information that you read in documentation, on Stack Overflow, or in blogs.

A common reason to add a second remote is when you have done a "fork and clone" of a repo and your personal copy (your fork) is set up as the `origin` remote.
Eventually you will want to pull changes from the original repository. It is common to use `upstream` as the nickname for this remote.

```console
git remote add upstream https://github.com/TRUE_OWNER/REPO.git
```

## Fetching data from remotes

To get new data from a remote use `git fetch <remote_name>`.
This retrieves the data locally, but importantly it does _not_ change the state of your local files in any way.
To incorporate the data into your repository, you need to merge or rebase your project with the remote project.

```console
# Fetch the data
git fetch happygit

# Now merge it with our local main
git merge happygit/main main

# git pull is a shortcut which does the above in one command
git pull happygit main
```

For more detail on `git pull` workflows, see \@ref(pull-tricky).

## Pushing to remotes

Use `git push <remote> <branch>` to push your local changes to the `<branch>`
branch on the `<remote>` remote.

```console
# push my local changes to the origin remote's main branch
git push origin main

# push my local changes to the happygit remote's test branch
git push happygit test
```

## Renaming and changing remotes

`git remote rename` can be used to rename a remote:

```console
git remote rename happygit hg
```

`git remote set-url` can be used to change the URL for a remote.
This is sometimes useful if you initially set up a remote using HTTPS, but now want to use SSH instead (or *vice versa*).

```console
git remote set-url happygit git@github.com:jennybc/happy-git-with-r.git
```

One fairly common workflow is you initially cloned a repository on GitHub
locally (without forking it), but now want to create your own fork and push
changes to it.
As described earlier, it is common to call the source repository `upstream` and to call your fork `origin`.
So, in this case, you need to first rename the existing remote (from `origin` to `upstream`).
Then add your fork as a new remote, with the name `origin`.

```console
git remote rename origin upstream
git remote add origin git@github.com:jimhester/happy-git-with-r.git
```

## Upstream tracking branches

It is possible to set the branch on the remote each of your local remotes
corresponds to.
`git clone` sets this up automatically, so for your own `main` branch this is not something you will run into.
However by default if you create a new branch and try to push to it you will see something like this:

```console
git checkout -b mybranch
git push
# fatal: The current branch foo has no upstream branch.
# To push the current branch and set the remote as upstream, use
#
#     git push --set-upstream origin foo
```

You can do as the error message says and explicitly set the upstream branch
with `--set-upstream`.
However I would recommend instead changing the default behavior of `push` to automatically set the upstream branch to the branch with the same name on the remote.

You can do this by changing the git `push.default` option to `current`.

```console
git config --global push.default current
```

See also Working with Remotes:

<https://git-scm.com/book/en/v2/Git-Basics-Working-with-Remotes>

<!--chapter:end:git-remotes.Rmd-->

# Refs {#git-refs}

Many extremely useful Git workflows require you to identify a specific point in your repo's history, i.e. a specific commit.

We've explained elsewhere that every commit is associated with a so-called SHA, i.e. a SHA-1 checksum of the commit itself.
These opaque strings of 40 letters and numbers are not particularly pleasant for humans to work with.
The entry-level coping strategy is to work with an abbreviated form of the SHA.
It's typical to only use the first 7 characters, as this almost always uniquely identifies a commit.


\begin{center}\includegraphics[width=0.6\linewidth]{img/refs-only-shas} \end{center}

Luckily, there are even more ways to talk about a specific commit, that are much easier for humans to wrap their head around.
These are called Git "refs", short for references and, if you're familiar with the programming concept of a pointer, that's exactly the right mental model.

## Useful refs

Here are some of the most useful refs:

* A branch name.
  Example: `main`, `wild-experiment`.
  When you refer to the `main` branch, that resolves to the SHA of the tip of
  the `main` branch.
  Think of a branch ref as a sliding ref that evolves as the branch does.
  

\begin{center}\includegraphics[width=0.6\linewidth]{img/refs-only-branches} \end{center}

* `HEAD`.
  This (almost always) resolves to the tip of the branch that is currently
  checked out.[^HEAD-no-branch]
  You can think of `HEAD` as a ref that points to the tip of the current branch,
  which itself is a ref, that points to a specific SHA.
  There are two layers of indirection.
  This is also called a *symbolic ref*.
  

\begin{center}\includegraphics[width=0.6\linewidth]{img/refs-branches-and-HEAD-1} \end{center}
  
* A tag.
  Example: `v1.4.2`.
  Tags differ from branch refs and the `HEAD` ref in that they tend to be much
  more static.
  Tags aren't sliding by nature, although it is possible to reposition a tag to
  point at a new SHA, if you make an explicit effort.
  The most common use of a tag is to provide a nice label for a specific SHA.


\begin{center}\includegraphics[width=0.6\linewidth]{img/refs-tag} \end{center}

[^HEAD-no-branch]: When does `HEAD` not resolve to the SHA at the tip of some branch?
When you are a *detached HEAD* state.
Detached HEAD!
That sounds bad, but it's not intrinsically good or bad.
It IS bad, though, to be in a detached HEAD state if you didn't mean to be and you don't understand the deal.
You get into a detached HEAD state when you directly checkout a specific commit, as opposed to checking out or switching to a *branch*.
In experienced hands, this can be a legit thing to do.
But in the meantime, I recommend that you always visit a specific state in the history by checking out a *branch*, even if that means you need to create a temporary branch like `holder` or `time-travel`.
To get out of the detached `HEAD` state, checkout some existing branch, with `git checkout main` or similar.
Otherwise, the StackOverflow thread [How do I fix a Git detached head?](https://stackoverflow.com/q/10228760) addresses many vexing detached `HEAD` scenarios.

If you'd like to make all of this more concrete, you can use `git rev-parse` in the shell to witness how refs resolve to concrete SHAs.
Here's the general pattern:

```console
git rev-parse YOUR_REF_GOES_HERE
```

Here are some examples executed in the Happy Git repo:

```console
~/rrr/happy-git-with-r % git rev-parse HEAD
631fee855db49d87f6c2a2cab474e89c11322bf4

~/rrr/happy-git-with-r % git rev-parse main
631fee855db49d87f6c2a2cab474e89c11322bf4

~/rrr/happy-git-with-r % git rev-parse testing-something                       
1eeb91d177b7cb5f9a0b29ebee3e6c0c8ff98f88
```

Notice that `HEAD` and `main` resolve to the same SHA, since the `main` branch was checked out at the time.
`testing-something` is the name of a branch that happened to be lying around.

These refs can be used in all sorts of Git operations, such as `git diff`, `git reset`, and `git checkout`:

```console
git diff main testing-something

git reset testing-something -- README.md

git checkout -b my-new-branch main
```

## Relative refs

There are also modifiers that help you specify a commit relative to a ref, e.g. "the commit just before this one".

`HEAD~1` refers to the commit just before `HEAD`.
`HEAD^` is another way to say exactly the same thing.


\begin{center}\includegraphics[width=0.6\linewidth]{img/refs-relative} \end{center}

Here are some examples executed in the Happy Git repo:

```console
~/rrr/happy-git-with-r % git rev-parse HEAD~1
5dacec4950a3746310bb30704417a792302b044a

~/rrr/happy-git-with-r % git rev-parse HEAD^
5dacec4950a3746310bb30704417a792302b044a
```

Notice that `HEAD~1` and `HEAD^` resolve to the same SHA.

Both of these patterns generalize.
`HEAD~3` and `HEAD^^^` are valid and equivalent refs.

I must admit that I am not a big fan of these relative ref shortcuts and especially not when reaching back more than one commit.
I worry that I have some sort of off-by-one error in my understanding and I'll end up targetting the wrong commit.

Tools like GitKraken and GitHub make it extremely easy to copy specific SHAs to your clipboard.
So when I need a ref that's not a simple branch name or tag, I almost always lean on user-friendly tools like GitKraken or GitHub to allow me to state my intent using the actual SHA of interest.
I suspect that the relative ref shortcuts are most popular with folks who are exclusively using command line Git and are operating under different constraints.
There's actually a rich set of ways to specify a target commit that goes well beyond the `^` and `~` syntax shown here.
You can learn more in the [official Git documention about revision parameters](https://git-scm.com/docs/gitrevisions).

In GitKraken, right or control click on the target commit to access a menu that includes "Copy commit sha", among many other useful commands.
If you're using another Git client, there is probably a way to do this and it's worth figuring that out.


\begin{center}\includegraphics[width=0.6\linewidth]{img/gitkraken-screenshot-copy-commit-sha} \end{center}

GitHub also makes it extremely easy to copy a SHA in many contexts.
This screenshot shows just one example.
Once you start looking for this feature, you'll find it in many places on GitHub.


\begin{center}\includegraphics[width=0.6\linewidth]{img/github-screenshot-copy-the-full-sha} \end{center}

<!--chapter:end:git-refs.Rmd-->

# (PART) Remote setups {-} 

# Git remote setups {#remote-scenarios-intro .unnumbered}

The previous part ended with some basics about [Git remotes](#git-remotes), such as how to define or rename one. Recall that a Git remote is another copy of the repo, usually living elsewhere (hence the term "remote"), that you can pull changes from or push changes to. Remotes are the foundation for all collaborative Git work.

But knowing the mechanics of how to add or rename a remote does little good if you don't know *why* or *when* to do it. Luckily, we have very strong opinions about how you should set up your remotes, all motivated by getting you prepared for smooth, happy collaborative work.

In this part we describe various remote setups that are common (for better or worse) and what they are good for (or what's wrong with them and how to fix).

<!--chapter:end:remote-setups-intro.Rmd-->

# Common remote setups {#common-remote-setups}

We only consider a very constrained set of remotes here:

* The remote is on GitHub, e.g. its URL looks something like `https://github.com/OWNER/REPO.git` or `git@github.com:OWNER/REPO.git`.
* The remote is named `origin` or `upstream`. These may not be the most evocative names in the world, but they are the most common choices.

If you use a different host or different remote names, you should still be able to translate these examples to your setting.

Along the way, we note how these setups relate to the usethis package, i.e. how usethis can help you get into a favorable setup or how a favorable setup unlocks the full power of usethis.
Many of these operations -- including characterizing your GitHub remotes -- require that you have configured a GitHub personal access token.
See section \@ref(get-a-pat) for more details on why and how to do that.
If you don't use usethis, feel free to ignore these asides.

## No GitHub

As a starting point, consider a local Git repo that is not yet connected to GitHub.


\begin{center}\includegraphics[width=0.6\linewidth]{img/no-github} \end{center}

This is not very exciting, but sets the stage for what's to come.
We introduce the icon we use for a Git repo, which looks like a stack of coins or a barrel.
This one is blue, which indicates you have write permission.

How to achieve:

  * Command line Git: `git init`
  * With usethis, existing project: `usethis::use_git()`
  * With RStudio:
    - Existing Project: *Tools > Version Control > Project Setup*, select Git
      as the version control system
    - New Project: Make sure "Create a Git repository" is selected
  
usethis describes this setup as "no_github".

## Ours (more specifically, yours) {#ours-you}

A common next step is to associate a local repo with a copy on GitHub, owned by you.


\begin{center}\includegraphics[width=0.6\linewidth]{img/ours-you} \end{center}

A remote named `origin` is configured and you have permission to push to (and pull from) `origin`.
(That's why `origin` is colored blue and there are solid arrows going both directions.)
The `origin` remote on GitHub is what we'll call a **source** repo, meaning it is not a fork (i.e. copy) of anything else on GitHub.
In this case, `origin` is also what we'll call your **primary** repo, meaning it is the primary remote you interact with on GitHub (for this project).

How to achieve if the local repo exists first:

  *  Detailed instructions are in
     [Existing project, GitHub last](#existing-github-last).
  * With usethis: `usethis::use_github()`.
  * Command line Git or RStudio: You can't complete this task fully from the
    command line or from RStudio:
    - Create a new GitHub repo in the browser, with the correct name,
      and capture its HTTPS or SSH URL.
    - Configure the repo as the `origin` remote.
    - Push.
    - Even now, the setup may not be ideal, because upstream tracking
      relationships are probably not setup, which means you may not be able to
      push and pull easily. You may need to explicitly configure an upstream
      tracking branch for one or more local branches. Next time you want to
      create a GitHub repo from a local repo, consider using
      `usethis::use_github()`, which completes all of this setup in one go.
    
How to achieve if the remote repo exists first:
  
  * Detailed instructions are in
    [New RStudio Project via git clone](#git-clone-usethis-rstudio).
  * With usethis: `usethis::create_from_github("OWNER/REPO", fork = FALSE)`
  * Command line: `git clone <URL>`, with the source repo's HTTPS or SSH URL
  * In RStudio: Capture the source repo's HTTPS or SSH URL and do
    *File > New Project > Version Control > Git*.
  
usethis describes this setup as "ours".

## Ours {#ours-them}

Here is a variation on "ours" that is equivalent in practice.


\begin{center}\includegraphics[width=0.6\linewidth]{img/ours-them} \end{center}

A remote named `origin` is configured and you can push to (and pull from) `origin`.
As above, `origin` is a **source** repo, meaning it is not a fork (or copy) of anything else on GitHub.
The `origin` remote is, however, not owned by you.
Instead it's owned by another GitHub user or organisation.
`origin` is also your **primary** repo in this setup.

How does this happen?

1. The source repo is owned by an organisation and your role in this organisation confers enough power to create repos or to push to this repo.
2. The owner of the source repo has added you, specifically, as a collaborator to this specific repo.

How to achieve? The procedure is the same as for the previous "ours" setup. But remember to specify `usethis::use_github(organisation = "ORGNAME")` if you want to create a new repo under an organisation, instead of your personal account.

usethis describes this setup as "ours".

## Theirs {#theirs}

This is a setup that many people get themselves into, when it's not actually what they need.
It's not broken *per se*, but it's limiting.


\begin{center}\includegraphics[width=0.6\linewidth]{img/theirs} \end{center}

You cannot push to `origin`, which is both the source repo and your primary repo.
(This is indicated by the orange color of `origin` and the greyed out, dashed "push" arrow.)
`origin` is read-only for you.

If you are taking a repo for a quick test drive, this configuration is fine.
But there is no way to get changes back into the source repo, since you cannot push to it and you haven't created a fork, which is necessary for a pull request.

How does this happen?

* Cloning the source repo, either via `git clone <URL>` (command line) or through a Git client, e.g. RStudio's *File > New Project > Version Control > Git* workflow.
* Calling `usethis::create_from_github("OWNER/REPO", fork = FALSE)`.

usethis describes this setup as "theirs".

What if you do want to make a pull request?
This means you should have done *fork-and-clone* instead of *clone*.
If you've made no changes or they're easy to save somewhere temporarily, just start over with a fork-and-clone workflow (fully explained in \@ref(fork-and-clone)) and re-introduce your changes.
It is also possible to preserve your work in a local branch, fork the source repo, re-configure your remotes, re-sync up with the source repo, and get back on track.
But this is much easier to goof up.
And remember to fork and clone (not just clone) in the future!

## Fork (of theirs) {#fork-them}

This is an ideal setup if you want to make a pull request and generally follow the development of a source repo owned by someone else.


\begin{center}\includegraphics[width=0.6\linewidth]{img/fork-them} \end{center}

This shows a successful "fork-and-clone".
Your local repo can pull changes from the source repo, which is configured as `upstream`, which you cannot push to (but you can pull from).
You have a fork of the source repo (a very special copy, on GitHub) and it is configured as `origin`.
`origin` is your primary repo.
You can push to and pull from `origin`.
You can make a pull request back to the source repo via your fork.

usethis describes this setup as "fork".

How to achieve:

  * Detailed instructions are given in [Fork and clone](#fork-and-clone).
  * With usethis: `usethis::create_from_github("OWNER/REPO", fork = TRUE)`
  * Command line Git or RStudio: You can't complete this task fully from the
    command line or RStudio:
    - Fork the source repo in the browser, capture the HTTPS or SSH
      URL of **your fork**, then use `git clone <FORK_URL>`
      (command line) or RStudio's *File > New Project > Version Control > Git*
      workflow. But, wait, you're not done! If you stop here, you will have the
      incomplete setup we refer to as
      ["fork (salvageable)"](#fork_upstream_is_not_origin_parent), below.
    - You still need to add the source repo as the `upstream` remote. Capture
      the HTTPS or SSH URL of the **source repo**. At the command line, do `git
      remote add upstream <SOURCE_URL>` or click RStudio's *New Branch* button,
      which brings up a window where you can add the `upstream` remote.
    - Even then, the setup may not be ideal, because your local default branch
      is probably tracking `origin`, not `upstream`, which is preferable for
      a fork. `usethis::create_from_github()` completes all of this setup in
      one go.
    - These last two steps are described in
      [Finish the fork and clone setup](#fork-and-clone-finish).

## Fork (of ours)

This is a less common variation on the fork setup.


\begin{center}\includegraphics[width=0.6\linewidth]{img/fork-ours} \end{center}

In this case, you have permission to push to the source repo, but you elect to create a personal fork anyway.
Certain projects favor this approach and it offers maximum development flexibility for advanced users.
However, most users are better served by the simpler "ours" setup in this case.

How to achieve:

  * In general, it's the same as the regular [fork setup](#fork-them) above.
  * With usethis, make sure to explicitly specify `fork = TRUE`, i.e. do
    `usethis::create_from_github("OWNER/REPO", fork = TRUE)`.
    
usethis describes this setup as "fork".
 
## Fork (salvageable) {#fork_upstream_is_not_origin_parent}

Here is one last fork setup that's sub-optimal, but it can be salvaged.


\begin{center}\includegraphics[width=0.6\linewidth]{img/fork_upstream_is_not_origin_parent} \end{center}

This is what happens when you do fork-and-clone and you *only* do fork-and-clone.
What's missing is a connection back to the source repo.

How does this happen?

* Cloning your own fork, either via `git clone` in the shell or through a Git client, such as RStudio. And then stopping here.

If you only plan to make one pull request, this setup is fine.
When the exchange is done, delete your local repo and your fork and move on with your life.
You can always re-fork in the future.
But if your pull request stays open for a while or if you plan to make repeated contributions, you'll need to pull ongoing developments in the source repo into your local copy.

You can convert this into the ideal [fork setup](#fork-them) like so:

* Detailed instructions are in 
  [Finish the fork and clone setup](#fork-and-clone-finish).
* Add the source repo as the `upstream` remote.
* Set `upstream/main` as the upstream tracking branch for local `main`
  (substitute whatever your default branch is called).

Next time you do fork-and-clone, consider using `usethis::create_from_github(fork = TRUE)` instead, which completes all of this setup in one go.

usethis describes this setup as "fork_upstream_is_not_origin_parent".

<!--chapter:end:remote-setups-common.Rmd-->

# Equivocal remote setups {#equivocal}

Just like the previous section about the most common setups, we only consider a very constrained set of remotes:

* The remote is on GitHub, e.g. its URL looks something like `https://github.com/OWNER/REPO.git` or `git@github.com:OWNER/REPO.git`.
* The remote is named `origin` or `upstream`.

The setups described here are characterized by *incomplete information*.
This section exists mostly to explain feedback that the usethis package might give about a GitHub remote configuration.

To identify any of the remote setups described in section \@ref(common-remote-setups), we need information from GitHub:

  * Whether you can push to a repo
  * Whether a repo is a fork
  * For a fork, what is its source repo

Sometimes some of this information is publicly available, but some of it never is, such as repo permissions.
This means that programmatic access to this information, i.e. requests to the GitHub API, generally requires authorization by an authenticated GitHub user.

This means that client packages, like usethis, work best when you have configured a GitHub personal access token (PAT).
See section \@ref(get-a-pat) for more details on why and how to do that.

If you've configured a PAT and are being told your GitHub config is problematic, consider these other explanations:
Are you offline?
Is GitHub down?
Have you lost permission to access the repo?
Has your PAT expired?
By default, they now expire after 30 days.

## Maybe "ours" or "theirs"

When we detect just one GitHub remote, but we can't verify the info above, usethis describes the setup as "maybe_ours_or_theirs".


\begin{center}\includegraphics[width=0.6\linewidth]{img/maybe_ours_or_theirs} \end{center}

Once a PAT is available, this setup can be identified as being ["ours" (belonging to you)](#ours-you), ["ours" (but belonging to someone else)](#ours-them), or ["theirs"](#theirs).

## Maybe fork

When we detect two GitHub remotes, but we can't verify the info above, usethis describes the setup as "maybe_fork".


\begin{center}\includegraphics[width=0.6\linewidth]{img/maybe_fork} \end{center}

Once a PAT is available, this setup can be identified as being a well-configured [fork](#fork-them) or a [fork with incomplete setup](#fork_upstream_is_not_origin_parent) (or possibly something more weird).

## How to fix

These setups aren't necessarily broken, but usethis needs more information to operate.

To "fix" this, set up a GitHub personal access token.
See section \@ref(get-a-pat) for more details on why and how to do that.

<!--chapter:end:remote-setups-equivocal.Rmd-->

# (PART) Daily Workflows {-} 

# Useful Git patterns for real life {#workflows-intro .unnumbered}

*Much of this originates as live workshop materials; the unlinked workflows are planned but not yet converted to prose here.*

Git patterns that come up frequently in real work:

  * Commit early and often. Push less often. [The Repeated Amend](#repeated-amend).
  * [Help, my push was rejected!](#push-rejected)
  * [Integrating remote and local work](#pull-tricky). Probably so you can push again.
  * Burn it all down.
  * Time travel:
    - ["I just need to see the past".](#time-travel-see-past) Browse and search on GitHub.
    - "I need to visit the past". Create a checkout a branch.
    - "I want to return to the past". `git revert`, `git reset`
    - "I had a great cookie last October". `git cherry pick`, `git checkout REF -- path`

Play well with others:

  * [Fork and clone](#fork-and-clone).
  * [Get upstream changes for a fork](#upstream-changes).
  * Disposable fork.
  * [Make your repo rewarding to browse on GitHub](#workflows-browsability).
  * [Explore and extend a pull request](#pr-extend)

<!--chapter:end:workflows-intro.Rmd-->

# The Repeated Amend {#repeated-amend}

One of the principal joys of version control is the freedom to experiment without fear.
If you make a mess of things, you can always go back to a happier version of your project.
We describe several methods of such time travel in *link to come*.
But you must have a good commit to fall back to!

## Rock climbing analogy

<div class="figure">
  <blockquote>
Using a Git commit is like using anchors and other protection when climbing. If you're crossing a dangerous rock face you want to make sure you've used protection to catch you if you fall. Commits play a similar role: if you make a mistake, you can't fall past the previous commit. Coding without commits is like free-climbing: you can travel much faster in the short-term, but in the long-term the chances of catastrophic failure are high! Like rock climbing protection, you want to be judicious in your use of commits. Committing too frequently will slow your progress; use more commits when you're in uncertain or dangerous territory. Commits are also helpful to others, because they show your journey, not just the destination.
  </blockquote>
  <p class="caption">
  <a href="http://r-pkgs.had.co.nz/git.html#git-commit">R Packages, Hadley Wickham</a> (@r-pkgs-book)</p>
</div>

Let's talk about this:

> use more commits when you're in uncertain or dangerous territory

When I'm doing something tricky, I often proceed towards my goal in small increments, checking that everything still works along the way.
Yes it works?
Make a commit.
This is my new worst case scenario.
Keep going.

What's not to love?

This can lead to an awful lot of tiny commits.
This is absolutely fine and nothing to be ashamed of.
But one day you may start to care about the utility and aesthetics of your Git history.

The Repeated Amend is a pattern where, instead of cluttering your history with lots of tiny commits, you build up a "good" commit gradually, by amending.

*Yes, there are other ways to do this, e.g. via squashing and interactive rebase, but I think amending is the best way to get started.*

## Workflow sketch

### Initial condition

Start with your project in a functional state:

* R package? Run your tests or `R CMD check`.
* Data analysis? Re-run your script or re-render your `.Rmd` with the new chunk.
* Website or book? Make sure the project still compiles.
* You get the idea.

Make sure your "working tree is clean" and you are synced up with your GitHub remote. `git status` should show something like:

```console
~/tmp/myrepo % git status                                                          
On branch main
Your branch is up to date with 'origin/main'.

nothing to commit, working tree clean
```

### Get to work

Imagine we start at commit C, with previous commit B and, before that, A:

``` bash
... -- A -- B -- C
```

Make a small step towards your goal.
Re-check that your project "works".

Stage those changes with and make a commit with the message "WIP", meaning "work in progress".
Do this in RStudio or in the shell (Appendix \@ref(shell)):

```console
git add path/to/the/changed/file
git commit -m "WIP"
```

The message can be anything, but "WIP" is a common convention.
If you use it, whenever you return to a project where the most recent commit message is "WIP", you'll know that you were probably in the middle of something.
If you push a "WIP" commit, on purpose or by mistake, it signals to other people that more commits might be coming.

Your history now looks like this:

``` bash
A -- B -- C -- WIP*
```

**Don't push!**
The `*` above signifies a commit that exists only in your local repo, not (yet) on GitHub.
If you called `git status`, you'd see something like "Your branch is ahead of 'origin/main' by 1 commit.", which is also displayed in RStudio's Git pane.

Do a bit more work.
Re-check that your project is still in a functional state.
Stage and commit again, but this time **amend** your previous commit.
RStudio offers a check box for "Amend previous commit" or in the shell:

```console
git commit --amend --no-edit
```

The `--no-edit` part retains the current commit message of "WIP".

**Don't push!**  Your history now looks like this:

``` bash
A -- B -- C -- WIP*
```

but the changes associated with the `WIP*` commit now represent your last two commits, i.e. all the accumulated changes since state C.

Keep going like this.

Let's say you've finally achieved your goal. One last time, check that your project is functional and in a state you're willing to share with others.

Commit, amending again, but with a real commit message this time.
Think of this as commit D.
Push.
Do this in RStudio or the shell:

```console
git commit --amend -m "Implement awesome feature; closes #43"
git push
```

Your history -- and that on GitHub -- look like this:

``` bash
A -- B -- C -- D
```

As far as the world knows, you implemented the feature in one fell swoop.
But you got to work on the task incrementally, with the peace of mind that you could never truly break things.

## What if I need to fall back?

Imagine you're in the middle of a Repeated Amend workflow:

```console
A -- B -- C -- WIP*
```

and you make some changes that break your project, e.g. tests start failing.
These bad changes are not yet committed, but they are saved.
You want to fall back to the last good state, represented by `WIP*`.

In Git lingo, you want to do a **hard reset** to the `WIP*` state.
Your local files will be forcibly reset to their state as of the `WIP*` commit.
With the command line:

```console
git reset --hard
```

which is implicitly the same as

```console
git reset --hard HEAD
```

which says: "reset my files to their state at the most recent commit".

This is also possible in RStudio.
In fact, the RStudio way makes it easier to selectively reset only specific files or only certain changes.
Click on "Diff" or "Commit".
Select a file with changes you do not want.
Use "Discard All" to discard all changes in that file.
Use "Discard chunk" to discard specific changes in a file.
Repeat this procedure for each affected file until you are back to an acceptable state.
Carry on.

If you committed a bad state, go to *link to come* for more reset scenarios.

## Why don't we push intermediate progress?

Amending a commit is an example of what's called "rewriting Git history".

Rewriting history that has already been pushed to GitHub -- and therefore potentially pulled by someone else -- is a controversial practice.
Like most controversial practices, lots of people still indulge in it, as do I.

But there is the very real possibility that you create headaches for yourself and others, so in Happy Git we must recommend that you abstain.
Once you've pushed something, consider it written in stone and move on.

## Um, what if I did push?

I told you not to!

But OK here we are.

Let's imagine you pushed this state to GitHub by mistake:

```console
A -- B -- C -- WIP (85bf30a)
```

and proceeded to `git commit --amend` again locally, leading to this state:

```console
A -- B -- C -- WIP* (6e884e6)
```

I'm deliberately showing two histories that sort of look the same, in terms of commit messages.
But the last SHA reveals they are actually different.

You are in a pickle now, as you can't do a simple push or pull.
A push will be rejected and a pull will probably lead to a merge that you don't want.

You have two choices:

* If you have collaborators who may have pulled the repo at commit
  `WIP (85bf30a)`, you have to regard that particular history as being written
  in stone now.
  If there is any very precious work that only exists locally, such as a
  specific file, save a copy of that to a new file path, temporarily.
  Hard reset your local repo to `C` (`git reset --hard HEAD^`) and pull from
  GitHub.
  GitHub and local history now show this:
  ```console
  A -- B -- C -- WIP (85bf30a)
  ```
  If you saved some precious work to a temporary file path, bring it back into
  the repo now; save, stage, commit, and push.
  GitHub and local history now show this:
  ```console
  A -- B -- C -- WIP (85bf30a) -- E
  ```
* If you have no collaborators or you have reason to believe they have not
  pulled, you can rewrite history, even on GitHub.
  You might as well make sure your local commit has a real, non-"WIP" message
  at this point.
  Force push your history to GitHub (`git push --force`).
  GitHub and local history now show this:
  ```console
  A -- B -- C -- D
  ```

In both cases, you've made the changes you want and your local repo and the 
GitHub remote are synced up again.
The history is nicer in the second case, but that's a secondary issue.

*There are many different ways to rewrite history and rescue some of these situations, but we find the approaches described above to be very approachable.*

<!--chapter:end:workflows-repeated-amend.Rmd-->

# Dealing with push rejection {#push-rejected}

Problem: You want to push changes to GitHub, but you are rejected like so:

``` bash
$ git push
To https://github.com/YOU/REPO.git
 ! [rejected]        main -> main (fetch first)
error: failed to push some refs to 'https://github.com/YOU/REPO.git'
hint: Updates were rejected because the remote contains work that you do
hint: not have locally. This is usually caused by another repository pushing
hint: to the same ref. You may want to first integrate the remote changes
hint: (e.g., 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
```

This means that your local Git history and that on the GitHub remote are not compatible, i.e. they have diverged.

I suggest that you use `git status`, your [Git client](#git-client ), or visit your GitHub remote in the browser to get more information about the situation, i.e. to get a sense of this work that you do not have.

In the abstract, this is the state on GitHub:

```
A -- B -- C (on GitHub)
```

And this is your local state:

```
A -- B -- D (what you have)
```

You can't cause some sort of merge to happen to the GitHub copy when you push. 

Instead, you've got to pull the commit `C` and somehow integrate it into your `D`-containing history. Then you will be able to push again.

This is covered in the workflow [Pull, but you have local work](#pull-tricky).

But before you behold the full horror of that, this is a great time to reflect on what we can learn from this situation.

## She who pushes first wins!

You may have noticed that you -- the author of `D` -- are faffing around with Git more than the person who committed and pushed `C`, i.e. your collaborator.

There is a lesson to be learned here!

If you had pushed `D` first, you'd be relaxing and they'd be figuring out how to integrate `C` into their history in order to push. So push your work often. Don't go dark and work "offline" for long stretches of time.

Obviously, you should push work to `main` because it's "ready" to share (or at least "ready enough"), not to avoid Git merges.

There is a truly legitimate point here: It is better for the overall health of a project to be committing, pushing, and integrating more often, not less. This does not eliminate the need to integrate different lines of work, but it makes each integration smaller, less burdensome, and less prone to error.

## Stay in touch

Another take away is this: the sooner you know about `C`, the better. Pull (or fetch) often.

Let's think about your commit `D`. Maybe it was built up over a couple of days via the [Repeated Amend pattern](#repeated-amend). Maybe `C` was sitting there on GitHub the whole time or appeared very early in your process.

Consider that it might be easier to integrate `C` into your work `D` sooner rather than later. Sometimes this is not true, but more often it is.

In general, it pays off to be proactively aware of what others are doing (e.g. to pull or fetch often) than to always be in reactive mode, learning about your collaborator's work only when your push is rejected.

## Use branches

Finally, your early experiences collaborating with others and yourself in `main` will give you a visceral understanding of why most Git users eventually start to use [branches](#git-branches).

Branches afford explicit workflows for integrating different lines of work on your own terms. This is much nicer than trying to do a tricky merge or rebase in a frustrated panic, because you need to push your work to GitHub at the end of the day.


<!--chapter:end:workflows-push-rejected.Rmd-->

# Pull, but you have local work {#pull-tricky}

Problem: You want to pull changes from upstream, but you have done some new work locally since the last time you pulled. This often comes up because [what you actually want to do is *push*](#push-rejected), but Git won't let you until you first incorporate the upstream changes.

For the sake of simplicity, assume we're dealing with the `main` branch and the remote is called `origin`.

Recent commit history of `origin/main`:

``` sh
A--B--C
```

Recent commit history of the local `main` branch:

``` sh
A--B--D
```

or maybe

``` sh
A--B--(uncommitted changes)
```

Your goal: get commit `C` into your local branch, while retaining the work in commit `D` or your uncommitted changes.

  * Local state is `A--B--(uncommitted changes)`: You could use `git stash`. Or you could just make a commit to simplify your life (see next bullet).
  * Local state is `A--B--D`: You can get to `A--B--C--D` or `A--B--(something that includes C and D)`.
  * Local state is `A--B--D--(uncommitted changes)`: You could just make a commit -- a new one or amend `D` -- to simplify your life (see previous bullet).
  
We prioritize simple approaches that are good for early Git use, but mention nicer long-term alternatives.

## Local work is uncommitted

Remote state is `A--B--C`.  
Local state is `A--B--(uncommitted changes)`.

### Happy simple cases

There are two happy scenarios, in which `git pull` will "just work":

  * You've introduced completely new files that don't exist in the remote branch and, therefore, cannot possibly have conflicting changes. You're in luck! You can just `git pull`.
  * The files affected by your local work have ZERO overlap with the files affected by the changes you need to pull from the remote. You're also in luck! You can just `git pull`.
  
Summary of these happy `git pull` scenarios:

``` sh
                 Remote: A--B--C

Local before 'git pull': A--B--(uncommitted changes)
 Local after 'git pull': A--B--C--(uncommitted changes)
```

What has actually happened here is that `git pull` resulted in a *fast-forward merge*, i.e. we placed commit `C` right on the end of your history. This would also be the case in the simpler situation where recent local history was just `A--B`, i.e. you had not added any local work since the last sync up with `origin/main`.

### `git stash` works, sometimes

If your changes affect a file (`foo.R` in the example below) that has also been changed in commit `C`, you cannot `git pull`. It doesn't hurt to try, but you will fail and it will look something like this:

``` sh
jenny@2015-mbp ethel $ git pull
remote: Enumerating objects: 5, done.
remote: Counting objects: 100% (5/5), done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 1), reused 1 (delta 0), pack-reused 0
Unpacking objects: 100% (3/3), done.
From github.com:jennybc/ethel
   db046b4..2d33a6f  main     -> origin/main
Updating db046b4..2d33a6f
error: Your local changes to the following files would be overwritten by merge:
        foo.R
Please commit your changes or stash them before you merge.
Aborting
```

Now what? First, you must safeguard your local changes by either stashing or committing them. (I personally would choose to commit and execute a workflow described in \@ref(git-pull-with-local-commits).)

I am not a big fan of `git stash`; I think it's usually better to take every possible chance to solidify your skills around core concepts and operations, e.g., make a commit, possibly in a branch. But if you want to use `git stash`, this opportunity is as good as it gets.

`git stash` is a way to temporarily store some changes to get them out of the way. Now you can do something else, without a lot of fuss. In our case, "do something else" is to get the upstream changes with a nice, simple `git pull`. Then you reapply and delete the stash and pick up where you left off.

For more details about stashing, I recommend

  * The stashing coverage in the "Filesystem interactions" chapter of Git in Practice ([book website](https://gitinpractice.com) or [read on GitHub](https://github.com/GitInPractice/GitInPractice#readme))
  * [7.3 Git Tools - Stashing and Cleaning](https://git-scm.com/book/en/v2/Git-Tools-Stashing-and-Cleaning) in [Pro Git](https://git-scm.com/book/en/v2).

Here's the best case scenario for "stash, pull, unstash" in the example above:

``` bash
git stash save
git pull
git stash pop
```

And here's the output from our example:

``` sh
jenny@2015-mbp ethel $ git stash save
Saved working directory and index state WIP on main: db046b4 Merge branch 'main'of github.com:jennybc/ethel

jenny@2015-mbp ethel $ git pull
Updating db046b4..2d33a6f
Fast-forward
 foo.R | 2 +-
 1 file changed, 1 insertion(+), 1 deletion(-)

jenny@2015-mbp ethel $ git stash pop
Auto-merging foo.R
On branch main
Your branch is up-to-date with 'origin/main'.

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   foo.R

no changes added to commit (use "git add" and/or "git commit -a")
Dropped refs/stash@{0} (012c4dcd3a4c3af6757c4c3ca99a9eaeff1eb2a4)
```

That is what success looks like. You've achieved this:

``` sh
      Remote: A--B--C

Local before: A--B--(uncommitted changes)
 Local after: A--B--C--(uncommitted changes)
```

As above, we have just enjoyed a fast-forward merge, made possible by temporarily stashing then unstashing the uncommitted local changes.

### `git stash` with conflicts

If your local changes have some overlap with changes you are pulling, you will, instead get a merge conflict from `git stash pop`. Now you have some remedial work to do. In this case, you have gained nothing by using `git stash` in the first place, which explains my general lack of enthusiasm for `git stash`.

Here's how to execute the `git stash` workflow in our example, in the face of conflicts (based on [this Stack Overflow answer](https://stackoverflow.com/a/27382210/2825349)):

``` sh
jenny@2015-mbp ethel $ git stash save
Saved working directory and index state WIP on main: 2d33a6f Back to 5

jenny@2015-mbp ethel $ git pull
Updating 2d33a6f..1eddf9e
Fast-forward
 foo.R | 1 +
 1 file changed, 1 insertion(+)
 
jenny@2015-mbp ethel $ git stash pop
Auto-merging foo.R
CONFLICT (content): Merge conflict in foo.R
```

At this point, you must resolve the merge conflict (*future link*). Literally, at each locus of conflict, pick one version or the other (upstream or stashed) or create a hybrid yourself. Remove the all the markers inserted to demarcate the conflicts. Save.

Since `git stash pop` did not go smoothly, we need to manually reset (*future link*) and delete the stash to finish.

``` sh
jenny@2015-mbp ethel $ git reset
Unstaged changes after reset:
M       foo.R

jenny@2015-mbp ethel $ git stash drop
Dropped refs/stash@{0} (7928db50288e9b4d934803b6b451a000fd7242ed)
```

Phew, we are done. We've achieved this:

``` sh
      Remote: A--B--C

Local before: A--B--(uncommitted changes)
 Local after: A--B--C--(uncommitted changes*)
```

The asterisk on `uncommitted changes*` indicates that your uncommitted changes might now reflect adjustments made when you resolved the conflicts.

## Local work is committed {#git-pull-with-local-commits}

Remote state is `A--B--C`.  
Local state is `A--B--D`.

### Pull (fetch and merge)

The simplest option is to fetch the commits from upstream and merge them, which is what `git pull` does. This is a good option if you're new to Git. It leads to a messier history, but when you are new, this is the least of your worries. Merge, be happy, and carry on.

Here is the best case, no-merge-conflicts version of `git pull`:

``` sh
jenny@2015-mbp ethel $ git pull

< YOU WILL PROBABLY BE KICKED INTO AN EDITOR HERE RE: MERGE COMMIT MESSAGE! >

Merge made by the 'recursive' strategy.
 README.md | 4 ++--
 1 file changed, 2 insertions(+), 2 deletions(-)
```

Depending on your version of Git, your config, and your use of a GUI, you might be required to confirm/edit a commit message for the merge commit.

Or what if things don't go this smoothly? If commit `C` (on the remote) and commit `D` (local) have changes to the same parts of one or more files, Git may not be able to automatically merge and you will get merge conflicts. It will look something like this:

``` sh
jenny@2015-mbp ethel $ git pull
Auto-merging foo.R
CONFLICT (content): Merge conflict in foo.R
Automatic merge failed; fix conflicts and then commit the result.
```

You must resolve these conflicts (*future link*). Literally, at each locus of conflict, pick one version or the other (upstream or local) or create a hybrid yourself. Remove the all the markers inserted to demarcate the conflicts. Save.

Mark the affected file `foo.R` as resolved via `git add` and make an explicit `git commit` to finalize this merge.

``` sh
jenny@2015-mbp ethel $ git add foo.R
jenny@2015-mbp ethel $ git commit
[main 20b297b] Merge branch 'main' of github.com:jennybc/ethel
```

Again, do not be surprised if, during `git commit`, you find yourself in an editor, confirming/editing the commit message for the merge commit.

We've achieved this:

``` sh
      Remote: A--B--C

Local before: A--B--D
 Local after: A--B--D--(merge commit)
                  \_C_/
```

### Pull and rebase

`git pull --rebase` creates a nicer history than `git pull` when integrating local and remote commits. It avoids a merge commit, so the history is less cluttered and is linear. It can make merge conflicts more onerous to resolve, which is why I still recommend `git pull` as the entry-level solution.

Here is the best case, no-merge-conflicts version of `git pull --rebase`:

```
jenny@2015-mbp ethel $ git pull --rebase
First, rewinding head to replay your work on top of it...
Applying: Take max
```

Notice that you were NOT kicked into an editor to fiddle with the commit message for the merge commit, because there is no merge commit! This is the beauty of rebasing.

We've achieved this:

``` sh
      Remote: A--B--C

Local before: A--B--D
 Local after: A--B--C--D
```

It is as if we pulled the upstream work in commit `C`, then did the local work embodied in commit `D`. We have no cluttery merge commits and a linear history. Nice!

The bad news: As with plain vanilla `git pull`, it is still possible to get merge conflicts with `git pull --rebase`. If you have multiple local commits, you can even find yourself resolving conflicts over and over, as these commits are sequentially replayed. Hence this is a better fit for more experienced Git users and in situations where conflicts are unlikely (those tend to be correlated, actually).

At this point, if you try to do `git pull --rebase` and get bogged down in merge conflicts, I recommend `git rebase --abort` to back out. For now, just pursue a more straightforward strategy.

## Other approaches

There are many more ways to handle this situation, which you can discover and explore as you gain experience and start to care more about the history. We sketch some ideas here.

### Use a temporary branch for local work

Recall:  
Remote state is `A--B--C`.  
Local state is `A--B--(uncommitted changes)`.

This is an alternative to the stash workflow that has the advantage of giving you practice with Git techniques that are more generally useful. It also leads to a nice history.

Create a new, temporary branch and commit your uncommitted changes there. Checkout `main` and `git pull` to get changes from upstream. You now need to recover the work from the commit in the temporary branch. Options:

  * Merge the temporary branch into `main`.
  * Cherry pick the commit from the temporary branch into `main`.
  
In either case, it is still possible you will need to deal with merge conflicts.

In either case, if you felt forced to commit before you were ready or to accept an ugly merge commit, you can either do a mixed reset to "uncommit" but keep the changes on `main` or keep amending until you are satisfied with the commit.

## Some local work is committed, some is not

This is an awkward hybrid situation that can be handled with a combination of strategies seen above: make a pragmatic commit on `main` or a temporary branch. Integrate the upstream and local changes in `main`. If you aren't happy with the final pragmatic commit (which only exists locally), reset or amend until you are.

<!--chapter:end:workflows-pull.Rmd-->

# Time travel: See the past {#time-travel-see-past}

<!-- http://www.commitstrip.com/en/2019/01/28/git-lfs/? -->

Sometimes you just need to **see** various files in your project as they were at some significant moment in the past. Examples:

  * "I liked the color scheme of this plot better in last week's draft". "What's up with that new funky outlier in figure 2?"
    - Here you'll want to visit scripts and source data as they were the last time you generated visualizations to share with this colleague.
  * "The build has been failing on Windows for two weeks."
    - Here you'll want to inspect package source at the "last known good" version and scrutinize subsequent commits.

All projects move through various states that you regard as "good" vs. "bad" or something in between. It can be useful to explore the past, when trying to get into a "good" state.

## Hyperlinks are awesome!

This is where GitHub (and GitLab or BitBucket) really shine. The ability to quickly explore different commits/states, switch between branches, inspect individual files, and see the discussion in linked issues is incredibly powerful.

Yes, technically, you can visit past states of your project using Git commands locally. But it is significantly more cumbersome. You generally have to checkout these previous states, which raises the prospect of getting comfortable in the "detached head" state and unintentionally making new commits on the wrong branch or on no branch at all.

GitHub's hyperlink-rich presentation of your repo and its history is one of the top reasons to sync local work to a copy on GitHub, even if you keep it private. It can be much easier to hone in on a state or change of interest by clicking around or using GitHub's search features. Also, because it is so clearly a remote and read-only action, there is no possibility of goofing up local state or committing new work to the wrong branch.

## Browse commit history and specific commits

From your repo's landing page, access commit history by clicking on "xyz commits". This is like using `git log` locally, but much more rewarding. If you have a good [local Git client](#git-client), it probably also provides a graphical overview of history.

\begin{figure}
\includegraphics[width=1\linewidth]{img/screenshots/github-link-to-commits} \caption{Link to commit listing on GitHub.}(\#fig:github-link-to-commit-listing)
\end{figure}

Once you're viewing the history, notice three ways to access more info for each commit:

  1. The clipboard icon copies the SHA-1 of the commit. This can be handy if you need to refer to this commit elsewhere, e.g. in an issue thread or a commit message or in a Git command you're forming for local execution.
  1. Click on the abbreviated SHA-1 itself in order to the view the diff associated with the commit.
  1. Click on the double angle brackets `<>` to browse the state of the entire repo at that point in history.

\begin{figure}
\includegraphics[width=1\linewidth]{img/screenshots/github-commit-listing} \caption{Example of a commit listing on GitHub.}(\#fig:github-commit-listing)
\end{figure}

Back out of any drilled down view by clicking on `YOU/REPO` to return to your repo's landing page. This brings you back to the present state and top-level of your repo.

### Use hyperlinks yourself!

Once you've identified a relevant commit, diff, or file state, you can copy the current URL from your browser and use it to enhance online discussion elsewhere, i.e. to bring other people to this exact view of the repo. The hyperlink-iness of repos hosted on GitHub can make online discussion of a project much more precise and efficient.

## File driven inquiries

What if you're interested in how a specific file came to be the way it is? First navigate to the file, then notice "Blame" and "History" in the upper right.

\begin{figure}
\includegraphics[width=1\linewidth]{img/screenshots/github-specific-file} \caption{Visiting a specific file on GitHub.}(\#fig:github-specific-file)
\end{figure}

### Blame

The "blame" view of a file is related to what `git blame` does on the command line. It reveals who last touched each line of the file, how long ago, and the associated commit message. Click on the commit message to visit that commit. Or click the "stacked rectangles" icon to move further back in time, but staying in blame view. This is handy when doing forensics on a specific and small set of lines.

*add a screenshot (and update that above) but first pick a better example than Happy Git, i.e. one with more contributors / more interesting history*

### History

The "history" view for a file is very much like the overall commit history described above, except it only includes commits that affect the file of interest. This can be handy when your inquiry is rather diffuse and you're trying to digest the general story arc for a file.

### Hyperlink to specific lines at a specific state

When viewing a file on GitHub, you can click on a line number to highlight it. Use "click ... shift-click" to select a range of lines. Notice your browser's URL shows something of this form:

``` bash
https://github.com/OWNER/REPO/blob/SHA/path/to/file.R#L27-L31
```

If the URL does not contain the SHA, type "y" to toggle into that form.

These file- and SHA-specific URLs are a great way to point people at particular lines of code in online conversations. It's best practice to use the uglier links that contain the SHA, as they will stand the test of time.

## Search

Search is always available in the upper-righthand corner of GitHub.

\begin{figure}
\includegraphics[width=1\linewidth]{img/screenshots/github-repo-search} \caption{Typing into GitHub search bar.}(\#fig:github-repo-search)
\end{figure}

Once you enter some text in the search box, a dropdown provides the choice to search in the current repo (the default) or all of GitHub. GitHub searches the contents of files (described as "Code"), commit messages, and issues. Take advantage of the search hits across these different domains. Again, this is a powerful way to zoom in on specific lines of code, revisit an interesting time in project history, or re-discover a conversation thread.

### Issue search

If you want to search issues specifically, the search box on any repo's Issues page is prepopulated with the filters `is:issue` and `is:open`.


<!--chapter:end:workflows-see-the-past.Rmd-->

# Fork and clone {#fork-and-clone}

Use **fork and clone** to get a copy of someone else's repo if there's any chance you will want to propose a change to the owner, i.e. send a pull request.
If you are waffling between "just clone" and "fork and clone", go with "fork and clone".

We want to achieve this:


\begin{center}\includegraphics[width=0.6\linewidth]{img/fork-and-clone} \end{center}

Below we show a couple of methods for fork and clone and you should pick one:

* Use a combination of the browser, command line Git, and RStudio
* Via `usethis::create_from_github()`

Vocabulary: `OWNER/REPO` refers to what we call the **source** repo, owned by `OWNER`, who is not you.
`YOU/REPO` refers to your fork, i.e. your remote copy of the source repo, on GitHub.
This is the same vocabulary used elsewhere, such as the chapter on [common remote configurations](#common-remote-setups).

This is a good time to navigate to the [GitHub](https://github.com) repo of interest, i.e. the source repo `OWNER/REPO`.

## Fork and clone without usethis

I assume you're already visiting the source repo in the browser.
In the upper right hand corner, click **Fork**.

This creates a copy of `REPO` in your GitHub account and takes you there in the browser.
Now we are looking at `YOU/REPO`.

**Clone** `YOU/REPO`, which is your copy of the repo, a.k.a. your fork, to your local machine.
Make sure to clone your repo, not the source repo.
Elsewhere, we describe multiple methods for cloning a remote repo.
Pick one:

  * The [cloning instructions in Existing project, GitHub first](#git-clone-usethis-rstudio)
    cover usethis and RStudio.
  * The [cloning instructions in Connect to GitHub](#git-clone-command-line)
    show how to do this with command line Git.

Make a conscious decision about the local destination directory and HTTPS vs SSH URL.

### Finish the fork and clone setup {#fork-and-clone-finish}

If you stop at this point, you have what I regard as an incomplete setup, described elsewhere as ["fork (salvageable)"](#fork_upstream_is_not_origin_parent).


\begin{center}\includegraphics[width=0.6\linewidth]{img/fork-no-upstream-sad} \end{center}

This is sad, because there is no direct connection between your local copy of the repo and the source repo `OWNER/REPO`.

There are two more recommended pieces of setup:

* Configure the source repo as the `upstream` remote
* Configure your local `main` branch (or whatever the default is) to track
  `upstream/main`, not `origin/main`
  
The nickname `upstream` can technically be whatever you want.
There is a strong tradition of using `upstream` in this context and, even though I have better ideas, I believe it is best to conform.
Every book, blog post, and Stack Overflow thread that you read will use `upstream` here.
Save your psychic energy for other things.
  
These steps make it easier for you to stay current with developments in the source repo.
We talk more below about why you should never commit to the default branch, e.g. `main`, when you're working in a fork (see \@ref(fork-dont-touch-main)).

### Configure the `upstream` remote {#fork-configure-upstream}

The first step is to get the URL of the **source** repo `OWNER/REPO`.
Navigate to the source repo on GitHub.
It is easy to get to from your fork, `YOU/REPO`, via the "forked from" link in the upper left.

Use the big green "Code" button to get the URL for `OWNER/REPO` on your clipboard.
Be intentional about whether you copy the HTTPS or SSH URL.

You can configure the `upstream` remote with command line Git, usethis, or RStudio.

Here's how to use command line Git in a shell:

``` bash
git remote add upstream https://github.com/OWNER/REPO.git
```

`usethis::use_git_remote()` allows you to configure a Git remote.
Execute this in R:


``` r
usethis::use_git_remote(
  name = "upstream",
  url = "https://github.com/OWNER/REPO.git"
)
```

Finally, you can do this in RStudio, although it feels a bit odd.
Click on "New Branch" in the Git pane ("two purple boxes and a white square").


\begin{center}\includegraphics[width=0.6\linewidth]{img/rstudio-new-branch} \end{center}

This will reveal a button to "Add Remote".
Click it.
Enter `upstream` as the remote name and paste the URL for `OWNER/REPO` that you got from GitHub.
Click "Add".
Decline the opportunity to add a new branch by clicking "Cancel".

Regardless of how you configured `upstream`, do this in a shell:

``` bash
git fetch upstream
```

### Set upstream tracking branch for the default branch {#fork-set-upstream-tracking-main}

This is optional but highly recommended for most fork and clone situations.
We're going to set `upstream/main` from the source repo as the upstream tracking branch of local `main`.
(If your default branch has a different name, substitute accordingly.)

This is desirable so that a simple `git pull` pulls **from the source repo**, not from your fork.
It also means a simple `git push` will (attempt to) push to the source repo, which will almost always be rejected since you probably do not have permission.
This failure will alert you to the fact that you're doing something questionable, while it's still easy to back out.

First, fetch info for the `upstream` remote.
This is especially important if you just configured `upstream` for the first time.

``` bash
git fetch upstream
```

The two commands below do the same thing; the first is just shorthand for the second.
Do this with command line Git in a shell:

``` bash
git branch -u upstream/main
git branch --set-upstream-to upstream/main
```

If you found this fork and clone workflow long and tedious, consider using `usethis::create_from_github()` next time!

## `usethis::create_from_github("OWNER/REPO", fork = TRUE)` {#fork-and-clone-create-from-github}

The [usethis package](https://usethis.r-lib.org) has a convenience function, [`create_from_github()`](https://usethis.r-lib.org/reference/create_from_github.html), that can do "fork and clone" (as well as just clone).
The `fork` argument controls whether the source repo is cloned or fork-and-cloned.
Note that `create_from_github(fork = TRUE)` requires that you have [configured a GitHub personal access token](#https-pat).

I assume you're already visiting the source repo in the browser.
Now click the big green button that says "<> Code".
Copy a clone URL to your clipboard.
If you're taking our default advice, copy the HTTPS URL.
But if you're opting for SSH, then make sure to copy the SSH URL.

You can execute this next command in any R session.
If you use RStudio, then do this in the R console of any RStudio instance.
In either case, after successful completion, you should find yourself in the new project that is the local repo connected to your fork.


``` r
usethis::create_from_github(
  "https://github.com/OWNER/REPO",
  destdir = "~/path/to/where/you/want/the/local/repo/",
  fork = TRUE
)
```

The first argument is `repo_spec` and it accepts the GitHub repo specification in various forms.
In particular, you can use the URL we just copied for the source repo.

The `destdir` argument specifies the parent directory where you want the new folder (and local Git repo) to live.
If you don't specify `destdir`, usethis defaults to some very conspicuous place, like your desktop.
If you like to keep Git repos in a certain folder on your computer, you can personalize this default by setting the `usethis.destdir` option in your `.Rprofile`.

The `fork` argument specifies whether to clone (`fork = FALSE`) or fork and clone (`fork = TRUE`).
You often don't need to specify `fork` and can just enjoy the default behaviour, which is governed by your permissions on the source repo.
By default, `fork = FALSE` if you can push to the source repo and `fork = TRUE` if you cannot.

Here is what that might look like (note that we're accepting the default behaviour for many arguments):


``` r
usethis::create_from_github("https://github.com/OWNER/REPO")
#> ℹ Defaulting to 'https' Git protocol
#> ✔ Setting `fork = TRUE`
#> ✔ Creating '/some/path/to/local/REPO/'
#> ✔ Forking 'OWNER/REPO'
#> ✔ Cloning repo from 'https://github.com/YOU/REPO.git' into '/some/path/to/local/REPO'
#> ✔ Setting active project to '/some/path/to/local/REPO'
#> ℹ Default branch is 'main'
#> ✔ Adding 'upstream' remote: 'https://github.com/OWNER/REPO.git'
#> ✔ Pulling changes from 'upstream/main'.
#> ✔ Setting remote tracking branch for local 'main' branch to 'upstream/main'
#> ✔ Setting active project to '<no active project>'
```

For an RStudio user, `create_from_github(fork = TRUE)` does all of this:

* Forks the source repo on GitHub.
* Clones your fork to a new local repo (and RStudio Project).
  This configures your fork as the `origin` remote.
* Configures the source repo as [the `upstream` remote](#upstream-changes).
* Sets the upstream tracking branch for `main` (or whatever the default branch
  is) to `upstream/main`.
* Opens a new RStudio instance in the new local repo (and RStudio Project).

## Engage with the new repo

If you used `usethis::create_from_github()` or did fork and clone via [Existing project, GitHub first](#existing-github-first), you are probably in an RStudio Project for this new repo.

Regardless, get yourself into this project, whatever that means for you, using your usual method.

Explore the new repo in some suitable way.
If it is a package, you could run the tests or check it.
If it is a data analysis project, run a script or render an Rmd.
Convince yourself that you have gotten the code.

You should now be in the perfect position to sync up with ongoing developments in the source repo and to propose new changes via a pull request from your fork.


\begin{center}\includegraphics[width=0.6\linewidth]{img/fork-them-pull-request} \end{center}

You can use the commands below to review more of the nitty gritty Git details of your fork and clone setup:

* Command line Git in a shell:
  - `git remote -v`
  - `git remote show origin` (or `upstream`)
  - `git branch -vv`
* In R:
  - `usethis::git_remotes()`
  - `usethis::git_sitrep()`

In the shell, `git remote -v` should reveal that your remotes are configured like so:

``` bash
origin    https://github.com/YOU/REPO.git (fetch)
origin    https://github.com/YOU/REPO.git (push)
upstream  https://github.com/OWNER/REPO.git (fetch)
upstream  https://github.com/OWNER/REPO.git (push)
```

Comparable info is available In R with `usethis::git_remotes()`:


``` r
git_remotes()
#> $origin
#> [1] "https://github.com/YOU/REPO.git"
#> 
#> $upstream
#> [1] "https://github.com/OWNER/repo.git"
```

In the shell, with the default branch checked out, `git branch -vv` should reveal that `upstream/main` is the upstream tracking branch:

``` bash
~/some/repo/ % git branch -vv                   
* main 2739987 [upstream/main] Some commit message
```

All of this info about remotes and branches is also included in the rich information reported with `usethis::git_sitrep()`.

## Don't mess with `main` {#fork-dont-touch-main}

Here is some parting advice for how to work in a fork and clone and situation.

If you make any commits in your local repository, I **strongly recommend** that you work in [a new branch](#git-branches), not `main` (or whatever the default branch is called).

I **strongly recommend** that you do not make commits to `main` of a repo you have forked.
If you commit to `main` in a repo you don't own, it creates a divergence between that branch's history in the source repo and in your repo.
Nothing but pain will come from this.
(If you've already done this, we discuss how to fix the situation in [Um, what if I did touch `main`?](#touched-main).)

When you treat `main` as read-only, it makes life much easier when you want to [pull upstream work](#upstream-changes) into your copy.
The `OWNER` of `REPO` will also be happier to receive your pull request from a non-`main` branch.

For more detail, this Q&A on Stack Overflow is helpful: [Why is it bad practice to commit to your fork's master branch?](https://stackoverflow.com/q/33749832).

<!--chapter:end:workflows-fork-and-clone.Rmd-->

# Get upstream changes for a fork {#upstream-changes}

This workflow is relevant if you have done [fork and clone](#fork-and-clone) and now you need to pull subsequent changes from the source repo into your copy.
We are talking about both your fork (your remote copy of the repo, on GitHub) and your local copy.

This is the ideal starting situation:


\begin{center}\includegraphics[width=0.6\linewidth]{img/fork-them-pull-request} \end{center}

First, we're going to actively verify the above configuration.
If your setup is sub-optimal, we'll discuss how to address that.

## Verify your local repo's configuration

Vocabulary: `OWNER/REPO` refers to what we call the **source** repo, owned by `OWNER`, who is not you.
`YOU/REPO` refers to your fork, i.e. your remote copy of the source repo, on GitHub.
This is the same vocabulary used elsewhere, such as the chapter on [common remote configurations](#common-remote-setups).

### List your remotes

Let's inspect [the current remotes](#git-remotes) for your local repo.

You can check this with command line Git in the shell (Appendix \@ref(shell)):

``` bash
git remote -v
```

We want to see something like this:

``` bash
origin    https://github.com/YOU/REPO.git (fetch)
origin    https://github.com/YOU/REPO.git (push)
upstream  https://github.com/OWNER/REPO.git (fetch)
upstream  https://github.com/OWNER/REPO.git (push)
```

Comparable info is available in R with `usethis::git_remotes()`:


``` r
git_remotes()
#> $origin
#> [1] "https://github.com/YOU/REPO.git"
#> 
#> $upstream
#> [1] "https://github.com/OWNER/repo.git"
```

If you only have one remote, probably `origin`, I highly recommend you modify the remote configuration.
But first, we'll check one other thing.

### View the upstream tracking branch

Ideally, your local `main` branch has `upstream/main` as its upstream tracking branch.
Even you have a correctly configured `upstream` remote, this is worth checking.
If your default branch has a branch other than `main`, substitute accordingly.

In the shell, with the default branch checked out, `git branch -vv` should reveal that `upstream/main` is the upstream tracking branch:

``` bash
~/some/repo/ % git branch -vv                   
* main 2739987 [upstream/main] Some commit message
```

If, instead, you see `origin/main`, I highly recommend you reconfigure the tracking branch.

All of this info about remotes and branches is also included in the rich information reported with `usethis::git_sitrep()`.

### Repair or complete your repo's configuration

Instructions for adding the `upstream` remote and setting upstream tracking for your default branch are given in [Finish the fork and clone setup](#fork-and-clone-finish).

## Verify that your "working tree is clean"

We assume your repo has this favorable configuration:


\begin{center}\includegraphics[width=0.6\linewidth]{img/fork-them} \end{center}

Make sure you are on the default branch, e.g. `main`, and that your "working tree is clean".
First, let's make sure our information on the `upstream` remote is current:

``` bash
git fetch upstream
```

`git status` should now show something like:

``` bash
On branch main
Your branch is up to date with 'origin/main'.

nothing to commit, working tree clean
```

If you have modified files, you should either discard those changes or create a new branch and commit the changes there for safekeeping.

It's also fine if you see something like this:

```
Your branch is behind 'upstream/main' by 2 commits, and can be fast-forwarded.
```

However, if you see something like this:

```
Your branch is ahead of 'upstream/main' by 1 commit.
```

or this:

```
Your branch and 'upstream/main' have diverged,
and have 1 and 1 different commits each, respectively.
```

this is a sign that you have made some regrettable choices.

I recommend that you [never make your own commits to the default branch of a fork](#fork-dont-touch-main) or to any branch that you don't effectively (co-)own.
However, if you have already done so, we explain how to fix the problem in [Um, what if I did touch `main`?](#touched-main).

## Sync option 1: Pull changes from `upstream`, then push to `origin`

Now we are ready to pull the changes that we don't have from the source repo `OWNER/REPO` into our local copy.

``` bash
git pull upstream main --ff-only
```

This says: "pull the changes from the remote known as `upstream` into the `main` branch of my local repo".
I am being explicit about the remote (`upstream`) and the branch (`main`) in this case, both to make it more clear and to make this command robust to repo- and user-level Git configurations.
But if you've followed our setup recommendations, you don't actually need to be this explicit.

I also **highly recommend** using the `--ff-only` flag in this case, so that you also say "if I have made my own commits to `main`, please force me to confront this problem NOW".
Here's what it looks like if a fast-forward merge isn't possible:

``` bash
$ git pull upstream main --ff-only
From github.com:OWNER/REPO
 * branch              main     -> FETCH_HEAD
fatal: Not possible to fast-forward, aborting.
```

See [Um, what if I did touch `main`?](#touched-main) to get yourself back on the happy path.

Assuming you've succeeded with `git pull`, this next step is optional and many people who are facile with Git do not bother.

If you take my advice to [never work in `main` of a fork](#fork-dont-touch-main), then the state of the `main` branch in your fork `YOU/REPO` does not technically matter.
You will never make a pull request from `main` and there are ways to set the correct base for the branches and pull requests that you do create.

If, however, your grasp of all these Git concepts is tenuous at best, it can be helpful to try to keep things simple and orderly and synced up.

Feel free to push the newly updated state of local `main` to your fork `YOU/REPO` and enjoy the satisfaction of being "caught up" with `OWNER/REPO`, in both your remote fork and in your local repo.

In the shell:

``` bash
git push origin main
```

If you've followed our configuration advice, you really do need to be this explicit in order to push to `origin` (not `upstream`).

## Sync option 2: Sync your fork on GitHub, pull changes from `origin` to local repo

For many years, this was not possible, though many GitHub users wished for this feature.
Happily it is now possible to sync a fork with its source repo in the browser, i.e. to do the sync between the 2 GitHub repos.
The official GitHub documentation for this is [Syncing a fork branch from the web UI](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/working-with-forks/syncing-a-fork#syncing-a-fork-branch-from-the-web-ui).

Navigate to the main page of your fork `YOU/REPO`, i.e. your primary repo which is configured as the `origin` remote.

At the top you'll see some information on how the state of `main` in your fork relates to `main` in the source repo, similar to what we see with `git status` in the alternative approach above.
Ideally you will see something like:

```
This branch is 2 commits behind OWNER:main.
```

which indicates you can sync up in the ideal fast-forward sense.

If you see something like this:

```
This branch is 1 commit ahead, 2 commits behind OWNER:main.
```

this is a sign that you have made some regrettable choices.

I recommend that you [never make your own commits to the default branch of a fork](#fork-dont-touch-main) or to any branch that you don't effectively (co-)own.
However, if you have already done so, we explain how to fix the problem in [Um, what if I did touch `main`?](#touched-main).

Once you are ready to proceed, click "Sync fork" in the upper right corner.
Upon success, the main page of `YOU/REPO` shows something like

> This branch is up to date with `OWNER/REPO:main`.

If you have made commits on the default branch of your fork, which we [strongly advise against](#fork-dont-touch-main), this can result in a merge commit (or even merge conflicts).
If you are suffering due to commits you've made on `main` and it's beyond the help we describe below, consider deleting your fork and local repo and making a fresh start with [Fork and clone](fork-and-clone).
Live and learn.

Once you have successfully synced the default branch of `YOU/REPO` with the default branch of `OWNER/REPO`, you probably want to do the same for your local repo.
Since they are synced, you can pull from either `upstream` or `origin`.

In the shell, with the default branch checked out, execute one of these:

``` bash
git pull upstream main --ff-only
git pull origin main --ff-only
```

If you've followed our configuration advice, you don't actually need to specify the remote and branch, because this branch is configured to pull from `upstream`.
For the same reasons as before, it's a good idea to include the `--ff-only` flag.
If you have made local commits to `main`, this will surface that problem, which is solved in the next section.

## Um, what if I did touch `main`? {#touched-main}

I told you not to!

But OK here we are.

Let's imagine this is the state of `main` (or whatever the default branch is called) in the source repo `OWNER/REPO`:

``` bash
... -- A -- B -- C -- D -- E -- F
```

and and this is the state of the `main` branch in your local copy:

``` bash
... -- A -- B -- C -- X -- Y -- Z
```

The two histories agree, up to commit or state `C`, then they diverge.

If you want to preserve the work in commits `X`, `Y`, and `Z`, create a new branch right now, with tip at `Z`, like so, but substituting your preferred branch name:

``` bash
git checkout -b my-great-innovations
```

This safeguards your great innovations from commits `X`, `Y`, and `Z`.
Now checkout `main` again:

``` bash
git checkout main
```

I now assume you have either preserved the work in `X`, `Y`, and `Z` (with a branch) or have decided to let it go.

Do a hard reset of the `main` branch to `C`.

``` bash
git reset --hard C
```

You will have to figure out how to convey `C` in Git-speak.
Specify it relative to `HEAD` or provide the SHA.
See *future link about time travel* for more support.

<!-- TODO: come back when there is content about referring to previous states. -->

The history of your `main` branch is now compatible with its history in `OWNER/REPO`.
The instructions above for pulling changes from `upstream` should now work.
A fast-forward-only pull should succeed.

``` bash
git pull upstream main --ff-only
```

And now your local history for `main` should match that in the source repo:

``` bash
... -- A -- B -- C -- D -- E -- F
```

If you chose to create a branch with your work, you will also have that locally:


``` bash
... -- A -- B -- C -- D -- E -- F (main)
                   \
                    -- X -- Y -- Z (my-great-innovations)
```

If you pushed your alternative history (with commits `X`, `Y`, and `Z`) to your fork `YOU/REPO` and you like keeping everything synced up, you will also need to force push `main` to the `origin` remote:

``` bash
git push --force origin main
```

We really, really don't like discussing force pushes in Happy Git, though.
We only do so here, because we are talking about a fork, which is fairly easy to replace if things go sideways.

<!--chapter:end:workflows-upstream-changes-into-fork.Rmd-->

# Explore and extend a pull request {#pr-extend}

Scenario: you maintain an R package on GitHub with pull requests (PRs) from external contributors e.g. Jane Doe, janedoe on GitHub. Sometimes you need to experiment with the PR in order to provide feedback or to decide whether or not to merge. Going further, sometimes you want to add a few commits and then merge. Or maybe there are just some merge conflicts that require your personal, local attention. Let's also assume that you want the original PR author to get credit for their commits, i.e. you want to preserve history and provenance, not just diffs.

How do you checkout and possibly extend an external PR?

## Update from the future

The lessons learned here eventually lead to the `pr_*()` family of functions in usethis.
`pr_fetch()` and `pr_push()` are now my workhorses for exploring and extending PRs.
You can read more about usethis's functions to help with pull requests in their very own article: [Pull request helpers](https://usethis.r-lib.org/articles/pr-functions.html).

## Terminology

Vocabulary I use throughout.

**fork branch** The name of the branch in the fork from which the PR was made. Best case scenario: informative name like `fix-fluffy-bunny`. Worst case scenario: PR is from `master`.

**local PR branch** The name of the local branch you'll use to work with the PR. Best case scenario: can be same as fork branch. Worse case scenario: PR is from `master`, so you must make up a new name based on something about the PR, e.g. `pr-666` or `janedoe-master`.

**PR parent** The SHA of the commit in the main repo that is the base for the PR.

**PR remote** The SSH or HTTPS URL for the fork from which the PR was made. Or the nickname of the remote, if you've bothered to set that up.

## Official GitHub advice, Version 1

Every PR on GitHub has a link to "command line instructions" on how to merge the PR locally via command line Git. On this journey, there is a point at which you can pause and explore the PR locally.

Here are their steps with my vocabulary and some example commands:

  * Create and check out the local PR branch, anticipating its relationship to the fork branch. Template of the Git command, plus an example of how it looks under both naming scenarios:

        # Template of the Git command
        git checkout -b LOCAL_PR_BRANCH master 
        # How it looks under both naming scenarios
        git checkout -b fix-fluffy-bunny master 
        git checkout -b janedoe-master master 
    
  * Pull from the fork branch of the PR remote:
        
        # Template of the Git command
        git pull REMOTE FORK_PR_BRANCH
        # How it looks under both naming scenarios
        git pull https://github.com/janedoe/yourpackage.git fix-fluffy-bunny
        git pull https://github.com/janedoe/yourpackage.git master
  
  * Satisfy yourself that all is well and you want to merge.
  * Checkout `master`:
  
        git checkout master
  
  * Merge the local PR branch into master with `--no-ff`, meaning "no fast forward merge". This ensures you get a true merge commit, with two parents.
  
        # Template of the Git command
        git merge --no-ff LOCAL_PR_BRANCH
        # How it looks under both naming scenarios
        git merge --no-ff fix-fluffy-bunny
        git merge --no-ff janedoe-master
  
  * Push `master` to GitHub.
  
        git push origin master
  
What's not to like? The parent commit of the local PR branch will almost certainly not be the parent commit of the fork PR branch, where the external contributor did their work. This often means you get merge conflicts in `git pull`, which you'll have to deal with ASAP. The older the PR, the more likely this is and the hairier the conflicts will be.

I would prefer to deal with the merge conflicts only *after* I've vetted the PR and to resolve the conflicts locally, not on GitHub. So I don't use this exact workflow.

## Official GitHub advice, Version 2

GitHub has another set of instructions: [Checking out pull requests locally](https://help.github.com/articles/checking-out-pull-requests-locally/)

It starts out by referring to the Version 1 instructions, but goes on to address an inactive pull request", defined as a PR "whose owner has either stopped responding, or, more likely, has deleted their fork".

This workflow may NOT give the original PR author credit (next time it's easy to test this, I'll update with a definitive answer). I've never used it verbatim because I've never had this exact problem re: deleted fork.

## Official GitHub advice, Version 3

GitHub has yet another set of instructions: [Committing changes to a pull request branch created from a fork](https://help.github.com/articles/committing-changes-to-a-pull-request-branch-created-from-a-fork/)

The page linked above explains all the pre-conditions, but the short version is that a maintainer can probably push new commits to a PR, effectively pushing commits to a fork. Strange, but true!

This set of instructions suggests that you clone the fork, checkout the branch from which the PR was made, make any commits you wish, and then push. Any new commits you make will appear in the PR. And then you could merge.

My main takeaway: maintainer can push to the branch of a fork associated with a PR.

## A workflow I once used

*The lessons learned here eventually lead to the `pr_*()` family of functions in usethis.
`pr_fetch()` and `pr_push()` are now my workhorses for exploring and extending PRs.
You can read more about usethis's functions to help with pull requests in their very own article: [Pull request helpers](https://usethis.r-lib.org/articles/pr-functions.html).*

This combines ideas from the three above approaches, but with a few tweaks. I am sketching this up in R code, with the hope of putting this into a function and package at some point. This is a revision of an earlier approach, based on feedback from Jim Hester.

Example of a PR from the `master` branch (suboptimal but often happens) from fictional GitHub user `abcde` on usethis.


``` r
library(git2r)

## add the pull requester's fork as a named remote
remote_add(name = "abcde", url = "git@github.com:abcde/usethis.git")

## fetch
fetch(name = "abcde")

## list remote branches and isolate the one I want
b <- branches(flags = "remote")
b <- b[["abcde/master"]]

## get the SHA of HEAD on this branch
sha <- branch_target(b)

## create local branch
branch_create(commit = lookup(sha = sha), name = "abcde-master")

## check it out
checkout(object = ".", branch = "abcde-master")

## set upstream tracking branch
branch_set_upstream(repository_head(), name = "abcde/master")

## confirm upstream tracking branch
branch_get_upstream(repository_head())

## make one or more commits here

## push to the branch in the fork and, therefore, into the PR
push()
```


<!--chapter:end:workflows-explore-extend-pull-request.Rmd-->

# Make a GitHub repo browsable {#workflows-browsability}

**The unreasonable effectiveness of GitHub browsability**. One of my favorite aspects of GitHub is the ability to inspect a repository's files in a browser. Certain practices make browsing more rewarding and can postpone the day when you must create a proper website for a project. Perhaps indefinitely.

## Be savvy about your files

Keep files in the plainest, web-friendliest form that is compatible with your main goals. Plain text is the very best. GitHub offers special handling for certain types of files:

  * Markdown files, which may be destined for conversion into, e.g., HTML
  * Markdown files named `README.md`
  * HTML files, often the result of compiling Markdown files
  * Source code, such as `.R` files
  * Delimited files, such as CSVs and TSVs
  * PNG files
  
## Get over your hang ups re: committing derived products
  
Let's acknowledge the discomfort some people feel about putting derived products under version control. Specifically, if you've got an R Markdown document `foo.Rmd`, it can be `knit()` to produce the intermediate product `foo.md`, which can be converted to the ultimate output `foo.html`. Which of those files are you "allowed" to put under version control? Source-is-real hardliners will say only `foo.Rmd` but pragmatists know this can be a serious bummer in real life. Just because I *can* rebuild everything from scratch, it doesn't mean I *want* to.

The taboo of keeping derived products under version control originates from compilation of binary executables from source. Software built on a Mac would not work on Windows and so it made sense to keep these binaries out of the holy source code repository. Also, you could assume the people with access to the repository have the full development stack and relish opportunities to use it. None of these arguments really apply to the `foo.Rmd --> foo.md --> foo.html` workflow. We don't have to blindly follow traditions from the compilation domain!

In fact, looking at the diffs for `foo.md` or `foo-figure-01.png` can be extremely informative. This is also true in larger data analytic projects after a `make clean; make all` operation. By looking at the diffs in the downstream products, you often catch unexpected changes. This can tip you off to changes in the underlying data and/or the behavior of packages you depend on.

This chapter explores cool things GitHub can do with various file types, if they happen to end up in your repo. I won't ask you how they got there.
  
## Markdown

You will quickly discover that GitHub renders Markdown files very nicely. By clicking on `foo.md`, you'll get a decent preview of `foo.html`. Yay! You should read [GitHub's own guide](https://guides.github.com/features/mastering-markdown/) on how to leverage automatic Markdown rendering.

Exploit this aggressively. Make Markdown your default format for narrative text files and use them liberally to embed notes to yourself and others in a repository hosted on Github. It's an easy way to get pseudo-webpages inside a project "for free". You may never even compile these files to HTML explicitly; in many cases, the HTML preview offered by GitHub is all you ever need.

## R Markdown

What does this mean for R Markdown files? **Keep intermediate Markdown. Or only render to Markdown.** Commit both `foo.Rmd` and `foo.md`, even if you choose to `.gitignore` the final product, e.g. `foo.html` or `foo.pdf` or `foo.docx`. From [September 2014](https://github.com/github/markup/pull/343), GitHub renders R Markdown files nicely, like Markdown, and with proper syntax highlighting, which is great. But, of course, the code blocks just sit there un-executed, so my advice about keeping Markdown still holds.

If your target output format is not Markdown, you want [YAML frontmatter](https://gist.github.com/jennybc/402761e30b9be8023af9) that looks something like this for `.Rmd`:




``` yaml
---
title: "Something fascinating"
author: "Jenny Bryan"
date: "`r format(Sys.Date())`"
output:
  html_document:
    keep_md: TRUE
---
```

or like this for `.R`:

``` yaml
#' ---
#' title: "Something fascinating"
#' author: "Jenny Bryan"
#' date: "`r format(Sys.Date())`"
#' output:
#'   html_document:
#'     keep_md: TRUE
#' ---
```

The `keep_md: TRUE` part says to keep the intermediate Markdown. In RStudio, when editing `.Rmd`, click on the gear next to "Knit HTML" for YAML authoring help.

Since 2016, `rmarkdown` offers a [custom output format for GitHub-flavored markdown, `github_document`](http://rmarkdown.rstudio.com/github_document_format.html). Read about [R Markdown workflows](#rmd-test-drive) for explicit examples of how to use this. If Markdown is your target output format, your [YAML can be even simpler](https://gist.github.com/jennybc/402761e30b9be8023af9) and look like this for `.Rmd`:




``` yaml
---
output: github_document
---
```

or like this for `.R`:

``` yaml
#' ---
#' output: github_document
#' ---
```

For a quick, stand-alone document that doesn't fit neatly into a repository or project (yet), make it a [Gist](https://gist.github.com). Example: Hadley Wickham's [advice on what you need to do to become a data scientist](https://gist.github.com/hadley/820f09ded347c62c2864). Gists can contain multiple files, so you can still provide the R script or R Markdown source __and__ the resulting Markdown, as I've done in this write-up of [Twitter-sourced tips for cross-tabulation](https://gist.github.com/jennybc/04b71bfaaf0f88d9d2eb). I've collected [YAML examples](https://gist.github.com/jennybc/402761e30b9be8023af9) for all the above scenarios in a gist.

## `README.md`

You probably already know that GitHub renders `README.md` at the top-level of your repo as the *de facto* landing page. This is analogous to what happens when you point a web browser at a directory instead of a specific web page: if there is a file named `index.html`, that's what the server will show you by default. On GitHub, files named `README.md` play exactly this role for directories in your repo. 

Implication: for any logical group of files or mini project-within-your-project, create a sub-directory in your repository. And then create a `README.md` file to annotate these files, collect relevant links, etc. Now when you navigate to the sub-directory on GitHub the nicely rendered `README.md` will simply appear. The GitHub repo that backs the [gapminder](https://cran.r-project.org/package=gapminder) data package has a [README in the `data-raw` subdirectory](https://github.com/jennybc/gapminder/tree/master/data-raw#readme) that explains exactly how the package data is created. In fact, it is generated programmatically from [`README.Rmd`](https://github.com/jennybc/gapminder/blob/master/data-raw/README.Rmd).

Some repositories consist solely of `README.md`. Examples: Jeff Leek's write-ups on [How to share data with a statistician](https://github.com/jtleek/datasharing) or [Developing R packages](https://github.com/jtleek/rpackages). I am becoming a bigger fan of `README`-only repos than gists because repo issues trigger notifications, whereas comments on gists do not.

If you've got a directory full of web-friendly figures, such as PNGs, you can use [code like this](https://gist.github.com/jennybc/0239f65633e09df7e5f4) to generate a `README.md` for a quick DIY gallery, as Karl Broman has done with [his FruitSnacks](https://github.com/kbroman/FruitSnacks/blob/master/PhotoGallery.md). I did same for all the [fantastic O RLY book covers](https://github.com/jennybc/orly-full-res#readme) made by The Practical Dev.

I have also used this device to share Keynote slides on GitHub (*mea culpa!*). Export them as PNGs images and throw 'em into a README gallery: slides on [file organization](https://github.com/Reproducible-Science-Curriculum/rr-organization1/tree/27883c8fc4cdd4dcc6a8232f1fe5c726e96708a0/slides/organization-slides) and some on [file naming](https://github.com/Reproducible-Science-Curriculum/rr-organization1/tree/27883c8fc4cdd4dcc6a8232f1fe5c726e96708a0/slides/naming-slides).

## Finding stuff

OK these are pure GitHub tips but if you've made it this far, you're obviously a keener.

  * Press `t` to activate [the file finder](https://github.com/blog/793-introducing-the-file-finder) whenever you're in a repo's file and directory view. AWESOME, especially when there are files tucked into lots of subdirectories.
  * Press `y` to [get a permanent link](https://help.github.com/articles/getting-permanent-links-to-files/) when you're viewing a specific file. Watch what changes in the URL. This is important if you are about to *link* to a file or [to specific lines](http://stackoverflow.com/questions/23821235/how-to-link-to-specific-line-number-on-github). Otherwise your links will break easily in the future. If the file is deleted or renamed or if lines get inserted or deleted, your links will no longer point to what you intended. Use `y` to get links that include a specific commit in the URL.

## HTML

If you have an HTML file in a GitHub repository, simply visiting the file shows the raw HTML. Here's a nice ugly example:

  * <https://github.com/STAT545-UBC/STAT545-UBC.github.io/blob/master/bit003_api-key-env-var.html>

No one wants to look at that. ~~You can provide this URL to [rawgit.com](http://rawgit.com) to serve this HTML more properly and get a decent preview.~~

~~You can form two different types of URLs with [rawgit.com](http://rawgit.com):~~

  * ~~For sharing low-traffic, temporary examples or demos with small numbers of people, do this:~~
    - ~~<https://rawgit.com/STAT545-UBC/STAT545-UBC.github.io/master/bit003_api-key-env-var.html>~~
    - ~~Basically: replace `https://github.com/` with `https://rawgit.com/`~~
  * ~~For use on production websites with any amount of traffic, do this:~~
    - ~~<https://cdn.rawgit.com/STAT545-UBC/STAT545-UBC.github.io/master/bit003_api-key-env-var.html>~~
    - ~~Basically: replace `https://github.com/` with `https://cdn.rawgit.com/`~~

*2018-10-09 update: RawGit [announced](https://rawgit.com/) that it is in a sunset phase and will soon shut down. They recommended: [jsDelivr](https://www.jsdelivr.com/rawgit), [GitHub Pages](https://pages.github.com/), [CodeSandbox](https://codesandbox.io/), and [unpkg](https://unpkg.com/#/) as alternatives.*
    
This sort of enhanced link might be one of the useful things to put in a `README.md` or other Markdown file in the repo.

You may also want to check out this [Chrome extension](https://chrome.google.com/webstore/detail/github-html-preview/cphnnfjainnhgejcpgboeeakfkgbkfek?hl=en) or [GitHub & BitBucket HTML Preview](https://htmlpreview.github.io), though recently I've more success with [rawgit.com](http://rawgit.com). (Neither work with private GitHub repos, which is all the more reason
to keep intermediate markdown files for HTML, as described above.)

Sometimes including HTML files will cause GitHub to think that your R repository is HTML. Besides being slightly annoying, this can make it difficult for people to find your work if they are searching specifically for R repos.  You can exclude these files or directories from GitHub's language statistics by [adding a .gitattributes file](https://github.com/github/linguist#using-gitattributes) that marks them as 'documentation' rather than code. [See an example here](https://github.com/jennybc/googlesheets/blob/master/.gitattributes).

## Source code

You will notice that GitHub does automatic syntax highlighting for source code. For example, notice the coloring of this [R script](https://github.com/jennybc/ggplot2-tutorial/blob/master/gapminder-ggplot2-stripplot.r). The file's extension is the primary determinant for if/how syntax highlighting will be applied. You can see information on recognized languages, the default extensions and more at [github/linguist](https://github.com/github/linguist/blob/master/lib/linguist/languages.yml). You should be doing it anyway, but let this be another reason to follow convention in your use of file extensions.

Note you can click on "Raw" in this context as well, to get just the plain text and nothing but the plain text.
    
## Delimited files

GitHub will nicely render tabular data in the form of `.csv` (comma-separated) and `.tsv` (tab-separated) files. You can read more in the [blog post](https://github.com/blog/1601-see-your-csvs) announcing this feature in August 2013 or in [this GitHub help page](https://help.github.com/articles/rendering-csv-and-tsv-data).

Advice: take advantage of this! If something in your repo can be naturally stored as delimited data, by all means, do so. Make the comma or tab your default delimiter and use the file suffixes GitHub is expecting. I have noticed that GitHub is more easily confused than R about things like quoting, so always inspect the GitHub-rendered `.csv` or `.tsv` file in the browser. You may need to do light cleaning to get the automagic rendering to work properly. Think of it as yet another way to learn about imperfections in your data.

Here's an example of a tab delimited file on GitHub: [lotr_clean.tsv](https://github.com/jennybc/lotr/blob/master/lotr_clean.tsv), originally found ~~here~~ (nope, IBM shut down manyeyes July 2015).

Note you can click on "Raw" in this context as well, to get just the plain text and nothing but the plain text.

## PNGs

PNG is the "no brainer" format in which to store figures for the web. But many of us like a vector-based format, such as PDF, for general purpose figures. Bottom line: PNGs will drive you less crazy than PDFs on GitHub. To reduce the aggravation around viewing figures in the browser, make sure to have a PNG version in the repo.

Examples:

  * [This PNG figure](https://github.com/jennybc/STAT545A/blob/master/hw06_scaffolds/01_justR/stripplot_wordsByRace_The_Fellowship_Of_The_Ring.png) just shows up in the browser
  * A different figure [stored as PDF](https://github.com/jennybc/ggplot2-tutorial/blob/master/gapminder-country-colors.pdf) ~~produces the dreaded, annoying "View Raw" speed bump. You'll have to click through and, on my OS + browser, wait for the PDF to appear in an external PDF viewer.~~ *2015-06-19 update: since I first wrote this GitHub has [elevated its treament of PDFs](https://github.com/blog/1974-pdf-viewing) so YAY. It's slow but it works.*
  
Hopefully we are moving towards a world where you can have "web friendly" and "vector" at the same time, without undue headaches. As of [October 2014](https://github.com/blog/1902-svg-viewing-diffing), GitHub provides enhanced viewing and diffing of SVGs. So don't read this advice as discouraging SVGs. Make them! But consider keeping a PNG around as emergency back up for now.
  
## Other document formats

You may also have a document you want others to be able to browse and interact with, but it is not in the markdown format. Fortunately, the open-source Pandoc program, written by John MacFarlane, allows you to convert a range of formats into markdown, including the widely used `.docx` format.

When you click the Knit button in RStudio it is actually Pandoc which performs the final conversion to HTML or Microsoft Word (`.docx`) formats. If you are willing to use the command-line, you can perform the opposite conversion (eg `.docx` to `.md`), commonly retaining features such as headings, tables, equations and even figures.

As some boilerplate, running in Windows PowerShell `pandoc --extract-media .\media  -f docx .\example.docx -t markdown_github -o example_image.md` converts a word document called `example.docx` to markdown, and extracts the images into a directory which corresponds to a filepath in the newly created `example.md` document. A full list of supported formats and example code for conversions are available at https://pandoc.org/.

You can also perform simple conversions to GitHub-flavored markdown from different markdown flavours (Pandoc supports `markdown_mmd`, `markdown_php_extra` and `markdown_strict`) from within RStudio. To do so you need to rename the file by changing the extension (eg from `foo.md` to `foo.Rmd`), then open the renamed file in RStudio and add the following text to the top of the document.

``` yaml
---
output: github_document
---
```

You can then click on "Knit" then "Knit to github document" to perform the conversion. See  [Output format](## Output format) for more details of controlling output formats with the YAML frontmatter.

## Linking to a ZIP archive of your repo

The browsability of GitHub makes your work accessible to people who care about your content but who don't (yet) use Git themselves. What if such a person wants all the files? Yes, there is a clickable "Download ZIP" button offered by GitHub. But what if you want a link to include in an email or other document? If you add `/archive/master.zip` *to the end* of the URL for your repo, you construct a link that will download a ZIP archive of your repository. Click here to try this out on a very small repo:

<https://github.com/jennybc/lotr/archive/master.zip>

Go look in your downloads folder!

## Links and embedded figures

* To link to another page in your repo, just use a relative link: `[admin](courseAdmin/)` will link to the `courseAdmin/` directory inside the current directory. `[admin](/courseAdmin/)` will link to the top-level `courseAdmin/` directory from any where in the repo

* The same idea also works for images. `![](image.png)` will include `image.png` located in the current directory

## Let people correct you on the internet

They love that!

You can create a link that takes people directly to an editing interface in the browser. Behind the scenes, assuming the click-er is signed into GitHub but is not you, this will create a fork in their account and send you a pull request. When I click the link below, I am able to actually commit directly to `master` for this repo.

[CLICK HERE to suggest an edit to this page!](https://github.com/jennybc/happy-git-with-r/edit/master/workflows-make-github-repo-browsable.Rmd)

Here's what that link looks like in the Markdown source:

```
[CLICK HERE to suggest an edit to this page!](https://github.com/jennybc/happy-git-with-r/edit/master/workflows-make-github-repo-browsable.Rmd)
```

and here it is with placeholders:

```
[INVITATION TO EDIT](<URL to your repo>/edit/master/<path to target source file>)
```

AFAIK, to do that in a slick automatic way across an entire repo/site, you need to be using Jekyll or some other automated system. But you could easily handcode such links on a small scale.

<!--chapter:end:workflows-make-github-repo-browsable.Rmd-->

# (PART) Activity prompts {-} 

# Clone a repo {#clone}

Clone someone else's repository on GitHub where you just want a copy. But you also want to track its evolution. That is what differentiates a GitHub clone from, say, simply downloading the ZIP archive at a specific point in time.

Pick a GitHub repository that interests you. Inspiration:

  * an R package you care about
  * a data analytic project you find interesting
    - Example: The GitHub repo that underpins [Polygraphing's blog post](http://polygraph.cool/films/) analyzing 2,000 screenplays is here: <https://github.com/brandles/scripts>
    - Example: FiveThirtyEight shared the data and code behind their [Gun Deaths in America](http://fivethirtyeight.com/gun-deaths/) project on GitHub: <https://github.com/fivethirtyeight/guns-data>. Have a look around their other repos as well.
    
Create a new RStudio Project from this GitHub repo. Refresh your memory of how to do that by re-visiting our "GitHub first" workflow in chapter \@ref(new-github-first).
    
Once you have the code locally, try to run some of it. Try to understand how it works.

Do you want to make a change? Fine do that!

Do you want to send changes back to the original author? Now you have firsthand knowledge of when you should *fork instead of clone*. See chapter \@ref(fork-and-clone).

<!--chapter:end:prompt-clone.Rmd-->

# Create a bingo card {#bingo}

Here's a specific suggestion for practicing "fork and pull".

The general workflow is laid out in chapter \@ref(fork-and-clone).

Jenny and Dean have a repository that makes bingo cards with R:

  * <https://github.com/jennybc/bingo>
  * Read the README to learn more about it!
  
Your mission:

  * Maybe find a partner? Or a couple of partners?
  * Fork the `bingo` repo.
  * Clone it to someone's local machine.
  * Create a new bingo card by making a file of possible squares.
    - Follow the instructions in <https://github.com/jennybc/bingo/blob/master/CONTRIBUTING.md> to see how to contribute a new card.
    - Protip: It's easy to be very funny, but create a very difficult bingo card. Remember to include some easy stuff so people have a chance to bingo.
  * If you're feeling virtuous, run the tests and check the package. Ask us for help! Or live dangerously and skip this.
  * Commit!
  * Push your changes back to your copy of the repo on GitHub.
  * Make a pull request back to the main `bingo` repo.
  * If your card is appropriate, we'll merge your request and it will become part of the package and available via the [Shiny app](http://daattali.com/shiny/bingo/).
  
**Special inspiration for useR**:

  * Make useR-specific conference bingo.
  * See this issue thread for lots of square ideas!
    - <https://github.com/jennybc/bingo/issues/4>

  

<!--chapter:end:prompt-fork-pr-bingo.Rmd-->

# Burn it all down {#burn}

This is a highly inelegant, but effective technique for disaster recovery.

It has been immortalized in an xkcd comic, so it must be ok:

  * <https://xkcd.com/1597/>
  * <http://explainxkcd.com/wiki/index.php/1597:_Git>

Basic idea:

  * Commit early and often.
  * Push to a remote, like GitHub, often.
  * The state of things on GitHub is your new "worst case scenario".
  * If you really screw things up locally, copy all the files (or the ones that have changed) to a safe place.
    - Usually your files are JUST FINE. But it is easy to goof up the Git infrastructure when you're new at this. And it can be hard to get that straightened out on your own.
  * Rename the existing local repo as a temporary measure, i.e. before you do something radical, like delete it.
  * Clone the repo from GitHub to your local machine. You are back to a happy state.
  * Copy all relevant files back over from your safe space. The ones whose updated state you need to commit.
  * Stage and commit. Push.
  * Carry on with your life.

Practice this before you need it, so you see how it works.


<!--chapter:end:prompt-burn-it-all-down.Rmd-->

# Resetting {#reset}

Practice recovering from mistakes.

Use a repository you've created earlier in the tutorial for this. It only needs to be local, i.e. this does not involve GitHub.

If it's not your most recent commit, seriously consider just letting that go. Just. Let. It. Go.

So you want to undo the last commit?

If "YES UNDO IT COMPLETELY": `git reset --hard HEAD^`. You will lose any changes that were not reflected in the commit-before-last!

If "YES undo the commit, but leave the files in that state (but unstaged)": `git reset HEAD^`. Your files will stay the same but the commit will be undone and nothing will be staged.

If "YES go right back to the moment before I committed": `git reset --soft HEAD^`. Your files will stay the same but the commit will be undone. Even your staged changes will be restored.

**If you just want to fiddle with the most recent commit or its message, you can amend it. You can do this from RStudio!**

  * Make the change you want and amend the commit.
  * Do you only want to change the commit message?
    - Make another small change. Surely you have a typo somewhere? Amend the commit, which gives you the chance to edit the message

To amend from the command line, using an editor to create the message:

``` bash
git commit --amend
```

To amend from the command line, providing the new message:

``` bash
git commit --amend -m "New commit message"
```

Git Reset Demystified:

<https://git-scm.com/book/en/v2/Git-Tools-Reset-Demystified>

<!--chapter:end:prompt-practice-resets.Rmd-->

# Search GitHub {#search}

## Basic resources

GitHub searching

  * <https://github.com/search/advanced>
  * <https://help.github.com/articles/searching-code/>
  * <https://help.github.com/articles/search-syntax/>
  
Read-only mirror of R source by Winston Chang:
 
  * <https://github.com/wch/r-source>

Read-only mirror of all packages on CRAN by Gábor Csárdi:

  * <https://github.com/cran>
  * <http://cran.github.io>
  * [METACRAN](http://www.r-pkg.org)

## Use case

What if a function in a package has no examples? Or is poorly exampled? Wouldn't it be nice to find functioning instances of it "in the wild"?

[Via Twitter](https://twitter.com/noamross/status/563422536633839617), Noam Ross taught me a clever way to do such searches on GitHub. Put this into the GitHub search box to see how packages on CRAN use the `llply()` function from `plyr`:

``` bash
"llply" user:cran language:R
```

Or just [click here](https://github.com/search?l=r&q=%22llply%22+user%3Acran+language%3AR&ref=searchresults&type=Code).

Another example that recently came up on r-package-devel:

How to see lots of examples of roxygen templates?

This search finds >1400 examples of roxygen templates in the wild:

<https://github.com/search?q=man-roxygen+in%3Apath&type=Code&ref=searchresults>

<!--chapter:end:prompt-search-github.Rmd-->

# (PART) Notes {-} 

# Notes {#notes-intro .unnumbered}

This part holds content that is deprecated/stale, does not exist yet, or relates to bookdown mechanics.

<!--chapter:end:notes-intro.Rmd-->

# Run a course with GitHub {#classroom-overview}

*This content is rather stale and unlikely to see further development.*

GitHub makes a wonderful platform on which to run a course. I've been doing this on [github.com](https://github.com) since 2014 in [STAT 545](http://stat545.com), an 80-student grad course in data analysis with R, and in a second large, code-intensive graduate course in statistical genomics. We're running all of the courses for UBC's [Master of Data Science program](https://ubc-mds.github.io) off a private instance of [GitHub Enterprise](https://enterprise.github.com/home) hosted in Canada.

## Benefits

For the instructor

  * If you already use Git/GitHub, it's extremely efficient to use the same workflows to manage course materials, student work, and communication with students and TAs.
    - When I switched to Git/GitHub and R Markdown, abandoning my old "system" of accepting all manner of stuff as email attachments? It was the first time I actually ran the code in my students' final projects, because it was so easy to get it on my computer in an organized fashion. I even made some corrections as pull requests!
  * If you're still in your early days with Git/GitHub, the sheer volume of operations and regular small deadlines will increase your mastery very quickly. Practice makes perfect! However, I would not recommend running a course on GitHub as your *first* substantial version control project.

For the students

  * I have found that students adjust to Git/GitHub fairly quickly and genuinely like it. They find it gratifying to see their beautiful, figure-rich R Markdown reports up on the internet. Since it's easy to expose their work within the class, we do a lot of peer review. I find that expertise spreads around the class like a virus. That applies to the main course substance as well as workflow.
  * Many students are specifically interested in learning Git and GitHub, as a complement to the coding and analytical skills we teach in these courses. The fact that we use it for course mechanics kills two birds with one stone. Teaching the use of distributed version control is a valid pedagogical goal in and of itself.

## The STAT 545 student setup

GitHub's Organizations/Teams and API have changed over the 3+ years we've been doing this, so my approach has evolved over time and is also shaped by hard experience.

Major points:

  * [Create an Organization](https://help.github.com/articles/creating-a-new-organization-account/) for the course.
    - Immediately request an [Education discount](https://education.github.com) for the Organization, so that you get unlimited private repos.
  * Have your students register for free, personal [GitHub accounts](https://github.com).
    - Encourage them to request an [Education discount](https://education.github.com) on their own behalf (aka "student developer pack"). But rest assured, nothing you need for your course machinery will depend on this.
  * Get the GitHub usernames from your students -- we use a [Shiny](http://deanattali.com/blog/shiny-persistent-data-storage/) [app](http://deanattali.com/2015/06/14/mimicking-google-form-shiny/)! -- plus some shred of information that allows you link them back to your official course list.
  * Create a students [Team](https://help.github.com/enterprise/2.7/admin/guides/user-management/organizations-and-teams/) and a TA Team. I make such teams for each run of the course, e.g. `2016_students` and `2016_ta`.
  * Invite students to join your course organization and the students team. Ditto for TAs and the TA team.
  * Create a canonical name for each student, based on the official course list, i.e. `lastname_firstname`.
  * Create a repository for each student, using the student's canonical name.
    - This is a private repository within the course Organization.
    - I turn wikis off and either let GitHub auto-initialize or immediately push files, including a README, into the repos.
    - Give the student team read or pull access to each student's repo. Yes, this allows them to see each others work. I discuss this elsewhere.
    - Give the TA team write or push access to each student's repo.
    - Add the student as collaborator with write or push access.
    - Unwatch these repos personally! Wow such notification.

That's the setup! I use the [gh](https://github.com/gaborcsardi/gh) and [purrr](https://github.com/hadley/purrr) packages to script all of this [GitHub API](https://developer.github.com/v3/) work. *In a second wave, I'll post code snippets for the above operations.*
    
What you should NOT do (voice of experience, here):

Do NOT allow students to create their own repositories.

  - You will have a naming convention and they will never, ever, ever follow it.
  - You need to have admin rights over their course repo, so you can manipulate it at will via the GitHub API. You will ask them to add you and the TAs as collaborators, but they will not all manage to execute this task.
  - You will want to do various bulk operations on the repos and your API work will be simpler if the repos belong to the same Organization vs looping over randomly named repos owned by random people, subject to their whims.
  
## The homework-flow

In class, the students [take possession of their repos](http://stat545.com/git08_claim-stat545-repo.html), from RStudio via *File > New Project*. They do the bulk of their coursework here: it is a directory on their computer, a Git repo associated with GitHub remote, and an RStudio project.

Typically homework is done in R Markdown, using the [`github_document`](http://rmarkdown.rstudio.com/github_document_format.html) output format. They commit and push `.Rmd`, `.md`, and any necessary files, such a figures.

Homework is submitted by opening an issue:

  * Issue name is "Mark homework x of lastname_firstname". OK not really, but I can dream.
  * Body should contain SHA of their latest commit, tag(s) for the marking TA or the TA team, and, ideally, links to the file(s) to be marked.
  
TAs leave feedback here. Actual marks are stored elsewhere and distributed via email. As the TAs mark, they close the issues.

After homework submission, we randomly assign each student to review the work of two peers. Each peer review assignment takes the form of an issue, assigned to the reviewer. Students leave feedback for each other here. As the TAs mark, they read and assess these peer reviews (also marked!) and close the issues.


## GitHub as course management system

*2017-05-29 This section was excised from an article I am writing. It is partially redundant with the above and the the two will be merged.*

[STAT 545](http://stat545.com) is a data wrangling and analysis course at the University of British Columbia. I was the instructor in charge for several years, which coincided with my own adoption of Git/GitHub. GitHub is used to manage the development of course material, to serve the course website, to create a discussion forum, and to host all student-submitted work. 

Given that students must submit their work and provide peer review of others' work via GitHub, the use of hosted version control is an explicit, though modest, part of the course. The website [Happy Git and GitHub for the useR](http://happygitwithr.com) holds our battle-tested instructions for setup and early usage. The students achieve basic competence quite quickly and find it gratifying to see their formatted, figure-rich R Markdown reports up on the internet. Since it’s easy to expose their work within the class, we conduct peer review, which helps expertise to spread quickly through the group.

### Use a GitHub Organization

[GitHub Organizations](https://help.github.com/articles/differences-between-user-and-organization-accounts/) are "shared accounts where groups of people can collaborate across many projects at once". This is the most appropriate structure for stewarding course resources, since I can grant TAs and students different levels of access to various repositories. Access can be controlled at the individual user level or, more conveniently, for entire [Teams](https://help.github.com/articles/setting-up-teams/). The TA Team shares write access with me on a private repository for internal matters. I provide each student with their own private repository for coursework and grant other members of the Students Team read access, in order to facilitate peer review. There is a public repository that underpins the course website (see below). We have one other public repository that exists solely so the [Issues](https://github.com/STAT545-UBC/Discussion/issues) can be used as a discussion forum.

GitHub actively encourages the use of its platform in teaching. As an instructor you can request a [free Organization account](https://help.github.com/articles/discounted-organization-accounts/) that provides features normally available only on paid plans, such as private repositories. In fact, GitHub provides tooling for specific teaching workflows via [GitHub Classroom](https://classroom.github.com/), although I do not use it. That is not an intentional knock on their tools. I started teaching with GitHub several years before this existed and developed a different way of using the platform. I also find the [GitHub Education](https://education.github.com) resources to be geared more towards computer science than data science.

### GitHub Pages for course website

All course content is provided on the [STAT 545 website](http://stat545.com). Each page is generated from an R Markdown document that is rendered to HTML locally using the rmarkdown package, retaining the intermediate Markdown. These pages are a mix of prose and rendered R code, reflecting the live coding done in class. All of these files and their history can be explored in the [source repository](https://github.com/STAT545-UBC/STAT545-UBC.github.io). The TA team has permission to write to this repo, meaning they can (and do!) help me maintain the website. I rejoice that I am no longer the webmaster. We also get typo corrections and other input from the world at large, since this is entirely public.

If I were starting from scratch today, I would continue to use R Markdown, RStudio, and GitHub Pages (see below), but would upgrade to a more modern, automated approach to rendering the pages. I now recommend [R Markdown websites](http://rmarkdown.rstudio.com/rmarkdown_websites.html), [bookdown](https://bookdown.org), or [blogdown](https://bookdown.org/yihui/blogdown/) to manage the process of creating a static website from a large and inter-related set of `.Rmd` files.

GitHub offers several ways to host a website directly from a repository, collectively known as [GitHub Pages](https://help.github.com/categories/github-pages-basics/). The STAT 545 website is a very simple [Organization Page](https://help.github.com/articles/user-organization-and-project-pages/) that uses a [custom domain](https://help.github.com/articles/custom-domain-redirects-for-github-pages-sites/), `stat545.com`, instead of the default `orgname.github.io`.

This system for managing course content is a great example of integrating the doing of work and the sharing of it. We analyze data live in class, using R, based on the scripts on the website. I re-render the associated `.R` or `.Rmd`, commit the changed files, push, and see it reflected right away on http://stat545.com. There is no separation between having an idea, implementing it, and posting on the website.

### Student-specific private repos

Early in the course I elicit GitHub usernames for registered students, via a [Shiny app](https://shiny.rstudio.com), and invite them to join the course Organization. I then create one private repository per student, in the STAT 545 Organization. The targeted student has write access and the other students have read access. This is somewhat controversial, due to the possibility of cheating, but I have seen more pros than cons for this setup, in the STAT 545 context. In other settings, I have also used one repo per student *per homework assignment*, which allows you to keep the repos completely private until homework submission, then increase their visibility during marking and peer review. Some courses will work better with one model or the other.

Each student does their work in this repo, submitting a major assignment approximately once a week. The first assignment is simply to claim the repository and create a README, which proves they have all the relevant software setup and they can write a little Markdown. Each week we tackle some new data analysis or wrangling task, with increasing latitude for independence. Homework is implemented in R Markdown documents, rendered to Markdown, and pushed to GitHub. Students submit their work by opening an issue in their repo, naming the assignment in the title, providing the SHA of the associated final commit, and linking to the main `.md` file. We leave feedback as comments in the issue thread or, occasionally, propose changes to code via "pull requests". Two peers are selected at random to review each assignment, a process that we also implement via GitHub Issues.

At the end of term, the student (and their instructor!) can visit the repo to find an organized, navigable sequence of ~10 assignments. Each student leaves with self-written documentation of everything they've done, ready to consult in future projects. The last assignments require writing an R package or Shiny app, which they generally do in public repositories under their own accounts. They finish STAT 545 with several months of Git/GitHub experience and the start of a data science portfolio.




    
    
    
    
    

<!--chapter:end:notes-classroom-overview.Rmd-->

# Ideas for content

## Common workflow questions

### Common predicaments and how to recover/avoid

https://twitter.com/JennyBryan/status/743457387730735104

### Keep something out of Git

List it in `.gitignore.`

### I didn't mean to commit that

Committing things you didn't mean to (too big, secret). How to undo.

## git stuff

Git explainers, heavy on the diagrams

https://twitter.com/JennyBryan/status/743548245645791232

A Visual Git Reference  
http://marklodato.github.io/visual-git-guide/index-en.html

A successful Git branching model  
http://nvie.com/posts/a-successful-git-branching-model/

A successful Git branching model considered harmful  
https://barro.github.io/2016/02/a-succesful-git-branching-model-considered-harmful/

Git Tutorials from Atlassian
https://www.atlassian.com/git/tutorials/

Software Carpentry Git Novice Lesson  
http://swcarpentry.github.io/git-novice/

Michael Freeman slides on Git collaboration  
http://slides.com/michaelfreeman/git-collaboration#/

GitHub Training materials  
https://services.github.com/kit/

Git for Ages 4 and Up  
<https://www.youtube.com/watch?v=3m7BgIvC-uQ>

Learn Git Branching  
http://learngitbranching.js.org

A Git Workflow Walkthrough Series
http://vallandingham.me/git-workflow.html

  * Part 1: Feature Branches
  * Part 2: Reviewing Pull Requests
  * Part 3: Reviewing Pull Requests Locally
  * Part 4: Merging Pull Requests

Git from the inside out  
https://codewords.recurse.com/issues/two/git-from-the-inside-out

## Disaster recovery

<http://stackoverflow.com/questions?sort=votes>

Break it down:

  * Is something wrong with my filesystem/files?
  * Is my git repo messed up?
  * How can I keep this from happening again?
  
Rebase avoidance techniques.

Headless state. Rebase hell.

What to do when you can't, e.g., switch branches. Stashing and WIP commits.

## Engage with R source on GitHub

Browsing

Searching

  * My gist, re: the cran user: <https://gist.github.com/jennybc/4a1bf4e9e1bb3a0a9b56>

Being a useful useR

  * stay informed re: development
  * use issues for bug reports, feature requests
  * make pull requests
  
## Workflow and psychology

Stress of working in the open

Workflows for group of 1, 2, 5, 10

  * Fork and Pull vs Shared Repository
  
    - <https://help.github.com/articles/about-collaborative-development-models/>
    - <https://help.github.com/articles/using-pull-requests/>

<!--chapter:end:notes-ideas.Rmd-->

# Bookdown cheat sheet

Here's where I park _little_ *examples* **for myself** about bookdown mechanics that I keep forgetting.

The bookdown book: <https://bookdown.org/yihui/bookdown/>

## Heading blah blah

## About labelling things {#id-example}

You can label chapter and section titles using `{#label}` after them, e.g., we can reference Section \@ref(id-example). If you do not manually label them, there will be automatic labels anyway, e.g., this reference to the unlabelled heading \@ref(heading-blah-blah) uses the automatically generated label `\@ref(heading-blah-blah)`.

## Cross-references

Add an explicit label by adding `{#label}` to the end of the section header. If you know you're going to refer to something, this is probably a good idea.

To refer to in a chapter- or section-number-y way, use `\@ref(label)`.

  * `\@ref(install-git)` example: In chapter \@ref(install-git) we explain how to install Git.

If you are happy with the section header as the link text, use it inside a single set of square brackets:

  * `[A picture is worth a thousand words]`: example "A picture is worth a thousand words" via [A picture is worth a thousand words]

There are two ways to specify custom link text:

  * `[link text][Section header text]`, e.g., "pic = 1000 words" via [pic = 1000 words][A picture is worth a thousand words]
  * `[link text](#label)`, e.g., "RStudio, meet Git" via [RStudio, meet Git](#rstudio-see-git)
  
The Pandoc documentation provides more details on automatic section IDs and implicit header references.

## Figures, tables, citations

Figures and tables with captions will be placed in `figure` and `table` environments, respectively.


``` r
par(mar = c(4, 4, .1, .1))
plot(pressure, type = 'b', pch = 19)
```

\begin{figure}

{\centering \includegraphics[width=0.8\linewidth]{notes-bookdown-cheat-sheet_files/figure-latex/nice-fig-1} 

}

\caption{Here is a nice figure!}(\#fig:nice-fig)
\end{figure}

Reference a figure by its code chunk label with the `fig:` prefix, e.g., see Figure \@ref(fig:nice-fig). Similarly, you can reference tables generated from `knitr::kable()`, e.g., see Table \@ref(tab:nice-tab).


``` r
knitr::kable(
  head(iris, 20), caption = 'Here is a nice table!',
  booktabs = TRUE
)
```

\begin{table}

\caption{(\#tab:nice-tab)Here is a nice table!}
\centering
\begin{tabular}[t]{rrrrl}
\toprule
Sepal.Length & Sepal.Width & Petal.Length & Petal.Width & Species\\
\midrule
5.1 & 3.5 & 1.4 & 0.2 & setosa\\
4.9 & 3.0 & 1.4 & 0.2 & setosa\\
4.7 & 3.2 & 1.3 & 0.2 & setosa\\
4.6 & 3.1 & 1.5 & 0.2 & setosa\\
5.0 & 3.6 & 1.4 & 0.2 & setosa\\
\addlinespace
5.4 & 3.9 & 1.7 & 0.4 & setosa\\
4.6 & 3.4 & 1.4 & 0.3 & setosa\\
5.0 & 3.4 & 1.5 & 0.2 & setosa\\
4.4 & 2.9 & 1.4 & 0.2 & setosa\\
4.9 & 3.1 & 1.5 & 0.1 & setosa\\
\addlinespace
5.4 & 3.7 & 1.5 & 0.2 & setosa\\
4.8 & 3.4 & 1.6 & 0.2 & setosa\\
4.8 & 3.0 & 1.4 & 0.1 & setosa\\
4.3 & 3.0 & 1.1 & 0.1 & setosa\\
5.8 & 4.0 & 1.2 & 0.2 & setosa\\
\addlinespace
5.7 & 4.4 & 1.5 & 0.4 & setosa\\
5.4 & 3.9 & 1.3 & 0.4 & setosa\\
5.1 & 3.5 & 1.4 & 0.3 & setosa\\
5.7 & 3.8 & 1.7 & 0.3 & setosa\\
5.1 & 3.8 & 1.5 & 0.3 & setosa\\
\bottomrule
\end{tabular}
\end{table}

You can write citations, too. For example, we are using the **bookdown** package [@R-bookdown] in this sample book, which was built on top of R Markdown and **knitr** [@knitr-book].

## How the square bracket links work

Context: you prefer to link with text, not a chapter or section number.

  * GOOD! Here's a link to [Contributors].
  * BAD. You can see contributors in \@ref(contrib).

Facts and vocabulary

  * Each chapter is a file. These files should begin with the chapter title using a level-one header, e.g., `# Chapter Title`.
  * A chapter can be made up of sections, indicated by lower-level headers, e.g., `## A section within the chapter`.
  * There are three ways to address a section when creating links within your book:
    - **Explicit identifier**: In `# My header {#foo}` the explicit identifier is `foo`.
    - **Automatically generated identifier**: `my-header` is the auto-identifier for `# My header`. Pandoc creates auto-identifiers according to rules laid out in [Extension: auto_identifiers](http://pandoc.org/README.html#extension-auto_identifiers).
    - The header text, e.g., `My header` be used verbatim as an **implicit header reference**. See [Extension: implicit_header_references](http://pandoc.org/README.html#extension-implicit_header_references) for more.
  * All 3 forms can be used to create cross-references but you build the links differently.
  * Advantage of explicit identification: You are less likely to update the section header and then forget to make matching edits to references elsewhere in the book.

How to make text-based links using explicit identifiers, automatic identifiers, and implicit references:

  * Use implicit reference alone to get a link where the text is exactly the section header:
    - `[Introduce yourself to Git]` [Introduce yourself to Git]
    - `[Success and operating systems]` [Success and operating systems]
  * You can provide custom text for the link with all 3 methods of addressing a section:
    - Implicit header reference: `[link text][Recommended Git clients]` [link text][Recommended Git clients]    
    - Explicit identifier: `[hello git! I'm Jenny](#hello-git)` [hello git! I'm Jenny](#hello-git)
    - Automatic identifier: `[Any text you want](#recommended-git-clients)` [Any text you want](#recommended-git-clients)

<!--chapter:end:notes-bookdown-cheat-sheet.Rmd-->

# (APPENDIX) Appendix {-}

<!--chapter:end:appendix.Rmd-->

# The shell {#shell}

Even if you do most of your Git operations via a client, such as RStudio or GitKraken, you must sometimes work in the shell. As you get more comfortable with Git, you might prefer to do more and more via the command line. You might also need to use Git or file system operations on a server that lacks your usual Git client. For all these reasons, it is a good idea to learn your way around the shell.

Here's a typical look for a shell. You'll see a simple blinking cursor, waiting for input:

<!-- why can bookdown not find this?!?
![](http://upload.wikimedia.org/wikipedia/commons/thumb/e/e7/Bash_screenshot.png/440px-Bash_screenshot.png)
-->

![](img/440px-Bash_screenshot.png)

## What is the shell?

The shell is a program on your computer whose job is to run other programs. Pseudo-synonyms are "terminal", "command line", and "console". There's a whole StackExchange thread on the differences ([What is the difference between Terminal, Console, Shell, and Command Line?](https://askubuntu.com/questions/506510/what-is-the-difference-between-terminal-console-shell-and-command-line)), but I don't find it to be terribly enlightening. Your mileage may vary.

Many programmers spend lots of time in a shell, as opposed to in GUIs, because it is very fast, concise, and ubiquitous in their relevant computing environments. This is how all work was done before we got the mouse and GUIs.

The most common shell is `bash` and it gets thrown around as a proxy for "shell" sometimes, just like "Coke" and "Kleenex" are proxies for cola and tissues.

In Happy Git, sometimes we demo the use of a shell for certain tasks, like navigating the file system and doing Git operations, when we don't want to or can't use RStudio. Providing shell commands is also less ambiguous and less perishable than describing human interactions with a GUI.

## Starting the shell

### From within RStudio

You can launch a shell from RStudio. This is often handy, because RStudio makes every effort to put you in a sane working directory, i.e. in the current project.

There are two ways:

  * *Tools > Terminal* launches a shell within RStudio, graphically and process-wise. I believe this is usually what you want.
  * *Tools > Shell ...* launches a shell external to RStudio.

### Outside of RStudio

#### macOS

The shell is often called the "terminal" on macOS, by which people mean Terminal.app. One way to launch is via Spotlight Search. Type Command + space and start typing "terminal". This process will something like so:
	
![](img/terminal_mac_search.png)

Terminal.app is typically located at */Applications/Utilities/Terminal.app*.
	
Opening Terminal.app brings you to a bash shell opened to your home directory `~/`, which is shorthand for `/Users/YOURUSERNAME`. You should see something like this:

![](img/terminal_mac.png)

If you have administrative rights on your computer, prefacing any command with `sudo` will allow you to run the command as an administrator. Expect to be challenged for your password. If you need to change administrative privileges or your password, see [this article](https://support.apple.com/en-us/HT204012) from Apple.

#### Windows

We defer this until the next section, due to the more complex shell situation on Windows.

## Windows is special ... and not in a good way {#windows-shell-hell}

Windows is not the ideal platform for scientific computing and software development. A lot of the functionality is going to feel janky and strapped on. Because it is.

There are no fewer than 4 possible shells you can end up in. Unless you know better, you almost certainly want to be in a Git Bash shell, especially here in Happy Git.

Windows users will want to understand the different types of shell, how to launch them, and how to tell which one you're in.

### Git Bash

*TL;DR how to tell if you're in a Git Bash shell? Do this:*

``` bash
$ echo $SHELL
/usr/bin/bash
```

Git Bash is a bash shell that ships with Git for Windows, which is [the Happy Git way to install Git on Windows](#install-git-windows). Therefore, you will not have Git Bash on your system until you install Git for Windows.

Git Bash is always the Windows shell we are targeting in Happy Git instructions.

RStudio should automatically detect the presence of Git Bash. You can inspect and influence this directly via *Tools > Global Options > Terminal*. Unless you have good reason to do otherwise, you want to see "Git Bash" in the "New terminals open with ..." dropdown menu.

![](img/git-bash-as-rstudio-terminal.png)

Troubleshooting tips:

  * Restart RStudio. You need to restart all instances of RStudio after installing Git for Windows (+ Git Bash), in order for RStudio to auto-detect Git Bash.
  * Update RStudio. The shell handling in RStudio has improved dramatically over time, so older versions might not behave as described here.

#### Accessing Git Bash outside of RStudio
	
Sometimes you want to run Git Bash outside of RStudio. Here's the easiest way: click the "Git" menu in the Windows menu and select "Git Bash".
	
![](img/2019-01_git_bash_windows.png)

A Git Bash shell running outside of RStudio looks something like this:

![](img/2018-01-15_git-bash.png)

Notice `MSYS` in the title bar. You might also see `MINGW64`.

Sometimes you need to run Git Bash as administrator, e.g. to run with higher privileges. Easiest way: click the "Git" menu in the Windows menu and *right-click* on "Git Bash". This reveals a submenu. Select "more" and then "Run as administrator".
	
![](img/2019-01-git-windows-administrator.png)

### Command prompt

*TL;DR how to tell if you're in Command Prompt? Do this:*

``` bash
C:\Users\jenny>echo %COMSPEC%
C:\WINDOWS\system32\cmd.exe
```

This is the native Windows command line interpreter. It's rarely what you want, especially for the work described in Happy Git.

A Command Prompt session running outside of RStudio looks something like this:

![](img/2018-01-15_command-prompt.png)

Notice the `cmd.exe` in the title bar, although it is not *always* present. You might also see "Command Prompt".

If you get an error message such as `'pwd' is not recognized as an internal or external command, operable program or batch file.` from a shell command, that suggests you have somehow launched into `cmd.exe` when you did not mean to.

### PowerShell

*TL;DR how to tell if you're in PowerShell? Do this:*

``` bash
PS C:\Users\jenny> Get-ChildItem Env:ComSpec

Name                           Value
----                           -----
ComSpec                        C:\WINDOWS\system32\cmd.exe
```

PowerShell is yet another Windows shell, a more modern successor to Command Prompt.  It's also rarely what you want, especially for the work described in Happy Git.

A PowerShell session running outside of RStudio looks something like this:

![](img/2018-01-15_power-shell.png)

Notice the `powershell.exe` in the title bar.

### Bash via Windows Services for Linux

*TL;DR how to tell if you're in Bash via WSL? Do this:*

``` bash
$ echo $SHELL
/bin/bash
```

In 2016, Microsoft launched the Windows Subsystem for Linux (WSL), "a new Windows 10 feature that enables you to run native Linux command-line tools directly on Windows". Overall, this is a fantastic development. However, at the time of writing (January 2019), you will only have this if you're running Windows 10 64-bit and have chosen to [install the optional WSL system component](https://docs.microsoft.com/en-us/windows/wsl/install-win10). Therefore, I expect only keeners to have this and, in that case, you probably don't need this chapter.

A WSL bash shell running outside of RStudio looks something like this:

![](img/2018-01-15_bash-windows-services-for-linux.png)

FYI Microsoft also refers to WSL as Bash on Ubuntu on Windows.

#### Windows bottom line

When in doubt, you probably want to be in a Git Bash shell.

## Basic shell commands

The most basic commands are listed below:

* [`pwd`](https://en.wikipedia.org/wiki/Pwd) (**p**rint **w**orking **d**irectory). Shows directory or "folder" you are currently operating in. This is not necessarily the same as the `R` working directory you get from `getwd()`.
* [`ls`](https://en.wikipedia.org/wiki/Ls) (**l**i**s**t files). Shows the files in the current working directory. This is equivalent to looking at the files in your Finder/Explorer/File Manager. Use `ls -a` to also list hidden files, such as `.Rhistory` and `.git`.
* [`cd`](https://en.wikipedia.org/wiki/Cd_(command)) (**c**hange **d**irectory). Allows you to navigate through your directories by changing the shell's working directory. You can navigate like so:
  - go to subdirectory `foo` of current working directory: `cd foo`
  - go to parent of current working directory: `cd ..`
  - go to your "home" directory: [`cd ~`](http://tilde.club/~ford/tildepoint.jpg) or simply `cd`
  - go to directory using absolute path, works regardless of your current working directory: `cd /home/my_username/Desktop`. Windows uses a slightly different syntax with the slashes between the folder names reversed, `\`, e.g. `cd C:\Users\MY_USERNAME\Desktop`.
    * Pro tip 1: Dragging and dropping a file or folder into the terminal window will paste the absolute path into the window.
    * Pro tip 2: Use the `tab` key to autocomplete unambiguous directory and file names. Hit `tab` twice to see all ambiguous options.
* Use arrow-up and arrow-down to repeat previous commands. Or search for previous commands with `CTRL` + `r`.
    
A few Git commands:

* `git status` is the most used git command and informs you of your current branch,  any changes or untracked files, and whether you are in sync with your remotes.
* `git remote -v` lists all remotes. Very useful for making sure `git` knows about your remote and that the remote address is correct.
* `git remote add origin GITHUB_URL` adds the remote `GITHUB_URL` with nickname `origin`.
* `git remote set-url origin GITHUB_URL` changes the remote url of `origin` to `GITHUB_URL`. This way you can fix typos in the remote url.
* *Feel free to suggest other commands that deserve listing in a [GitHub issue](https://github.com/jennybc/happy-git-with-r/issues).*

<!--chapter:end:shell.Rmd-->

# Comic relief {#comic-relief}

It's not you, it's Git!

If you're not crying already, these fictional-but-realistic Git man pages should do the trick:

  * [git-man-page-generator](http://git-man-page-generator.lokaltog.net)
  * And, of course, the underlying source is also available on GitHub:
    - <https://github.com/Lokaltog/git-man-page-generator>

If you can tolerate adult and often offensive language, you might enjoy:

  * <http://www.commitlogsfromlastnight.com>
  * <http://ohshitgit.com/>

Your commits will look more glorious scrolling by Star Wars style:

  * <http://starlogs.net>
  * <http://starlogs.net/#jennybc/googlesheets>
  * Do this for any repo: `http://starlogs.net/#USER/REPO`
  

<!--chapter:end:comic-relief.Rmd-->

# Resources {#resources}

We practice what we preach! This site is created with Git and R markdown, using the [`bookdown`](https://github.com/rstudio/bookdown/) package. Go ahead and [peek behind the scenes](https://github.com/jennybc/happy-git-with-r).

Long-term, you should understand more about what you are doing. Rote clicking in RStudio may be a short-term survival method but won't work for long.

  * [Git for Humans](https://speakerdeck.com/alicebartlett/git-for-humans) is a great set of slides by [Alice Bartlett](https://alicebartlett.co.uk), originally delivered in 2016 at UX Brighton.

  * [Git in Practice](https://www.manning.com/books/git-in-practice) by Mike McQuaid is an more approachable book, probably better than Pro Git (below) for most people starting out. Ancillary materials [on GitHub](https://github.com/MikeMcQuaid/GitInPractice).

  * The book [Pro Git](http://git-scm.com/book) is fantastic and comprehensive.

  * [Oh My Git!](https://ohmygit.org/) is a free and open source interactive game for learning Git. It's very beginner friendly, using a graph to visualise the worktree. Lessons can be completed using a playing card interface in addition to the built-in command line, which is there for when users become more comfortable.

  * [GitHub's own training materials](https://training.github.com) may be helpful. They also point to [many other resources](https://help.github.com/articles/what-are-other-good-resources-for-learning-git-and-github)

  * Find a powerful Git client (chapter \@ref(git-client)) if you'd like to minimize your usage of Git from the command line.
  
  * Ten Simple Rules for Taking Advantage of Git and GitHub <http://journals.plos.org/ploscompbiol/article?id=10.1371/journal.pcbi.1004947>

  * RStudio's guide [Version Control with Git and SVN](https://support.rstudio.com/hc/en-us/articles/200532077-Version-Control-with-Git-and-SVN)
  
  * The book *[Team Geek](http://shop.oreilly.com/product/0636920018025.do)* has insightful advice for the human and collaborative aspects of version control.  It proposes Git strategies suited to different characteristics of teams.



<!--chapter:end:references.Rmd-->

