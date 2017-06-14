---
layout: post
title:  "GitHub Usage Notes"
date:   2016-12-05 17:28:28 -0800
categories: 
---

## Basic commit and push usage

Clone the remote repo.

`git clone git@github.com:username/repo_name.git`

Sometimes you will get an empty dir content after 
you cloned it. It's because it does not have a 
`master` branch.

Show all the branches.

`git branch -a`

Enter a spefic branche.

`git checkout gh-pages`

See the modification status of the branch

`git status`

Add file to commmit.

`git add about.md`

Commit:

`git commit -m "description of this commit"`

Push:

`git push`



#### Adding an existing project to GitHub using command line

Follow [here](https://help.github.com/articles/adding-an-existing-project-to-github-using-the-command-line/).

