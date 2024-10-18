# Dotfiles

Manage your configuration "dot" files with Git.

## Philosophy

All I want for dotfile management is a thin Git wrapper.

The entire program is a small POSIX shell script that started as:
```bash
#!/bin/sh -eu
git \
    --git-dir="~/.local/share/dotfiles/dotfiles.git" \
    --work-tree="~" \
    "$@"
```

It's bigger now, but only because I've added barely enough extra features to eliminate some manual steps and annoyances.

Almost everything else can and should be done with setup programs checked into your dotfiles repository and automatically called by Git hooks.

## ⚠️ **Caution**

* *Your dotfiles generally contain sensitive and/or personal information.*
Anyone with access to your repository can access this information.
* *Setup programs from your repository are run whenever you clone or pull.*
Anyone with access to your repository can cause you to run arbitrary code.
* Therefore, **do not store your dotfiles in a public or insecure repository!**
If you want to share some of your dotfiles publically in Git repositories, carefully curate what you share, and set them up as submodules.

**This is true for all other dotfile managers as well**, but most don't warn you very strongly about this, or worse, assume by default that you are storing your dotfiles on `github.com`.
(I would highly recommend against this.)

## Quick Start (First System)

Download the "dotfiles" shell script and run `dotfiles init`, or:

```bash
sh -c 'curl -fsL https://github.com/wjl/dotfiles-project/releases/latest/download/dotfiles | sh -s init'
```

This will install dotfiles and initialize a new repository.
After this, you basically just use `dotfiles` just like `git` to manage things, for example:

```bash
dotfiles commit -m "New dotfiles repository."
dotfiles remote add origin <your dotfiles repo>
dotfiles push
```

## Quick Start (Additional System)

Download the "dotfiles" shell script and run `dotfiles clone <your dotfiles repo>`, or:

```bash
sh -c 'curl -fsL https://github.com/wjl/dotfiles-project/releases/latest/download/dotfiles | sh -s clone <your dotfiles repo>'
```

## General Usage

You basically just do `dotfiles <some git command>`, so you need to know how to use Git.

```
Dotfiles version 1.0.3
by Wesley J. Landaker
See https://github.com/wjl/dotfiles-project

Usage: dotfiles <command> ...

Manage configuration "dot" files with Git.

Commands:
  version       -- show version information
  help          -- show this help message

  init          -- initialize a dotfiles repository
  clone <repo>  -- clone an existing dotfiles repository
  setup         -- re-run setup programs explicitly

  git <command> -- run a Git command in dotfiles context
  *             -- anything else is passed through to Git

Your files:
  Git Repository: /home/you/.local/share/dotfiles/dotfiles.git
  Setup Programs: /home/you/.config/dotfiles/setup
```

## Alternatives

I started with a simple Git wrapper years ago.
It was a little clunky, but who cares, it was just for me.
Then I got exited about and tried other dotfiles managers.
A couple of them are pretty good.
Unfortunately, these are various technical, philosophical, and pragmatic reasons that I don't use these anymore.

But you may like them:

* [YADM](https://yadm.io/)
* [chezmoi](https://www.chezmoi.io/)
