# Syncing the Fork with Upstream

This fork (`ThomasLee94/superpowers`) tracks obra's `superpowers` as the
`upstream` remote and pushes to `origin`. Because the fork is **additive** — new
skill folders, modes, and wrappers, with core files left unedited — syncing with
upstream is low-conflict. See [`modes-and-wrappers.md`](modes-and-wrappers.md)
for why.

## TL;DR

```bash
git sync-main        # sync main with upstream/main
git sync-main dev    # sync any other branch with upstream/<branch>
```

## What `git sync-main` does

`git sync-main` is a git alias that rebases the local branch onto its upstream
counterpart and force-pushes the result to your fork:

```sh
f(){ set -e
  b=${1:-main}
  # refuse to run with uncommitted changes
  git diff --quiet && git diff --cached --quiet || { echo "Commit or stash changes first."; exit 1; }
  git fetch --all --prune
  git checkout "$b"
  git rebase "upstream/$b"
  git push --force-with-lease origin "$b"
}; f
```

Step by step:

1. **Guard** — aborts if the working tree or index has uncommitted changes, so a
   sync never happens on top of half-finished work.
2. **`git fetch --all --prune`** — updates every remote (`origin`, `upstream`)
   and prunes branches deleted upstream.
3. **`git checkout <branch>`** — switches to the target branch (default `main`).
4. **`git rebase upstream/<branch>`** — replays your local commits on top of
   upstream, keeping history linear (no merge commits).
5. **`git push --force-with-lease origin <branch>`** — updates your fork.
   Rebasing rewrites commit hashes, so a force push is required;
   `--force-with-lease` refuses to overwrite commits you haven't seen, making it
   safe against clobbering work pushed from elsewhere.

## Setup on a new machine

The alias lives in git config, not in the repo, so recreate it once per machine:

```bash
git config --global alias.sync-main '!f(){ set -e; b=${1:-main}; git diff --quiet && git diff --cached --quiet || { echo "Commit or stash changes first."; exit 1; }; git fetch --all --prune; git checkout "$b"; git rebase "upstream/$b"; git push --force-with-lease origin "$b"; }; f'
```

Make sure the `upstream` remote exists:

```bash
git remote add upstream https://github.com/obra/superpowers.git   # if missing
git remote -v
```

## Manual equivalent

Without the alias:

```bash
git fetch upstream
git checkout main
git rebase upstream/main
git push --force-with-lease origin main
```

A merge-based flow (`git fetch upstream && git merge upstream/main`, then a plain
`git push`) also works if you prefer merge commits over a linear history — it
avoids the force push at the cost of a merge commit each sync.
