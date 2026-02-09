---
title: "The Guide to Git I Never Had  A Developer s Complete Manual d47a912b52f2"
platform: Medium
original_file: 2024-09-06_The-Guide-to-Git-I-Never-Had--A-Developer-s-Complete-Manual-d47a912b52f2.md
---

# The Guide to Git I Never Had  A Developer s Complete Manual d47a912b52f2

::: {}
# The Guide to Git I Never Had: A Developer's Complete Manual {#the-guide-to-git-i-never-had-a-developers-complete-manual .p-name}
:::

::: {.section .p-summary field="subtitle"}
Git is an essential tool for any developer, yet many of us have stumbled
our way through it, picking up tips and tricks from colleagues or...
:::

::::::::::::::::::::::::::::::::::::::::::::::::::::::::::: {.section .e-content field="body"}
:::::: {#7371 .section .section .section--body .section--first}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### The Guide to Git I Never Had: A Developer's Complete Manual {#1b69 .graf .graf--h3 .graf--leading .graf--title name="1b69"}

<figure id="ca48" class="graf graf--figure graf-after--h3">
<img
src="https://cdn-images-1.medium.com/max/800/0*qWwgT1BG0Pbvr_uj.png"
class="graf-image" data-image-id="0*qWwgT1BG0Pbvr_uj.png"
data-width="1920" data-height="1080" data-is-featured="true" />
</figure>

Git is an essential tool for any developer, yet many of us have stumbled
our way through it, picking up tips and tricks from colleagues or Stack
Overflow, often without a solid understanding of what we were doing.
When I first started using Git, I wished for a comprehensive guide that
could explain not just the how, but the why behind Git's commands and
functionality. After years of using Git on a daily basis, I've compiled
this guide --- the one I wish I'd had when I started.

Whether you're just beginning your journey into version control or
you're a developer who wants to solidify their understanding of Git,
this guide will take you through everything you need to know, from Git
fundamentals to advanced workflows. Let's dive in!

### Table of Contents: {#b51c .graf .graf--h3 .graf-after--p name="b51c"}

1.  [**What is Git?**]{#2363}
2.  [**Installing Git**]{#c383}
3.  [**Understanding Version Control**]{#e7a9}
4.  [**Git Basics**]{#0b1d}

- [Repositories]{#0770}
- [Commits]{#7050}
- [Staging]{#3e08}

1.  [**Branching in Git**]{#9415}
2.  [**Merging and Resolving Conflicts**]{#4345}
3.  [**Git Workflows**]{#092d}
4.  [**Remote Repositories**]{#0dc8}
5.  [**Working with Pull Requests**]{#7867}
6.  [**Advanced Git Commands**]{#1f38}
7.  [**Git Best Practices**]{#5025}
8.  [**Common Mistakes and Troubleshooting**]{#a979}
:::
::::
::::::

:::::: {#9011 .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### 1. What is Git? {#f0a7 .graf .graf--h3 .graf--leading name="f0a7"}

Git is a **distributed version control system** (DVCS) created by Linus
Torvalds in 2005 to handle versioning for Linux Kernel development. Git
allows multiple developers to work on the same project simultaneously,
tracks changes in files, and facilitates collaboration across teams and
time zones. Unlike older version control systems, Git's distributed
nature means that every developer has a complete history of the project,
providing more flexibility and preventing data loss.

### Why Use Git? {#d902 .graf .graf--h3 .graf-after--p name="d902"}

Git is widely adopted because:

- [**Collaboration**: Multiple developers can work on the same project
  without overriding each other's work.]{#4dad}
- [**History Tracking**: Git stores a record of every change, making it
  easy to revert to earlier versions.]{#8cc7}
- [**Branching and Merging**: Developers can work on different features
  or fixes in parallel, then merge them back into the main
  project.]{#ca99}
- [**Open Source**: Git is free and open source, supported by an active
  community.]{#5312}
:::
::::
::::::

:::::: {#d731 .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### 2. Installing Git {#1968 .graf .graf--h3 .graf--leading name="1968"}

Before diving in, you need to install Git on your machine. Here's how
you can do it for various operating systems:

### Windows {#85c6 .graf .graf--h3 .graf-after--p name="85c6"}

1.  [Download the Git installer from
    [git-scm.com](https://git-scm.com/){.markup--anchor
    .markup--li-anchor data-href="https://git-scm.com/" rel="noopener"
    target="_blank"}.]{#74a8}
2.  [Run the installer and follow the steps.]{#ba9d}
3.  [Open **Git Bash** to start using Git via command line.]{#ff35}

### Mac {#3bc2 .graf .graf--h3 .graf-after--li name="3bc2"}

1.  [Open **Terminal**.]{#90ad}
2.  [Install Git using Homebrew:]{#d716}

- [`brew install git`{.markup--code .markup--li-code}]{#33db}

### Linux (Ubuntu) {#cc57 .graf .graf--h3 .graf-after--li name="cc57"}

1.  [Open **Terminal**.]{#8c14}
2.  [Install Git:]{#17eb}

- [`sudo apt-get update sudo apt-get install git`{.markup--code
  .markup--li-code}]{#0839}

Once installed, configure your Git identity:

``` {#5da5 .graf .graf--pre .graf-after--p .graf--trailing .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="csharp"}
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```
:::
::::
::::::

:::::: {#f197 .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### 3. Understanding Version Control {#6111 .graf .graf--h3 .graf--leading name="6111"}

Version control is the practice of tracking changes to files over time
so that you can recall specific versions later. With version control,
you can:

- [**Revert files** to a previous state.]{#756b}
- [**Compare changes** over time.]{#13d8}
- [**See who last modified something** that might be causing a
  bug.]{#a54f}
- [**Work on multiple versions** (branches) of a project
  simultaneously.]{#80e7}

There are two types of version control systems:

1.  [**Centralized (CVCS)**: One central server hosts the project, and
    developers pull and push their changes to this server.]{#d9a1}
2.  [**Distributed (DVCS)**: Every developer has a full copy of the
    project, allowing local development and committing without needing
    to communicate with a central server.]{#304a}

Git falls into the second category, making it more flexible and
fault-tolerant.
:::
::::
::::::

:::::: {#6d53 .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### 4. Git Basics {#c197 .graf .graf--h3 .graf--leading name="c197"}

Git operates through several key concepts that are critical to
understanding its workflow.

### Repositories {#fac0 .graf .graf--h3 .graf-after--p name="fac0"}

A **repository** is the basic unit of Git. It's a directory that
contains your project's files, as well as a hidden `.git`{.markup--code
.markup--p-code} directory where Git stores all the version control
information.

To create a new Git repository:

``` {#4825 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="csharp"}
git init
```

This initializes a repository in your project's root directory.

To clone an existing repository from a remote location:

``` {#35c7 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="bash"}
git clone <url>
```

### Commits {#c1e9 .graf .graf--h3 .graf-after--pre name="c1e9"}

A **commit** is a snapshot of your project at a specific point in time.
It records changes made to the files, allowing you to revert to it later
if necessary.

To commit changes:

1.  [First, add changes to the **staging area**:]{#699d}

- [`git add <filename>`{.markup--code .markup--li-code}]{#691b}

Then, commit the changes:

- [`git commit -m "Descriptive commit message"`{.markup--code
  .markup--li-code}]{#9b8a}

### Staging {#e657 .graf .graf--h3 .graf-after--li name="e657"}

Before committing, files need to be **staged**. The staging area allows
you to review changes and prepare them for the next commit. Think of it
as a way to mark which changes you're ready to commit.

To view the status of your files:

``` {#cc3f .graf .graf--pre .graf-after--p .graf--trailing .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="lua"}
git status
```
:::
::::
::::::

:::::: {#09b0 .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### 5. Branching in Git {#a8f5 .graf .graf--h3 .graf--leading name="a8f5"}

One of Git's most powerful features is its ability to create
**branches**. Branching allows you to work on separate versions of a
project without affecting the main codebase.

### Creating and Switching Branches {#551e .graf .graf--h3 .graf-after--p name="551e"}

To create a new branch:

``` {#c9d8 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="xml"}
git branch <branch-name>
```

To switch to a branch:

``` {#7410 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="xml"}
git checkout <branch-name>
```

Alternatively, you can create and switch to a new branch in one command:

``` {#d02c .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="css"}
git checkout -b <branch-name>
```

### Merging Branches {#6d9e .graf .graf--h3 .graf-after--pre name="6d9e"}

When your work on a branch is complete, you'll want to merge it back
into the main branch (often `master`{.markup--code .markup--p-code} or
`main`{.markup--code .markup--p-code}). To do this:

``` {#3203 .graf .graf--pre .graf-after--p .graf--trailing .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="css"}
git checkout main
git merge <branch-name>
```
:::
::::
::::::

:::::: {#80b1 .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### 6. Merging and Resolving Conflicts {#1599 .graf .graf--h3 .graf--leading name="1599"}

Merging combines changes from one branch into another. Most of the time,
Git automatically resolves differences between branches, but sometimes
conflicts arise when two branches modify the same part of a file.

### Resolving Conflicts {#4606 .graf .graf--h3 .graf-after--p name="4606"}

Git will mark conflicts in the affected files, and it's up to you to
resolve them manually:

``` {#764c .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="lua"}
git status
```

This will show which files have conflicts. Open the files, resolve the
differences, and then:

``` {#2175 .graf .graf--pre .graf-after--p .graf--trailing .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="sql"}
git add <filename>
git commit
```
:::
::::
::::::

:::::: {#a0bf .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### 7. Git Workflows {#16e8 .graf .graf--h3 .graf--leading name="16e8"}

Workflows define how your team will use Git. Some common ones include:

### Git Flow {#6d2e .graf .graf--h3 .graf-after--p name="6d2e"}

- [**Main**: This branch contains production-ready code.]{#7eae}
- [**Develop**: This branch is for development.]{#eb83}
- [**Feature branches**: Each feature is developed in its own branch,
  then merged into `develop`{.markup--code .markup--li-code}.]{#74eb}

### GitHub Flow {#54e0 .graf .graf--h3 .graf-after--li name="54e0"}

- [**Main**: Everything in this branch is deployable.]{#ad72}
- [**Feature branches**: Each feature gets a branch.]{#0b34}
- [**Pull Requests**: Used to propose changes to the main
  branch.]{#b6b4}
:::
::::
::::::

:::::: {#68bf .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### 8. Remote Repositories {#682e .graf .graf--h3 .graf--leading name="682e"}

Git allows you to interact with **remote repositories**, enabling
collaboration. Popular services like GitHub, GitLab, and Bitbucket host
Git repositories.

### Adding a Remote {#c482 .graf .graf--h3 .graf-after--p name="c482"}

To add a remote repository:

``` {#e812 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="csharp"}
git remote add origin <remote-url>
```

### Pushing Changes {#9a35 .graf .graf--h3 .graf-after--pre name="9a35"}

Once you've committed your changes locally, you can push them to a
remote repository:

``` {#bc50 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="xml"}
git push origin <branch-name>
```

### Pulling Changes {#ecea .graf .graf--h3 .graf-after--pre name="ecea"}

To update your local branch with the latest changes from a remote
repository:

``` {#fd79 .graf .graf--pre .graf-after--p .graf--trailing .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="xml"}
git pull origin <branch-name>
```
:::
::::
::::::

:::::: {#7f2f .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### 9. Working with Pull Requests {#7d2d .graf .graf--h3 .graf--leading name="7d2d"}

A **Pull Request** (PR) is a way to propose changes to a repository. PRs
are commonly used in collaborative projects to ensure that code changes
are reviewed before being merged into the main branch.

When creating a PR:

1.  [Push your feature branch to the remote repository.]{#e521}
2.  [Open a PR on GitHub or GitLab.]{#01c5}
3.  [Request reviewers to review and merge the changes.]{#d570}
:::
::::
::::::

:::::: {#e551 .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### 10. Advanced Git Commands {#686d .graf .graf--h3 .graf--leading name="686d"}

Once you're comfortable with Git basics, you can start using advanced
commands to optimize your workflow:

### Rebase {#7fe5 .graf .graf--h3 .graf-after--p name="7fe5"}

Rebasing allows you to move or combine a series of commits. It's often
used to keep a clean commit history.

To rebase onto another branch:

``` {#b470 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="xml"}
git checkout <branch>
git rebase <target-branch>
```

### Cherry-pick {#ea8b .graf .graf--h3 .graf-after--pre name="ea8b"}

If you want to apply a specific commit from one branch to another, use
`cherry-pick`{.markup--code .markup--p-code}:

``` {#f307 .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="xml"}
git checkout <branch>
git cherry-pick <commit-hash>
```

### Stash {#3215 .graf .graf--h3 .graf-after--pre name="3215"}

If you're in the middle of some work but need to switch branches, you
can use `stash`{.markup--code .markup--p-code} to save your uncommitted
changes temporarily:

``` {#aa1d .graf .graf--pre .graf-after--p .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
git stash
```

Later, retrieve them with:

``` {#8c1e .graf .graf--pre .graf-after--p .graf--trailing .graf--preV2 code-block-mode="1" spellcheck="false" code-block-lang="typescript"}
git stash apply
```
:::
::::
::::::

:::::: {#4690 .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### 11. Git Best Practices {#b777 .graf .graf--h3 .graf--leading name="b777"}

To ensure a smooth workflow, follow these Git best practices:

- [**Commit Often**: Frequent commits with meaningful messages make it
  easier to track progress and debug issues.]{#e0da}
- [**Use Branches**: Keep your work isolated from the main branch by
  using feature branches.]{#33c4}
- [**Write Descriptive Commit Messages**: Your commit messages should
  explain what changes were made and why.]{#c023}
- [**Sync Regularly**: Pull changes from the remote repository
  frequently to avoid conflicts.]{#71f4}
- [**Code Reviews**: Use Pull Requests and ensure all changes are
  reviewed before merging.]{#3f2b}
:::
::::
::::::

:::::: {#7eff .section .section .section--body}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### 12. Common Mistakes and Troubleshooting {#d9b7 .graf .graf--h3 .graf--leading name="d9b7"}

Even seasoned developers encounter Git issues. Here are some common
mistakes and how to fix them:

- [**Forgot to stage a file**: If you forget to `git add`{.markup--code
  .markup--li-code} a file, you can still stage it and amend the
  commit:]{#0bd5}
- [`git add <file> git commit --amend`{.markup--code
  .markup--li-code}]{#a398}
- [**Merge conflicts**: If conflicts arise, Git will guide you through
  resolving them manually. Use `git status`{.markup--code
  .markup--li-code} to see which files need attention.]{#a8c3}
- [**Detached HEAD state**: This happens when you checkout a commit
  directly instead of a branch. To fix it:]{#f014}
- [`git checkout <branch-name>`{.markup--code .markup--li-code}]{#9cc8}
:::
::::
::::::

:::::: {#78f5 .section .section .section--body .section--last}
::: section-divider

------------------------------------------------------------------------
:::

:::: section-content
::: {.section-inner .sectionLayout--insetColumn}
### Conclusion {#6203 .graf .graf--h3 .graf--leading name="6203"}

Git is an incredibly powerful tool, but it can be confusing when you're
just getting started. By understanding the basics of repositories,
commits, branches, and remotes, you'll be well on your way to mastering
Git. As you gain experience, you'll start using advanced commands like
`rebase`{.markup--code .markup--p-code} and `stash`{.markup--code
.markup--p-code} to improve your workflow.

Remember, Git is all about tracking changes and making collaboration
easier. With the right practices and tools, you'll never lose track of
your code again.

### Promote and Collaborate on Cybersecurity Insights {#3578 .graf .graf--h3 .graf-after--p name="3578"}

We are excited to offer promotional opportunities and guest post
collaborations on our blog and website, focusing on all aspects of
cybersecurity. Whether you're an expert with valuable insights to share
or a business looking to reach a wider audience, our platform provides
the perfect space to showcase your knowledge and services. Let's work
together to enhance our community's understanding of cybersecurity!

### About the Author: {#fb00 .graf .graf--h3 .graf-after--p name="fb00"}

[Vijay
Gupta](https://medium.com/@bevijaygupta/who-is-vijay-gupta-2ecad87f92a2){.markup--anchor
.markup--p-anchor
data-href="https://medium.com/@bevijaygupta/who-is-vijay-gupta-2ecad87f92a2"
rel="noopener" target="_blank"} is a cybersecurity enthusiast with
several years of experience in cyber security, [cyber crime forensics
investigation](https://play.google.com/store/books/details?id=VRz7EAAAQBAJ){.markup--anchor
.markup--p-anchor
data-href="https://play.google.com/store/books/details?id=VRz7EAAAQBAJ"
rel="noopener ugc nofollow noopener" target="_blank"}, and security
awareness training in schools and colleges. With a passion for
safeguarding digital environments and educating others about
cybersecurity best practices, Vijay has dedicated his career to
promoting cyber safety and resilience. Stay connected with Vijay Gupta
on various social media platforms and professional networks to access
valuable insights and stay updated on the latest cybersecurity trends.
:::
::::
::::::
:::::::::::::::::::::::::::::::::::::::::::::::::::::::::::

By [Vijay Kumar Gupta](https://medium.com/@bevijaygupta){.p-author
.h-card} on [September 6, 2024](https://medium.com/p/d47a912b52f2).

[Canonical
link](https://medium.com/@bevijaygupta/the-guide-to-git-i-never-had-a-developers-complete-manual-d47a912b52f2){.p-canonical}

Exported from [Medium](https://medium.com) on February 9, 2026.
