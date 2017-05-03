---
layout: episode
title: "Branch hygiene"
teaching: 10
exercises: 0
questions:
  - "Why is the Git log history important?"
objectives:
  - "Learn how to name branches."
---

## Branch naming

- Name your local branches such that you will recognize them 3 months later.
- "test", "foo", "debug", "mybranch" are not good branch names.
- Give descriptive names to remote branches.
- For topic branches we recommend to name them "author/topic" (example `joe/new-integrator`).
- Then everybody knows who is to be contacted about this branch (e.g. stale branches).
- Also you can easily find "your" branches:

```shell
$ git branch -r | grep joe
```

- Name bugfix branches after the issue/ticket (e.g. `issue-137`).
- For release branches we recommend e.g. `release-2.x` or `stable-2.x`.

---

## Always have only one main development line

- Document where it is.
- Organize branches according to features, not according to groups of people.
- Good: branches `feature-a`, `feature-b`, `feature-c`.
- Bad: branches `stockholm`, `san_francisco`, `helsinki`.
- Reason: `stockholm`, `san_francisco`, and `helsinki` will either diverge
  (three main development lines) or somebody will spend a heroic effort to keep
  them synchronized.

---

## Every commit on the main development line should compile

- Sometimes you want to find a commit in the past that broke some functionality.
- When using `git bisect` (we will exercise `git bisect` later)
  you will see that it is very helpful if all commits compile.
- On the other hand you will see that it is annoying if you hit a commit that does not compile.
- This is why we insist so much on a compiling main development line with nice history.
- There is no reason to commit broken or unfinished code to the main development line: for this we have branches.

---

## Branch hygiene

Often we have this situation:

```shell
$ git log --oneline

6e129cf documentation for feature C
05344f6 small fix for feature C
bc11c47 save work on feature C
aa25177 feature B
6b58ba4 feature A
```

But we would prefer to have this history:

```shell
$ git log --oneline

81e100c feature C
aa25177 feature B
6b58ba4 feature A
```

- We can use `git reset --soft aa25177`.
- This means that we move our repository back to commit `aa25177`
  **but** we keep the working tree of the last committed state.
- The final state of the actual code is identical.
- Alternative to `git reset --soft` is an interactive rebase.
- We recommend to create commits on the main development line which are nice logical units.
- Commits should be pickable (not too large not too small for a `cherry-pick`).
- Avoid ball-of-mud commits.