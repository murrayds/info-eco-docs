---
title: Git and GitHub
---

# Git

## Overview
Git is a tool for version control, which means it tracks changes made to a set of computer file, maintaining a history of the files and making it easier for teams to maintain a single code base without introducing conflicting code. A directory of files managed by Git is called a [**repository**](https://git-scm.com/book/en/v2/Git-Basics-Getting-a-Git-Repository). After it is initialized, changes made to the files in a repository are automatically detected, and can be **staged**, marking them changes to be added to the repository history, and [**committed**](https://git-scm.com/book/en/v2/Git-Basics-Recording-Changes-to-the-Repository), which actually adds them. Commits are made to a [**branch**](https://git-scm.com/book/en/v2/Git-Branching-Branches-in-a-Nutshell), which is a snapshot of a set of commits that can be [**merged**](https://git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging) together. When team members each commit to different branches and merge them together only after proper testing and review, it makes it easier to avoid breaking changes and conflicts. 

## Typical workflow
First, initialize the repository, and use `git status` to check which branch you are currently on and what changes are detected
```bash
cd my_repository/
git init
git status
```

Create a new branch and check it out. Using `git status` after should show this as the new active branch.
```bash
git checkout -b new_branch
```

Make changes to the files in the project, stage them, and commit them to the branch
```bash
# make a change
touch new_file.txt

# changes are detected, but unstaged
git status 

# Stage the file
git add new_file.txt

# make the commit
git commit -m "added new_file.txt"
```

Now, merge back into the main branch
```bash
# Get the branch we started on
git checkout main
git merge new_branch
```

Ideally, the merge goes through without issue. However, occasionally there are **merge conflicts**, meaning that the changes made to one branch conflict with other recent changes. When a marge conflict happens, they will need to be resolved by manually selecting which changes are the "real" ones. Check the [documentation](https://git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging) for how to resolve conflicts. 

## Tips and best practices
- Files that you do not want to ever track can be ignored by adding their name to a file called `.gitignore` in the repository
- Git tracks changes by line. In general, this means that the only files that should be committed are those with "lines", such as raw text or code. Binary files, like images or pdfs, don't have lines, and so every time a commit is made, it is not just a few lines that are edited, but the entire image is replaced. The result is that (a) the Git history is not very informative, and (b) it takes more storage, as multiple copies of (often large) binary files are stored. 
- Jupyter notebooks change with every execution, so committing them can really lead to inflated changes. Be sure to clear notebook outputs for each commit. 
- Branches and commits should be made frequently, for even (or *especially*) very small changes. Doing so makes it easier to isolate issues and revert. 
- The `main`/`master` branch should always contain production-level code. That is, it should always work. Any changes should first be made to a branch, and only be merged into the main branch after proper review. 
- Messages should be short, but descriptive. This is because messages will help to identify specific changes in the repository history.

## Resources
- [Main git documentation](https://git-scm.com/)
- [Learn on CodeAcademy](https://www.codecademy.com/learn/learn-git)
- [Fun visual tutorial of Git commits and branching](https://learngitbranching.js.org/?locale=en_US)
- [Atlassian's tutorial on Git](https://www.atlassian.com/git)
- [Git best practices from GitLab](https://about.gitlab.com/topics/version-control/version-control-best-practices/)
# Trivia
- Git was created by Linus Torvalds to help manage development of the Linux kernal


# GitHub
## Overview
GitHub is a cloud-based platform to facilitate distributed version control using [[Git]]. Distributed, here, means that teams can all work on their own versions of a project on their local computer, and handle storage of these changes and merging of changes through a central GitHub-hosted repository. GitHub also provides other features, such as access control, issue tracking, continuous integration pipelines, and project management tools. 

Here, I outline several key features of GitHub and best practices for working with them. 

## Issues
GitHub allows project maintainers and anyone else with access to add [issues](https://docs.github.com/en/issues/tracking-your-work-with-issues/about-issues). An "issue" is something like a "ticket", it is some requested change to a project. It could be a bug that needs fixed, a feature that should be developed, or a question that needs resolved. 

When adding an issue, be as clear and concise as possible, and provide example code or output of the error. Add appropriate tags to the issue, which help with choosing which issues to prioritize. Where appropriate, assign issues to a project maintainer with the relevant expertise. 

Each issue is automatically assigned a number. This number can be referenced elsewhere in the repository using the \# character, such as `#42`. Link between issues, and from issues to pull requests whenever possible. 

## Pull Requests
Directly merging changes to the main branch is bad practice, it runs the risk of introducing breaking changes. Instead, merges should always be made using [pull requests](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/about-pull-requests) (or PR). When changes are committed to a branch, and those changes pushed to the GitHub repository, you can merge these changes by submitting a PR. When submitting, you should include a clear description of the changes, add appropriate tags, and assign an appropriate reviewer. Then, the pull requests acts as a thread in which the changes can be reviewed and discussed and additional changes made.

The PR feature of GitHub includes features for conducting code reviews and resolving merge conflicts. 

As best practice, do all development in a separate branch, and always merge changes to the main branch using a PR, even when on a solo project. 

## Forks
When there is a public repository on GitHub, you can make a copy of it by using the [fork](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/working-with-forks/about-forks) feature. A fork of a repository makes a separate repository owned by you, but from which changes such as pull requests can be submitted to the original (upstream) repository.


## Resources
- [GitHub documentation](https://docs.github.com/en/get-started/quickstart/hello-world)
# Tips and Best Practices
- **Do not commit API keys**. They will be public for everyone to see and use, and can be difficult to completely expunge from a repository's history. Consider storing your keys in your local environment. This same advice goes for any sensitive information. 
# Trivia
- GitHub was acquired by Microsoft in 2018
- The mascot for GitHub is the "OctoCat", a cat-octopus creature with 5 tentacles