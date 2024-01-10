+++
title = "Website logistics"
date = "2024-01-09T19:29:30+08:00"

#
# description is optional
#
# description = "An optional description for SEO. If not provided, an automatically created summary will be used."

tags = ["markdown","syntax",]
+++

## After committing and pushing get stucked:
1. for uncommited changes:
git commit -m "Your commit message"

2. discard unstaged changes (note that directly copying from website will give a single - instead of consecutive two -):
git checkout -- .

3. for "already exists" branch:
git branch -d branch_name

4. use [link](https://stackoverflow.com/questions/5066041/moving-committed-but-not-pushed-changes-to-a-new-branch-after-pull) to restore: rebrase and other commands.

## To create a new blog:
terminal (top of the mac computer) -- new terminal -- *type* hugo new blog/name.md -- *editing file* -- *type* hugo server -- command + save -- *there will be a localhost link* -- *to make it visible to others, need to click the branch button (thrid on the left) AND click "+" button AND write a message AND choose "commit and push"*
