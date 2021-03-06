# git-paradox
Pull requests welcome!
---
![](http://i.imgur.com/tnEG7.png)

## What is it? Why use it?
`git-paradox` is an additional command to git that creates what I would call a "time paradox".

*`git-paradox` takes the data from some commit in the past and brings it to the present without disturbing any of the past*

[See full-size image](http://i.imgur.com/4PYqS.png)

![](http://i.imgur.com/4PYqS.png)
Flowchart made with [Gliffy](http://www.gliffy.com/)

`git-paradox` solves a common problem that I keep running into while working on projects: I realize that for the past 5 commits, the code that I have been working on is fundamentally broken, or it's broken in such a way that fixing the errors would take longer than just starting from when the code was working.

Essentially, all I want to do is take that working commit from HEAD~5 and bring it to the tip of my current branch. I don't want to lose my history, so I don't want to `git reset --hard HEAD~5`.
After searching on the internet for a while, I found a lot of solutions, and they all were several lines and unintuitive. This is the best one I could find:

```bash
git rm -r .
git checkout HEAD~5 .
git commit
```

The first line is pretty scary: Delete everything. Then things start making sense once you hit the next line since you don't want to have any new files in your working directory. If you abort the commit (let's say you changed your mind at this point). You have to do `git rm -rf .; git checkout HEAD .` in order to recover.

I felt that this is a fundamental funtion should be accessible with only one command.
Use it if you want an easy way to take some commit from the past and copy it to the tip of a branch.

As an example, lets say you want 5 commits ago to also be at the tip of your branch:

```bash
git paradox HEAD~5
```

## Usage
```bash
usage: git paradox [options] <commit>
Copy commit to the tip of the current branch easily and safely
where commit is part of a commit hash 'ea342e' or a shortcut 
      such as 'HEAD^^', 'HEAD~5'

Options:
  -m <msg>                the message to be inserted after the 
                                message indicating rollback in the commit
  -M <msg>                the message to be inserted in the commit
  -f <msg-file>           a file whose contents are to be 
                                inserted after the message indicating 
                                rollback in the commit
  -F <msg-file>           a file whose contents are to be 
                                inserted in the in the commit
Examples:
  git paradox ea342
  git paradox -M 'Back to when module X was working'
  git paradox -f file.whose.contents.are.message.txt

Report any issues to https://github.com/bkase/git-paradox
```

## How to install
From this point forward `master` will be stable

[Install from AUR](https://aur.archlinux.org/packages.php?ID=58154)

or 

Clone the repo somewhere and 
add repo to your path

```bash
cd /path/to/somewhere
git clone https://bkase@github.com/bkase/git-paradox.git
PATH=$PATH:/path/to/somewhere
```
or copy `git-paradox` to a folder in your path

```bash
git clone https://bkase@github.com/bkase/git-paradox.git
sudo cp git-paradox /usr/bin
```

## Why call it `git-paradox`?
When this command is issued, some state of the repository from the past is simultaneously existing in both the past and present. Any commits after this one from the past still exist as they once did, but this one is now both in front of and behind this set of commits.

It's sort of like a time paradox.
