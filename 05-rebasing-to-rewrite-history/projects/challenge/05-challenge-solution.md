# Chapter 5 - Challenge Solution

If you ran into any issues in working through the chapter, you may instead use the project in the challenge directory as a starter point for this challange.

## Challenge 1 Prompt: More squashing

You’d like to squash all of the `check0x` commits into one tidy commit. And you _could_ follow the pattern above, where you first rearrange the commits in one rebase and then perform the squash in a separate rebase.

But you can do this all in one rebase pass:

1. Figure out what your base ancestor is for the rebase.
2. Start an interactive rebase operation.
3. Reorder the `check0x` commits.
4. Change the `pick` rebase script command for `squash` on all commits from the `check02` commit, down to and including the `Refactoring the main check function` commit.
5. Save your work in Vim and exit.
6. Create a commit message in Vim for the squash operation.
7. Take a look at your Git log to see the changes you’ve made.

## Challenge 1 Solution

Here’s how I solved this:

1. Execute `git log --oneline --graph` to see the commit history. You'll see:

```none
* f8d6e1b (HEAD -> wValidator) Added Chris to README and updated team acronym
* ededa27 Refactoring the main check function
* 2670142 Removing TODO
* d0bdabb check04: Checking diagonal sums
* 4424300 check03: Checking row and column sums
* 5e087af check02: Checking the array contains the correct values
* 1cb3ad3 Creating utility functions for Magic Square validation
* 6adde96 check01: checking that the 2D array is square
* 69670e7 Adding a new secret
```

Again, it makes sense to rebase on top of `69670e7` as the ancestor commit.

2. Start the interactive rebase with `git rebase -i 69670e7`

3. Use **dd** and **p** to move the lines in the rebase script around to get all of the check01 to check04 lines together:

```none
pick 1cb3ad3 Creating utility functions for Magic Square validation
pick 6adde96 check01: checking that the 2D array is square
pick 5e087af check02: Checking the array contains the correct values
pick 4424300 check03: Checking row and column sums
pick d0bdabb check04: Checking diagonal sums
pick 2670142 Removing TODO
pick ededa27 Refactoring the main check function
pick f8d6e1b Added Chris to README and updated team acronym
```

4. Change the commands for "check02", "check03", "check04", "Removing TODO" and "Refactoring the main check function" from **pick** to **s**. You can use **s** as an abbreviation for squash. You should now have the following:

```none
pick 1cb3ad3 Creating utility functions for Magic Square validation
pick 6adde96 check01: checking that the 2D array is square
s 5e087af check02: Checking the array contains the correct values
s 4424300 check03: Checking row and column sums
s d0bdabb check04: Checking diagonal sums
s 2670142 Removing TODO
s ededa27 Refactoring the main check function
pick f8d6e1b Added Chris to README and updated team acronym
```

5. Save your changes with **Escape**, then **:wq**, and **Enter**.
6. Once you’re back into Vim to create the commit message for the squash, use **dG** to clear the buffer, press **i** to enter Insert mode, and set the message to "Creating the magic square validation function". Again use **Escape**, **:wq**, and **Enter** to save your work and exit Vim.
7. Pull up your log with `git log --oneline --graph` and you’ll see your squashed commit:

```none
* bd55c2b (HEAD -> wValidator) Added Chris to README and updated team acronym
* 10103c2 Creating the magic square validation function
* 6387539 Creating utility functions for Magic Square validation
* 69670e7 Adding a new secret
```

Nice and tidy!

## Challenge 2 Prompt: Rebase your changes onto main

Now that you’ve squashed your work down to just a few commits, it’s time to get wValidator back into the `main` branch. It’s likely your first instinct is to merge `wValidator` back to `main`. However, you’re a rebase guru by this point, so you’ll rebase those commits on top of `main` instead:

1. Execute `git rebase` with `main` as your rebase target.
2. Crud — a conflict. Open README.md and resolve the conflict to preserve your changes, and move the changes to the `## Contact` section.
3. Save your work.
4. Stage those changes with `git add README.md`.
5. Continue the rebase with `git rebase --continue`.
6. Check the log to see where `main` points and where `wValidator` points.
7. Check out the `main` branch.
8. Execute `git merge` for `wValidator`. What’s special about this merge that lets you avoid a merge commit?
9. Delete the `wValidator` branch.

## Challenge 2 Solution

Here’s how I solved this challenge:

1. Execute `git rebase main` to rebase the current branch on top of `main`.
2. I’ve got a conflict in README.md. So I open up that file, and see the following issue:

```none
# Maintainers

This project is maintained by teamWYXZC:
- Will
- Yasmin
- Xanthe
- Zack
<<<<<<< HEAD

## Contact Info

For info on this project, please contact [Xanthe](mailto:xanthe@example.com).

## Contributing

To contribute to this project, simply create a pull request on this repository and we’ll review it when we can.
||||||| parent of bd55c2b (Added Chris to README and updated team acronym)
=======
- Chris
>>>>>>> bd55c2b (Added Chris to README and updated team acronym)
```

Ah, OK -- the earlier addition of the Contact section conflicts with my addition of "- Chris". I just fix up the file, preserving both sections, so it looks like this:

```none
# Maintainers

This project is maintained by teamWYXZC:
- Will
- Yasmin
- Xanthe
- Zack
- Chris

## Contact Info

For info on this project, please contact [Xanthe](mailto:xanthe@example.com).

## Contributing

To contribute to this project, simply create a pull request on this repository and we’ll review it when we can.
```

3. I save my changes, and exit.
4. Stage those changes with `git add README.md`.
5. Continue the rebase with `git rebase --continue` and accept the default message in Vim.
6. If I execute `git log --oneline --graph --all` I see the following:

```none
* aed4d27 (HEAD -> wValidator) Added Chris to README and updated team acronym
* e50697e Creating the magic square validation function
* d991b70 Creating utility functions for Magic Square validation
* 4a48a7d (main) Updates readme
```

Now you can merge `main` and `wValidator`. Remember, rebasing simply replays the commits on top of the new base; it doesn’t move the labels around. That’s why you need to merge here.

7. `git checkout main`
8. `git merge wValidator`

Git responds with:

```none
Updating 4a48a7d..aed4d27
Fast-forward
 README.md                    |  3 ++-
 js/magic_square/validator.js | 90 ++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++--
 2 files changed, 90 insertions(+), 3 deletions(-)
```

Aha - a fast-forward merge. That’s what’s special about this. Remember, a fast-forward merge can happen when the branch to merge is a direct descendent of the branch being merged into.

9. Now that the merge has completed, use `git branch -D wValidator` to delete the branch.

---

end of file
