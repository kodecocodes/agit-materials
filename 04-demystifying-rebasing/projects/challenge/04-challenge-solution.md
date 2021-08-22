# Chapter 4 - Challenge Solution

If you ran into any issues in working through the chapter, you may instead use the project in the challenge directory as a starter point for this challange.

## Challenge Prompt

You’ve discovered that Zach has also been doing a bit of refactoring on the **zValidator** branch with the range checking function:

Run the following to see the relationship between the two branches:

```none
git log --oneline --graph wValidator origin/zValidator
```

You'll see that there is one commit on `origin/zValidator` after it branched from `wValidator`

```none
...
* 64b1b51 check02: Checking the array contains the correct values
| * 136dc26 (origin/zValidator) Refactoring the range checking function
|/
* 665575c util02: Adding function to check the range of values
```

Your challenge is to rebase the work you’ve done on the `wValidator` branch on top of Zach's `zValidator` branch. Again, the shared context here and the limited scope of the changes mean you don’t need a merge commit.

And don't worry, you won't have to resolve any merge conflicts!

## Challenge Solution

Here are the steps to follow to complete this challenge:

- First checkout `zValidator` with `git checkout zValidator`.
- Now switch back to the `wValidator` branch with `git checkout wValidator`.
- Execute `git rebase zValidator`; this should complete without conflict.
- Execute `git branch -d zValidator`; this should complete without issues.

> **Note**: Instead of checking out and then deleting `zValidator` you could also have just rebased directly onto `origin/zValidator`.

---

end of file
