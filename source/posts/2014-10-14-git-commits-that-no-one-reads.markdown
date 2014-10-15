---
title: Commits that No One Reads
layout: post
---

Does your commit log look like this?

```
* 245754d - work in progress

* d15cf15 - Handled a particular error.

* 2b55942 - One more time, but with feeling.
```

This is really frustrating because:

- It takes a lot of commands to view the change;
- And a very long time to understand what has changed;
- And you still have no idea why the change was made.

These problems get worse over time.

It would be amazing if you could do:

```
git log --oneline
```

And understand:

- The history of the code.
- How the team works together.
- Coding standards that a used;
- And most importantly, why each of the changes were made.

## 6 Years Ago

Tim Pope came up with a good system of formatting git commits:

> Capitalized, short (50 chars or less) summary

> More detailed explanatory text, if necessary.  Wrap it to about 72
> characters or so.  In some contexts, the first line is treated as the
> subject of an email and the rest of the text as the body.  The blank
> line separating the summary from the body is critical (unless you omit
> the body entirely); tools like rebase can get confused if you run the
> two together.

> Write your commit message in the imperative: "Fix bug" and not "Fixed bug"
> or "Fixes bug."  This convention matches up with commit messages generated
> by commands like git merge and git revert.

> Further paragraphs come after blank lines.

> - Bullet points are okay, too
> - Typically a hyphen or asterisk is used for the bullet, followed by a
>   single space, with blank lines in between, but conventions vary here
> - Use a hanging indent

[A Note About Git Commit Messages](http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html)

One of the most important elements of style presented here is that __git commits should be written in the present tense__. Doing this matches the output of commands like `git merge` and `git revert`.

Taking this a step further you can drill into the first line. It is the most important part of a git commit because all git tools focus on it.

The first line of a good git commit should have:

- What the change is.
- Where the change is.
- Why the change is being made.

Below is an example of the first line of a good git commit:

```
Add notice and example to timeline to improve onboarding.
```

- __What__: Add notice and example
- __Where__: to timeline
- __Why__: to improve onboarding.

## Going a Step Further

Deis has done an amazing job of [formalizing git commits](http://docs.deis.io/en/latest/contributing/standards/#commit-style-guide). They have come up with the form:

```
{type}({scope}): {subject}
<BLANK LINE>
{body}
<BLANK LINE>
{footer}
```

This dramatically increases clarity in the first line. The type can be anyone of the following:

- feat -> feature
- fix -> bug fix
- docs -> documentation
- style -> formatting
- ref -> refactoring code
- test -> adding missing tests
- chore -> maintenance

The first line needs to be all lowercase without a fullstop at the end. E.g.

```
feat(timeline): add notice and example to improve onboarding
```

This makes our example more succinct but keeps the what, where and why in commits.

- __What__: feat and "add notice and example"
- __Where__: (timeline)
- __Why__: to improve onboarding

## Taking Care of Commits

Read through [formalizing git commits](http://docs.deis.io/en/latest/contributing/standards/#commit-style-guide) and get into a consistent routine with your commits. Get your team to do the same and in no time your git log will smell like flowers.
