# git-tl: tlively's opinionated git workflow wrapper

git-tl makes it easy to create and manage [stacked
PRs](https://graphite.dev/blog/stacked-prs) on GitHub. It wraps plain git
commands and uses the [GitHub CLI](https://cli.github.com) to query the GitHub
API. The goal is for `git-tl` to do exactly what I need it to do in my everyday
work, not to be super configurable or general.

## Installation

Just put `git-tl` in your PATH. Then you can run `git tl ls`, `git tl sync`,
etc. This is not actually very pleasant to type, so you might want to configure
some aliases of you choice using `git config --global --edit`. Here are my aliases:

```ini
[alias]
	ls = tl ls
	bc = tl new-branch
	del = tl delete-branch
	up = tl up
	down = tl down
	sync = tl sync
	ss = tl push
```

You'll also have to separately [install](https://cli.github.com/manual/) the
GitHub CLI and run `gh auth login` to authorize it with your GitHub account.

## Commands

You can run `git-tl --help` to see an up-to-date list of subcommands and `git-tl
<subcommand> --help` to see the options for a particular subcommand. At time of
writing, these are the available subcommands:

 - **ls**: View the branches, how they are stacked, whether their corresponding
   PRs are up to date, the status of the PRs, and the URLs of the PRs.

 - **new-branch**: Create a new branch, either above or below the current branch.

 - **delete-branch**: Delete a branch and fix up the stack.

 - **up**: Check out the current branch's child.

 - **down**: Check out the current branch's parent.

 - **sync**: Fetch root branches, then rebase all other branches on their
   parents.

 - **push**: Push the current branch and its ancestors to GitHub, possibly
   creating new PRs.

## How stacking works

Each branch's parent is just its `upstream`, so you can reparent a branch
manually with `git branch --set-upstream-to new-parent my-branch`.
