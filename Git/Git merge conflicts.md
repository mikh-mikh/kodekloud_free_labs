
Practice as if you are the worst, Perform as if you are the best.

–

## 1 / 12

Max and Sarah have been contributing stories. And they are available on the remote repository.
Max's local repository has all the latest changes from the remote and is in sync with it. Check it out!
Note: You can Login to git UI with sarah user and password: Sarah_pass123

## 2 / 12

During a meeting the team decides to add an Index file to the repository named story-index.txt which would contain a list of all stories written.
It wasn't clear who would own this task, so Max decides to do it himself 💪 . He creates a file named story-index.txt and adds a list of stories to it. 
Check it out under the /home/max/story-blog directory.

```
max $ cd story-blog/ && ls
fox-and-grapes.txt  frogs-and-ox.txt    lion-and-mouse.txt  story-index.txt
max (master)$
```

## 3 / 12

Let's now stage and commit the story-index.txt file.
Use the message - Add index of stories
Check git commit

```
max (master)$ git branch
* master
max (master)$ git add . && git commit -m "^C
max (master)$ git status
On branch master
Your branch is up to date with 'origin/master'.

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        story-index.txt

nothing added to commit but untracked files present (use "git add" to track)
max (master)$ git add story-index.txt && git commit -m "Add index of stories"
[master b7951aa] Add index of stories
 1 file changed, 4 insertions(+)
 create mode 100644 story-index.txt
 ```
 
 ## 4 / 12
 
Let's now push the file to the remote repository.
Try with the git push origin master command, and select the response you get

```
max (master)$ git push origin master
To http://git.example.com/sarah/story-blog.git
 ! [rejected]        master -> master (fetch first)
error: failed to push some refs to 'http://git.example.com/sarah/story-blog.git'
hint: Updates were rejected because the remote contains work that you do
hint: not have locally. This is usually caused by another repository pushing
hint: to the same ref. You may want to first integrate the remote changes
hint: (e.g., 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
```

ну ясен ж перец - лабораторная называется "Слияние конфликтов"

right answer - "Rejected"

## 5 / 12

Read the error message and identify the cause of the failure.

right answer - "The remote contains work that you do not have locally"

Пуллить надо ёк-макарёк

## 6 / 12

Looks like someone has pushed changes to the remote that needs to be pulled first, before we can push any of our own changes to remote.
Pull the remote changes.
Check merge

```
max (master)$ git pull
remote: Enumerating objects: 4, done.
remote: Counting objects: 100% (4/4), done.
remote: Compressing objects: 100% (3/3), done.
remote: Total 3 (delta 1), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (3/3), 305 bytes | 305.00 KiB/s, done.
From http://git.example.com/sarah/story-blog
   fbd89ab..4ec3c5a  master     -> origin/master
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
Automatic merge failed; fix conflicts and then commit the result.
```

## 7 / 12

What was the result of the Pull operation?
Read the last 2 lines of the output of the git pull command.

right answer - "Merge Conflict"

## 8 / 12

We are now in a merge conflict! Looks like there was already a file named story-index.txt on remote. Someone beat us to it! Let's find out who.
Check the log of the origin/master branch to see what was the last commit on the repository and identify who added the story-index.txt file.

```
max (master)$ git log origin/master
commit 4ec3c5a16ef513d4112c200ba09c502c92e772f8 (origin/master, origin/HEAD)
Author: sarah <sarah@example.com>
Date:   Sun Jul 13 10:43:19 2025 +0000

    Added the index file

commit fbd89abe38ed44a28437c1ab6d16be21199281ce
Author: max <max@example.com>
Date:   Sun Jul 13 10:41:03 2025 +0000

    Added the fox and grapes story

commit 47ad333b7454e8b925f97aaa3c5dd044f8fe7c20
Merge: 1a678d5 1fd2716
Author: sarah <sarah@example.com>
Date:   Sun Jul 13 10:41:00 2025 +0000

    Merge branch 'story/frogs-and-ox'

commit 1a678d59bdf2d45246a23b832f9b96435c19ed2f
Author: sarah <sarah@example.com>
Date:   Sun Jul 13 10:41:00 2025 +0000

    Fix typo in story title

commit 1fd27166eccd1233178e8923ab393b4e3763f780
Author: sarah <sarah@example.com>
Date:   Sun Jul 13 10:41:00 2025 +0000

    Completed frogs-and-ox story

commit a50c195afbda3411d3bc552c887c354afcbf431a
Author: sarah <sarah@example.com>
Date:   Sun Jul 13 10:41:00 2025 +0000

    Added the lion and mouse story

commit 0268131d104f55f61141763bae68d4b5e2fc047a
Author: sarah <sarah@example.com>
Date:   Sun Jul 13 10:41:00 2025 +0000ry
```	

right answer - "Sarah" 

## 9 / 12

Looks like Sarah already pushed a version of the file. When we pulled latest changes, 
git tried to merge Max's and Sarah's versions of the story-index.txt file, but was unsuccessful. 
However the local story-index.txt file is updated with changes from both Max and Sarah to allow you to merge manually.

Inspect the file (use vi editor or just cat story-index.txt) and select the most appropriate statement below. 
The first section shows Max's data and the second section shows Sarah's data.

```
max (master)$ cat story-index.txt 
<<<<<<< HEAD
1. The Lion and the Mooose
2. The Frogs and the Ox
3. The Fox and the Grapes
4. The Donkey and the Dog
=======
1. The Lion and the Mouse
2. The Frogs and the Ox
3. The Fox and the Grapes
>>>>>>> 4ec3c5a16ef513d4112c200ba09c502c92e772f8
```

right answer - "Sarah 

## 10 / 12

Looks like both of them were partially wrong. Let's fix the file to remove the errors done by each of them. Let's manually merge changes from both users.
Update the contents of the file (use vi editor) to keep the correct version of the Lion and Mouse story and keep the Donkey and Dog story as well. Remove all the extra lines added by GIT
Check merge

story-index.txt:
```
1. The Lion and the Mouse
2. The Frogs and the Ox
3. The Fox and the Grapes
4. The Donkey and the Dog
```

## 11 / 12

Now that we have made a change, we must now commit it.
Commit the current changes with the message - Resolved merge conflicts and merged story index
Check git commit

```
max (master)$ git add . && git commit -m "Resolved merge conflicts and merged story index"
[master 8760fae] Resolved merge conflicts and merged story index
```

## Now that we have merged the changes, everything's clean ✨ . We can now push the changes to remote.
Check git push

```
max (master)$ git push
Enumerating objects: 9, done.
Counting objects: 100% (9/9), done.
Delta compression using up to 16 threads
Compressing objects: 100% (6/6), done.
Writing objects: 100% (6/6), 628 bytes | 628.00 KiB/s, done.
Total 6 (delta 3), reused 0 (delta 0), pack-reused 0
remote: . Processing 1 references
remote: Processed 1 references in total
To http://git.example.com/sarah/story-blog.git
   4ec3c5a..8760fae  master -> master
```

мы запулили, исправили конфликт и запушили свое + исправленное из запуленного
мне стремно - но я не допер до тонкостей механизма   