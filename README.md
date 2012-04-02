# git-paradox
---
![](http://i.imgur.com/tnEG7.png)

## What is it? Why use it?
`git-paradox` is an additional command to git that creates what I would call a "time paradox".

*`git-paradox` takes the data from some commit in the past and brings it to the present without disturbing any of the past*

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
git paradox [options] <commit>
```
where <commit> is some of the first characters in the commit hash, or a shortcut like HEAD~n, or HEAD^^^

At this time, there are no options

## How to install
From this point forward `master` will be stable


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
