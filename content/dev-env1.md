+++
date = "2015-07-08"
draft = false
title = "One Stop Dev Shop pt. 1"

+++

# Part one: Everything in one place
A **lot** of time and effort goes into creating a development environment that is productive and allows you to get down to work.
Things get even more complicated when working on more than one machine. The goal of this series is to give you tips and a starting place for a unified environment.

I recently started a position where a Mac was provided and, after working exclusively on a GNU/Linux system,
I needed to have a config that I could seemlessly use between both machines. So I started building my portable Unix dev environemnt.
I wanted to share what goes into creating a complete and portable

## Git
Git is intergal to almost every development team or company these days --- side note if you're not using version control yet, do it now, *seriously* ---
and it's what holds this environment together for a number of reasons.

* Anything you will be working on with more than one computer needs to be in `git`. Then just `git push` from one and `git pull` from the next and you're back to work. Done. Next.
* Git is makes this system work. You need to have a way to have all your config files easily accessable and sync-able across machines. Git is that way.

### Use a central repository
"Dotfile" repos are a common convention for developers to maintain a single place for config files.
However, they can be a lot more useful than that. [Mine](https://github.com/barbour-em/dotfiles) holds things like wallpapers, screenshots, and various reminders about
using some Unix tools. Determine what will be useful or convenient for you to have everywhere and throw it in there.

Clone this repository on all of your machines. Push and pull from it when changes are made. **How easy was that?**

For files that will have to live outside of the cloned repository (e.g. .vimrc, .tmux.conf, etc), the easiest way to keep these version controlled is symlinking them from
your repo, to where they have to reside. For example:

```bash
$ ln -s $HOME/dotfiles/.vimrc $HOME/.vimrc
```

All this means for you is that you will need to remember to commit and push these changes every once in a while to keep things up to date. Better yet, use a cron job to
systematically do this for you.

### Configure git
Okay, so we have all of our configurations and anything we want under git --- if you don't have any configs, don't worry, by the end of this post you will --- but let's
customize this tool we will be using a lot to make it even faster to use.

#### Aliases

A lot of my day is spent working directly with git. At my shop, we use a [git-flow](https://www.atlassian.com/git/tutorials/comparing-workflows/feature-branch-workflow)
workflow which, for me, means a lot of branching, merging, commiting, and rebasing. Because of this, I find myself typing a lot of commands many, many times a day.
Luckily, with git there is a way to cut down on the amount of typing you have to do to get stuff done.

Aliases are a *huge* time-saver for my workflow. Here is my global `.gitconfig` with a list of all the aliases I use.

<script src="https://gist.github.com/barbour-em/f13eab896dffca8c28b9.js"></script>

The biggest ones are

* `undo` which reverts the last commit and is a lot easier to remember
* `up` which combines some of my most typed commands into two letters to update a branch
* `ls` which shows the log in a much nicer format and also takes a number of lines to stop (i.e. `git ls -10` will show the last 10 commits)
    * This still doesn't beat [tig](https://github.com/jonas/tig), an awesome ncurses git interface that I would recommend to anyone

#### Commit template

In my `.gitconfig` above, you'll also notice a commit template. This is something that I learned about recently but has already saved me a huge amount of time writing
commit messages. Pretty commits are important, and often necessary depending on who you're contributing to, and setting up a template that encourages this behavior
and has boilerplate written makes things a lot easier. Here is what my template looks like.

<script src="https://gist.github.com/barbour-em/3b40a805c431a42b6181.js"></script>

Removing the octothorp (#) from the beginning of a line will make it show up in the commit and different commit stubs are already there. Just remove the comment,
add a description, add a body below the line and boom. There are also guides for line length wraps for both halves.

I recommend that you take a look at what your commits usually, or should, look like and write one for yourself. Then, throw it in your `dotfiles` push and start being more
productive!

---
*This post is part 1 in a series of posts I am writing about maintaining a consistent and portable
development envrionment across unix-like machines.*

---