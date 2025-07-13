Great things never came from comfort zones.

– Tony Luziaya

## 1 / 9

Sarah has been working on a new story The Hare and Tortoise for a while now, in the branch story/hare-and-tortoise
Explore the local repository at /home/sarah/story-blog

```
sarah $ cd story-blog/
sarah (story/hare-and-tortoise)$ ls
frogs-and-ox.txt       hare-and-tortoise.txt  lion-and-mouse.txt     story-index.txt
sarah (story/hare-and-tortoise)$ git status
On branch story/hare-and-tortoise
nothing to commit, working tree clean
sarah (story/hare-and-tortoise)$ git branch
  master
  story/frogs-and-ox
* story/hare-and-tortoise
sarah (story/hare-and-tortoise)$ git log
commit 93ff5b0bddc24d271bf53ae74a0563f3a759eefc (HEAD -> story/hare-and-tortoise)
Author: sarah <sarah@example.com>
Date:   Sun Jul 13 11:30:53 2025 +0000

    Add first draft of hare-and-tortoise story

commit 9df9acbf877d03bfa811a97c82980ebd50ad5ae6 (master)
Author: sarah <sarah@example.com>
Date:   Sun Jul 13 11:30:53 2025 +0000

    Added the story index file

commit 88348f90f55dcbbb14e3781612d7081323f7dbd6 (origin/master, story/frogs-and-ox)
Author: sarah <sarah@example.com>
Date:   Sun Jul 13 11:30:52 2025 +0000

    Completed frogs-and-ox story

commit 837dcbec976fcbe5e5252807deda6eb302c6bb6f
Author: sarah <sarah@example.com>
Date:   Sun Jul 13 11:30:52 2025 +0000

    Add incomplete frogs-and-ox story

commit 418106110d603b7b703740fc5b64b797130a11c5
Author: sarah <sarah@example.com>
Date:   Sun Jul 13 11:30:52 2025 +0000

    Added the lion and mouse story
```

## 2 / 9

Meanwhile her team mates have pushed more stories and updates to the story-index.txt file on the shared central repository.
Check the UI of the remote repository using the Gitea Portal UI button and identify who pushed the last commit.

Use the below credentials:
Username: sarah
Password: Sarah_pass123

там развернут gitea

```
  tom	77e0d91305	Added the wolf and goat story	3 минут назад
```
  
right answeer - "Tom"

## 3 / 9

Let's pull all the changes from remote to our local master branch.
Checkout the master branch and pull changes from remote	

```
sarah (story/hare-and-tortoise)$ git checkout master && git pull origin master
Switched to branch 'master'
From http://git.example.com/sarah/story-blog
 * branch            master     -> FETCH_HEAD
hint: Pulling without specifying how to reconcile divergent branches is
hint: discouraged. You can squelch this message by running one of the following
hint: commands sometime before your next pull:
hint: 
hint:   git config pull.rebase false  # merge (the default strategy)
hint:   git config pull.rebase true   # rebase
hint:   git config pull.ff only       # fast-forward only
hint: 
hint: You can replace "git config" with "git config --global" to set a default
hint: preference for all repositories. You can also pass --rebase, --no-rebase,
hint: or --ff-only on the command line to override the configured default per
hint: invocation.
CONFLICT (add/add): Merge conflict in story-index.txt
Auto-merging story-index.txt
Merge made by the 'recursive' strategy.
 fox-and-grapes.txt | 21 +++++++++++++++++++++
 story-index.txt    |  4 ++++
 wolf-and-goat.txt  | 17 +++++++++++++++++
 3 files changed, 42 insertions(+)
 create mode 100644 fox-and-grapes.txt
 create mode 100644 wolf-and-goat.txt
```

## 4 / 9

Great! Now our local master branch has many more commits. Sarah would like to update her working branch - story/hare-and-tortoise - branch with the latest updates.
Sarah is especially looking for the story-index.txt file so that she can update her story to it the clean way and not end up in a merge conflict as it did previously.	

## 5 / 9

But before we do that, let's check the current status. Check out the story/hare-and-tortoise branch and inspect the files in it.
How many commits do you see in the current branch?

```
sarah (master)$ git checkout story/hare-and-tortoise
Switched to branch 'story/hare-and-tortoise'
sarah (story/hare-and-tortoise)$ git log
commit 93ff5b0bddc24d271bf53ae74a0563f3a759eefc (HEAD -> story/hare-and-tortoise)
Author: sarah <sarah@example.com>
Date:   Sun Jul 13 11:30:53 2025 +0000

    Add first draft of hare-and-tortoise story

commit 9df9acbf877d03bfa811a97c82980ebd50ad5ae6
Author: sarah <sarah@example.com>
Date:   Sun Jul 13 11:30:53 2025 +0000

    Added the story index file

commit 88348f90f55dcbbb14e3781612d7081323f7dbd6 (story/frogs-and-ox)
Author: sarah <sarah@example.com>
Date:   Sun Jul 13 11:30:52 2025 +0000

    Completed frogs-and-ox story

commit 837dcbec976fcbe5e5252807deda6eb302c6bb6f
Author: sarah <sarah@example.com>
Date:   Sun Jul 13 11:30:52 2025 +0000

    Add incomplete frogs-and-ox story

commit 418106110d603b7b703740fc5b64b797130a11c5
Author: sarah <sarah@example.com>
Date:   Sun Jul 13 11:30:52 2025 +0000

    Added the lion and mouse story
```

