# Chapter 3 - Challenge Solution

If you ran into any issues in working through the chapter, you may instead use the project in the challenge directory as a starter point for this challange.

## Challenge Prompt

This challenge has you diving into the Git documentation a bit, to solve the following problem:

Execute `git stash list` and you’ll see there’s still a stash there. But you popped that stash, didn’t you? Of course you did.

Your challenge is twofold, and may require a little dive into the Git documentation:

1. Explain why there’s still a stash in the stack, even though you executed `git stash pop`.
2. Remove the remaining entry from the stash without using `git stash pop` or `git stash clear`. There’s one more way to remove entries from the stack with `git stash` — what is it?

## Challenge Solution

To answer #1, you executed `git stash pop` for sure, but Git encountered a conflict when trying to merge your stash. So Git immediately bailed on the stash removal option, and left the merge conflicts for you to clean up. So Git leaves the stash on the stack, just in case you wanted to roll back. If Git removed the stash from the stack before you had a chance to roll back, you’d be in a weird indeterminate state where you had a conflict and your saved stash would have vanished.

To answer #2, you’ll need to dig into the Git documentation just a little. `man git stash` or `git stash --help` will do it for you command-line diehards, but you can also search up the git stash documentation on the web.

Turns out there’s another way to remove stashes from the stack: `git stash drop <stashname>`. If you look back at the output from `git stash pop`, you’ll see that the last line of output reads like the following:

Dropped refs/stash@{0} (a75edcdeb09e2f2c5096fca4ecb278097a310d7a)

So popping a stash is just a combination of `apply` and then `drop`.

Execute the following to drop that last stash:

```bash
git stash drop stash@{0}
```

"git stash drop" is useful for cleaning up your stash stack, should you have a lot on there. But if your stash stack gets too big, then you’re invoking a lot of overhead to manage that stash stack. My preference is to keep my stash stacks brief and as short-lived as possible.

---

end of file
