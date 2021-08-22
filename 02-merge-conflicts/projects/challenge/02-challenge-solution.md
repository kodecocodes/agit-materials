# Chapter 2 — Challenge Solution

> **Note**: You may use the project in the challenge directory as a starter point for this challange.

## Challenge Prompt

This challenge simply reuses the commands you’ve already learned in this chapter to accomplish the following tasks:

- Checkout the `xReadmeUpdates` branch and look at the README.md file to see Xanthe’s version.
- Checkout `main`, since this is the destination for your merge.
- Resolve any merge conflicts by hand.
- Stage your changes.
- Commit your changes.
- Delete the `xReadmeUpdates` branch.

## Challenge Solution

Here are the steps I followed to complete this challenge; your solution may be slightly different:

1. Checkout the branch with the command: `git checkout xReadmeUpdates`.
2. Look at the file with the following command: `cat README.md`.
3. I can see that the file is pretty basic, with the simple information about the library and page, and some contact information below.
4. Switch to the main branch with the command: `git checkout main`.
5. Run the merge with the command: `git merge xReadmeUpdates`.
6. Git tells me there’s a merge conflict, so I open up README.md in a text editor.
7. I see the following contents in README.md:

```none
# magicSquareJS

magicSquareJS is a simple JavaScript library and HTML page that generates and validates magic squares.

For more information about magic squares, check out [Wikipedia](https://en.wikipedia.org/wiki/Magic_square).

<<<<<<< HEAD
# LICENSE

magicSquareJS is available under the Apache 2.0 license.

# Maintainers

This project is maintained by teamWYXZ:
- Will
- Yasmin
- Xanthe
- Zack
||||||| 4e6df27
=======
## Contact Info

For info on this project, please contact [Xanthe](mailto:xanthe@example.com).
>>>>>>> xReadmeUpdates
```

8. It appears someone has added license and maintainer information along the way, and Xanthe has added the contact information in a separate branch. Git sees this as a conflict because both authors added the text at the exact same place: the end of the file. Git doesn’t know anything about the semantics of this file, so it bails and asks you to manually correct the conflict.
9. I want to keep both sets of changes, so I remove the following line: `<<<<<<< HEAD`
10. I also remove: `||||||| 4e6df27`.
11. I also remove: `=======` but keep an empty blank line above `## Contact Info`.
12. I also remove: `>>>>> xReadmeUpdates`.
13. I save my work and exit out of the text editor.
14. I add my changes with the command: `git add README.md`.
15. I commit my changes with the command: `git commit`.
16. I use `:wq` to exit out of Vim and accept the default merge commit message.
17. I delete the `xReadmeUpdates` branch with the command: `git branch -d xReadmeUpdates`

---

end of file
