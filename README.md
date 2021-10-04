# How to contribute to a git project
This is a simple rule list for contributing to a project that is using git.  This file is specifically designed to be used by the [METU Racing Perception Driverless](https://meturacing.org/) team. This page should optimally be read in its [HTML version](https://htmlpreview.github.io/?https://github.com/utkuboduroglu/git-contrib-guide/blob/master/README.html).

At its very core, these are just rules to streamline the process of introducing changes to our codebase. The process is designed this way to improve readability and clarity, so that we can refer back to these changes later on and easily understand our progress. There are some ground rules on what should be followed.

Although it is convention for git to label new default branches `master`, we will resort to calling these branches `main` for this page.

# Working on changes
Whenever we need to introduce new changes, we will need to do it in a branch. The most important rule to be followed in this regard is that we **DO NOT** work directly on the `main` branch. This branch is only for storing code that is completely functional and only requires minor tweaks. When wanting to work on changes, the process is as follows:

1. Checkout to the `main` branch.
1. Create a new branch, aptly named after the task you want to complete:
    * For example, if you're going to work on implementing YOLOv4 on darknet, name your branch `models/darknet-YOLOv4`.
1. Checkout your new branch and introduce your changes there.

This way, your branch will contain the newest changes made to `main`, while also not introducing changes there.

## What happens after I complete my work in the branch?
If what you were working on is ready to be introduced to the `main` branch, navigate to your project's Github page and create a new pull request to pull the changes from your branch to `main`. Discuss how you're going to verify pull requests with your team and do so. For our workflow, we select other team members to review and approve pull requests.

# Styling changes
After your changes are made, you need to convert them into commits, but not before appropriately styling them for readability. Here are a few rules for "styling" commits to ensure they are readable and uniform.

## Modify the README file
Your changes will introduce new interfaces and/or features to the project. Please reflect these changes in the `README.md` file. Not all commits will introduce changes that need to be reflected in the README, but most changes will have caveats/notes that the user has to know about. Create a new section in the README file for this and include the changes in your commit.

## Follow the guidelines for commit messages
After you stage your changes and are ready to commit, you will need to specify a commit message to briefly describe what your commit does. Generally, using Github, these messages are along the lines of `'Update README.md'` or `'Add files via upload'`. These kinds of commit messages give no information about what the commit does and are generally considered to be bad commit messages. Ideally, your commit messages should completely describe what the commit is and any additional notes that one needs to be careful about. For our purposes, we will follow the [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/#summary) guidelines to ensure that we completely describe what is going on.

Taken from the conventional commits website, here is how a commit message should be structured:
```
<type>[optional scope]: <description>

[optional body]

[optional footer(s)]
```

The commit contains the following structural elements, to communicate intent to the consumers of your library:

1.    **fix**: a commit of the _type_ `fix` patches a bug in your codebase (this correlates with `PATCH` in Semantic Versioning).
1.    **feat**: a commit of the _type_ `feat` introduces a new feature to the codebase (this correlates with `MINOR` in Semantic Versioning).
1.    **BREAKING CHANGE**: a commit that has a footer `BREAKING CHANGE:`, or appends a `!` after the type/scope, introduces a breaking API change (correlating with `MAJOR` in Semantic Versioning). A BREAKING CHANGE can be part of commits of any _type_.
1.    _types_ other than `fix:` and `feat:` are allowed, for example [\@commitlint/config-conventional](https://github.com/conventional-changelog/commitlint/tree/master/%40commitlint/config-conventional) (based on the the Angular convention) recommends `build:`, `chore:`, `ci:`, `docs:`, `style:`, `refactor:`, `perf:`, `test:`, and others.
1.    _footers_ other than `BREAKING CHANGE: <description>` may be provided and follow a convention similar to [git trailer format](https://git-scm.com/docs/git-interpret-trailers).

# Steps to follow before introducing issues & approving requests
After everything else has been followed, we will have a pull request that is ready to be approved to be pulled into the `main` branch. Depending on how your team is handling this process, you may need to follow more steps to approve requests. These are the steps our team follows.

## Approving pull requests
For pull requests:

1. If there are no issues with the request, this must be stated in a team meeting. Only after everyone acknowledges that there are no issues can the pull request be approved and merged.
1. If there are issues with the request, the issues must be described underneath the pull request. After doing so, the pull request must be read by everyone in a team meeting and the next steps must be discussed. Either close the pull request until the issues are fixed, or if appropriate, approve the pull request but create an issue in the Issues tab of Github.

After the appropriate steps have been taken, someone else needs to review the pull request/issue. Select a person from the team to review these changes and assign them as the Assignee(s).

## Introducing issues
Issues are either introduced by commits or follow from external reasons (no dataset, badly tuned parameters etc.) The process for creating issues in the Issues tab is very simple. Simply describe the issue in a team meeting, and after everyone has been informed of the issue, create the issue in Github and link it. At this stage, the issue may need an assignee, so select those as well.

If any pull requests have been made that would fix the issue, link it to the issue using the 'Linked pull requests' prompt.

# `.gitignore` and not pushing personal files
During the development process, it is very natural that one would use tools (like IDEs) to help the development process. The issue is that these programs often introduce config files that reside in the project directory and are uploaded to Github. These files often contain personal details or are very large and clutter up the project repository. Therefore, we create `.gitignore` files in our repositories to prevent git from finding and including these config files in our project. Here are some of the things that must **NOT** be pushed upstream:

1. Any IDE config folders (`.idea`, `.vscode` etc.)
1. Any virtual environment folders (these take up space!)
1. Any dataset folders (images, rosbags etc.)
1. Any cache folders (`__pycache__` etc.)
1. Any error logs, weights files, model cfg files (`yolov4-*.cfg` etc.)

If datasets or config files are required for a project, they must be included in the team's cloud storage instead (GDrive, Dropbox etc.). `virtualenv`'s should always be created locally, **NEVER** push these upstream.

# Enforcing code standards
It is a good idea to enforce code standards to ensure that the code is always readable. Although we do not have rigid code standards, following conventions like Google's style guide for [Python](https://google.github.io/styleguide/pyguide.html) and [C++](https://google.github.io/styleguide/cppguide.html) is a good idea.

**NOTE**: These style guides will often enforce rules that are there because of Google's contributor size. It is often best that the code guides to be used be discussed by the team itself, since not everyone is Google.