right answer - "5"

## 6 / 9

Let's rebase the story/hare-and-tortoise branch on top of master.
Checkout the story/hare-and-tortoise branch first and then rebase master.
Run the command git rebase master
Check commit

```
sarah (story/hare-and-tortoise)$ git rebase master
Successfully rebased and updated refs/heads/story/hare-and-tortoise.
```

## 7 / 9

Awesome! Check the stories and the index file now. It should be up to date with all changes and the git log command should now include the commits from the others users as well.

```
sarah (story/hare-and-tortoise)$ git log
commit 8e8f529b2fb30fa3c9ea7dc3f4d7fce5c6376c3c (HEAD -> story/hare-and-tortoise)
Author: sarah <sarah@example.com>
Date:   Sun Jul 13 11:30:53 2025 +0000

    Add first draft of hare-and-tortoise story

commit 7f78941a4f40309019ff8794f56b1483add36317 (master)
Merge: 9df9acb 77e0d91
Author: sarah <sarah@example.com>
Date:   Sun Jul 13 11:39:49 2025 +0000

    Merge branch 'master' of http://git.example.com/sarah/story-blog

commit 77e0d913059f93d6c35eeba4ac4096414c9c05b0 (origin/master)
Author: tom <tom@example.com>
Date:   Sun Jul 13 11:30:54 2025 +0000

    Added the wolf and goat story

commit 9df9acbf877d03bfa811a97c82980ebd50ad5ae6
Author: sarah <sarah@example.com>
Date:   Sun Jul 13 11:30:53 2025 +0000
```

да там ранее их много

## 8 / 9

Sarah continues to update her story. Check the new commits on story/hare-and-tortoise.

```
sarah (story/hare-and-tortoise)$ git log
commit 1025420aaa3f05de19f375b6555e3655b8e67ba3 (HEAD -> story/hare-and-tortoise)
Author: sarah <sarah@example.com>
Date:   Sun Jul 13 11:44:08 2025 +0000

    Finish hare-and-tortoise
```

да в предыдущем начали черновик а теперь закончили интереснейшую историю

## 9 / 9

However she does not want multiple commits for the same story. She would like to squash all the commits into a single commit.

Run the command git rebase -i HEAD~3 to squash the last 3 commits into 1.
In the editor that opens, leave the first line as is, and change the second and third lines to use squash instead of pick. Then save the file. This way we pick the first commit and then squash the second and third commits to it.
In the next editor window that opens set the commit message to Add hare-and-tortoise story and save it.
Check commit

```
sarah (story/hare-and-tortoise)$ git rebase -i HEAD~3
```
```
pick 8e8f529 Add first draft of hare-and-tortoise story
squash efacfbe Update hare-and-tortoise
squash 1025420 Finish hare-and-tortoise

# Rebase 7f78941..1025420 onto 7f78941 (3 commands)
#
# Commands:
# p, pick <commit> = use commit
# r, reword <commit> = use commit, but edit the commit message
# e, edit <commit> = use commit, but stop for amending
# s, squash <commit> = use commit, but meld into previous commit
# f, fixup [-C | -c] <commit> = like "squash" but keep only the previous
#                    commit's log message, unless -C is used, in which case
#                    keep only this commit's message; -c is same as -C but
#                    opens the editor
# x, exec <command> = run command (the rest of the line) using shell
# b, break = stop here (continue rebase later with 'git rebase --continue')
# d, drop <commit> = remove commit
# l, label <label> = label current HEAD with a name
# t, reset <label> = reset HEAD to a label
# m, merge [-C <commit> | -c <commit>] <label> [# <oneline>]
# .       create a merge commit using the original merge commit's
# .       message (or the oneline, if no original merge commit was
# .       specified); use -c <commit> to reword the commit message
#
# These lines can be re-ordered; they are executed from top to bottom.
#
# If you remove a line here THAT COMMIT WILL BE LOST.
#
# However, if you remove everything, the rebase will be aborted.
#

# This is a combination of 3 commits.
# This is the 1st commit message:

Add hare-and-tortoise story               
                                
# This is the commit message #2:
                        
Update hare-and-tortoise
                                
# This is the commit message #3:
                        
Finish hare-and-tortoise
                                                                  
# Please enter the commit message for your changes. Lines starting 
# with '#' will be ignored, and an empty message aborts the commit.
#                                          
# Date:      Sun Jul 13 11:30:53 2025 +0000
#                                             
# interactive rebase in progress; onto 7f78941
# Last commands done (3 commands done):     
#    squash efacfbe Update hare-and-tortoise
#    squash 1025420 Finish hare-and-tortoise
# No commands remaining.                                                   
# You are currently rebasing branch 'story/hare-and-tortoise' on '7f78941'.
#                         
# Changes to be committed:               
#       new file:   hare-and-tortoise.txt
```
```
[detached HEAD c90134c] Add hare-and-tortoise story
 Date: Sun Jul 13 11:30:53 2025 +0000
 1 file changed, 20 insertions(+)
 create mode 100644 hare-and-tortoise.txt
Successfully rebased and updated refs/heads/story/hare-and-tortoise.
```


