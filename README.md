# Git Practical

## 1. Pull and Merge difference

### Git Pull

→ The `git pull` command first runs `git fetch` which downloads content from the specified remote repository. Then a `git merge` is executed to merge the remote content refs and heads into a new local merge commit.

→ The command

- `$ git pull <remote> <branch>`

→ is really just the same as

- `$ git fetch <remote>`
- `$ git merge <remote> <branch>`

### Git Merge

→ Git allows merging the whole branch in another branch. Suppose you have made many changes on a `bugFix` branch and want to merge all of that ina `master` branch at a time. Git allows you to do so.

→ The result of git merge is immediately committed
(unless there is a conflict)

→ To merge the bugFix branch into the master branch, switch over to the master branch.

- `$ git checkout master`

→ Use the git merg. The syntax for this is as follows:

- `$ git merge bugFix `

### Example:-

![Screenshot (453)](https://user-images.githubusercontent.com/88922832/219932522-d445609d-0993-4445-a80c-2f9aa7a99860.png)

## 2. Rebase

→ Rebase is designed to integrate changes from one branch onto another. Rebasing is the process of combining or moving a sequence of commits on top of a new base commit. Git rebase is the linear process of merging.

### What Does Git Rebase Do?

→ A Git rebase changes the base of the developer’s branch from one commit to another, so it looks like they have created their branch from a different commit. When you perform a Git rebase, you are, in effect, rewriting history.

### How to Git Rebase

→ Here’s the syntax for launching a standard Git rebase:

- `git rebase <base>`

→ And here’s the syntax for launching an interactive Git rebase:

- `git rebase --interactive <base>`

→ This command opens an editor that lets you enter commands for each commit you want to rebase.

### Rebase Commands

→ Here’s a summary of the different commands associated with Git rebase.

| Commands                                      | Meaning                                                                                                                              |
| --------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| git rebase <base>                             | Performs the standard rebase                                                                                                         |
| git rebase – interactive <base>               | Performs the interactive rebase                                                                                                      |
| git rebase -- d                               | The commit gets discarded from the final combined commit block during playback.                                                      |
| git rebase -- p                               | This leaves the commit alone, not modifying the content or message, and keeping it as an individual commit in the branches’ history. |
| git rebase -- x                               | This executes a command line shell script for each marked commit during playback.                                                    |
| git status                                    | Checks the rebase status.                                                                                                            |
| git rebase -- continue                        | Continue with the changes that you made.                                                                                             |
| git rebase --skip                             | Skips the changes                                                                                                                    |
| git add <project file>                        | Adds your branch to the repository                                                                                                   |
| git commit -m "new commit for <branch name>." | Commits the changes.                                                                                                                 |

## 3. Change commit message

→ If a commit message contains unclear, incorrect, or sensitive information, we can amend it locally and push a new commit with a new message to GitHub. we can also change a commit message to add missing information.

### Rewriting the most recent commit message

→ We can change the most recent commit message using the `git commit --amend` command.

→ In Git, the text of the commit message is part of the commit. Changing the commit message will change the commit ID--i.e., the SHA1 checksum that names the commit. Effectively, you are creating a new commit that replaces the old one.

### Commit has not been pushed online

→ If the commit only exists in your local repository and has not been pushed to GitHub.com, you can amend the commit message with the `git commit --amend` command.

### Amending older or multiple commit messages

→ If you have already pushed the commit to GitHub.com, you will have to force push a commit with an amended message.

→ First amend the commit message with the `git commit --amend` command and then, Use the `push --force-with-lease` command to force push over the old commit.

- `$ git push --force-with-lease origin EXAMPLE-BRANCH`

## 4. Git Cherry Pick

→ `git cherry-pick` is a powerful command that enables arbitrary Git commits to be picked by reference and appended to the current working HEAD. Cherry picking is the act of picking a commit from a branch and applying it to another. `git cherry-pick` can be useful for undoing changes. For example, say a commit is accidently made to the wrong branch. You can switch to the correct branch and cherry-pick the commit to where it should belong.

→ `git cherry-pick` is a useful tool but not always a best practice. Cherry picking can cause duplicate commits and many scenarios where cherry picking would work, traditional merges are preferred instead.

### Example:-

![Screenshot (455)](https://user-images.githubusercontent.com/88922832/219932465-58859068-3f34-470b-8880-b47f689106cf.png)

### Syntax:-

- $ `git cherry-pick <commit id> `

## 5. Drop Commit

→ Deleting the commit in Git must be approached in one of two ways, depending on if you have or have not pushed your changes. Please note before attempting this, running these commands will DELETE your working directory changes. Any changes to tracked files in the working tree since <commit> are discarded. Be sure to separately save any changes you'd like to have.

### difference between git reset --mixed, --soft, and --hard:-

![image](https://user-images.githubusercontent.com/88922832/219931750-ee1e06ff-da8a-41b3-adac-efe27b21a033.png)

#### In the simplest terms:

- **--soft:** uncommit changes, changes are left staged (index).
- **--mixed:** (default): uncommit + unstage changes, changes are left in working tree.
- **--hard:** uncommit + unstage + delete changes, nothing left.

### delete commits from a branch in Git

→ If your changes have not been pushed yet simply enter the command

- `git reset --hard HEAD~1`

→ This will discard all working tree changes and move HEAD to the commit before HEAD.

→ If you'd like to delete the commits up until a specific commit, running <git log> into the command line to find the specific commit id and then running

- `git reset --hard <sha1-commit-id>`

→ will discard all working tree changes and move HEAD to the commit chosen.

→ Alternatively, if you have already pushed your changes you will need to run the following code

- `git push origin HEAD --force `

→ Please note if others have pulled this branch you would be better off starting a new branch. If you don't do this when someone else pulled, it will just merge it into their work, and you will get it pushed back up again.

→ If you need to find a commit that you "deleted", it is typically present in <git reflog> unless you have garbage collected your repository.
