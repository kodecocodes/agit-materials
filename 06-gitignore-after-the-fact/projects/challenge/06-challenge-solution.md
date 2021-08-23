# Chapter 6 — Challenge Solution

If you ran into any issues in working through the chapter, you may instead use the project in the challenge directory as a starter point for this challange.

## Challenge Prompt

Now that you’ve learned how to eradicate any trace of a file from a repository, you can go back and remove all traces of **IGNORE_ME** from your repository.

You previously removed all traces of **SECRETS** from your repository, but that took you two steps. The challenge here is to do the same in one single command:

- Use `git filter-branch`.
- Use `--index-filter` to rewrite the index.
- You can use a similar `git rm` command, but remember, you’re filtering on a different file this time.
- Use `--prune-empty` to remove any empty commits.
- Remember that you want to apply this to all commits, starting at `HEAD` and going back.
- You’ll need to use `-f` to force this `filter-branch` operation, since you’ve already done a `filter-branch` and Git has stored a backup of that operation for you.

## Challenge Solution

Quite simply, you can reuse almost the same command you did to remove all traces of the SECRETS file:

```none
git filter-branch -f --index-filter 'git rm --cached --ignore-unmatch -- IGNORE_ME' --prune-empty HEAD
```

The only difference here is that you’ve run the `git rm` command against IGNORE_ME, and you’ve added the `--prune-empty` option as well.

---

end of file
