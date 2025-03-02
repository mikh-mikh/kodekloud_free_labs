# kodekloud free labs git - git branches

Don't just think, do.

– Horace

## 1 / 16
What is a branch in git?

right answer - "pointer to a specific commit in git"

## 2 / 16
What is the default branch of a git repository?

right answer - "master"

## 3 / 16
Sarah has been working on a git repo at /home/sarah/story-blog and has written a short story. 
Check git log command output in that directory to see the activity.
What's the name of the file created by Sarah?

```
sarah (master)$ git log --name-status
commit 7a07ea398b37fe442c21a24a7d428a5b7394c592 (HEAD -> master)
Author: sarah <sarah@example.com>
Date:   Sun Mar 2 18:21:57 2025 +0000

    Added the lion and mouse story

A       lion-and-mouse.txt
```
мама теперь я знаю то что забуду через день

right answer - "lion-and-mouse.txt"

## 4 / 16
To which branch is the 🦁 lion-and-mouse.txt 🐭 file committed to in the git repository?

right answer - "master"

## 5 / 16
Sarah decides to write a new story - 🐸 The Frogs and Ox 🐂. Let's create and checkout a new branch named story/frogs-and-ox

```
sarah (master)$ git checkout -b story/frogs-and-ox
Switched to a new branch 'story/frogs-and-ox'
```

## 6 / 16
View the output of the git log command and identify the branch to which HEAD is pointing to now.

да тут в шелле он показывается в скобочках, мы этот бренч создали и переключились на него в прошлом шаге

```
sarah (story/frogs-and-ox)$ git log
commit 7a07ea398b37fe442c21a24a7d428a5b7394c592 (HEAD -> story/frogs-and-ox, master)
Author: sarah <sarah@example.com>
Date:   Sun Mar 2 18:21:57 2025 +0000

    Added the lion and mouse story
```	

right answer - "story/frogs-and-ox"

## 7 / 16
As you can see the HEAD always points to the last commit on the currently checked-out branch.

## 8 / 16
Sarah is half way through the 🐸 Frogs and Ox 🐂 story. It's not complete yet.
View the story she has written in the file frogs-and-ox.txt

```
sarah (story/frogs-and-ox)$ cat frogs-and-ox.txt 
--------------------------------------------
      THE FROGS AND THE OX
--------------------------------------------

An Ox came down to a reedy pool to drink. As he splashed heavily into the water, he crushed a young Frog into the mud.

The old Frog soon missed the little one and asked his brothers and sisters what had become of him.

"A great big monster," said one of them, "stepped on little brother with one of his huge feet!"

"Big, was he!" said the old Frog, puffing herself up. "Was he as big as this?"

"Oh, much ....
```

ЛЯГУШКА

## 9 / 16
Max informs Sarah that in her first story there's a typo in the title and needs to be fixed ASAP!
We must go back and fix the story in the master branch. But before we do that, let's commit the 
new story we have written so far. We don't want to carry our incomplete story to the master branch.
Stage and commit the story with the message Add incomplete frogs-and-ox story

```
sarah (story/frogs-and-ox)$ git status
On branch story/frogs-and-ox
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        frogs-and-ox.txt

nothing added to commit but untracked files present (use "git add" to track)
sarah (story/frogs-and-ox)$ git add .
sarah (story/frogs-and-ox)$ git commit -m "Add incomplete frogs-and-ox story"
[story/frogs-and-ox 0d48a67] Add incomplete frogs-and-ox story
 1 file changed, 13 insertions(+)
 create mode 100644 frogs-and-ox.txt
```

## 10 / 16
Now checkout the master branch.

```
sarah (story/frogs-and-ox)$ git checkout master
Switched to branch 'master'
sarah (master)$
```

## 11 / 16

Let's fix the typo in the lion-and-mouse.txt file. LION 🦁 is mis-spelt as LIOON. Please fix it and then commit the changes.
Commit message: Fix typo in story title

```
sarah (master)$ sed -i -e 's/LIOON/LION/g' lion-and-mouse.txt 
sarah (master)$ cat lion-and-mouse.txt | grep LIOON
sarah (master)$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   lion-and-mouse.txt

no changes added to commit (use "git add" and/or "git commit -a")
sarah (master)$ git add .
sarah (master)$ git commit -m "Fix typo in story title"
[master 87f11d4] Fix typo in story title
 1 file changed, 1 insertion(+), 1 deletion(-)
```

## 12 / 16
Great! Now that it's out of the way, let's finish the 🐸 frogs-and-ox 🐂 story. Switch back to the story/frogs-and-ox branch.

```
sarah (master)$ git checkout story/frogs-and-ox
Switched to branch 'story/frogs-and-ox'
```

## 13 / 16
Sarah has now finished her story. Check the changes and commit them with the message Completed frogs-and-ox story

```
--------------------------------------------
      THE LIOON AND THE MOUSE
--------------------------------------------

A Lion lay asleep in the forest, his great head resting on his paws.

A timid little Mouse came upon him unexpectedly, and in her fright and haste to get away, ran across the Lion's nose.

Roused from his nap, the Lion laid his huge paw angrily on the tiny creature to kill her.

"Spare me!" begged the poor Mouse. "Please let me go and some day I will surely repay you."

The Lion was much amused to think that a Mouse could ever help him. But he was generous and finally let the Mouse go.

Some days later, while stalking his prey in the forest, the Lion was caught in the toils of a hunter's net.

Unable to free himself, he filled the forest with his angry roaring.

The Mouse knew the voice and quickly found the Lion struggling in the net.

Running to one of the great ropes that bound him, she gnawed it until it parted, and soon the Lion was free.

"You laughed when I said I would repay you," said the Mouse. "Now you see that even a Mouse can help a Lion."sarah (story/frogs-and-ox)$ cat 
.git/               frogs-and-ox.txt    lion-and-mouse.txt  
sarah (story/frogs-and-ox)$ cat frogs-and-ox.txt 
--------------------------------------------
      THE FROGS AND THE OX
--------------------------------------------

An Ox came down to a reedy pool to drink. As he splashed heavily into the water, he crushed a young Frog into the mud.

The old Frog soon missed the little one and asked his brothers and sisters what had become of him.

"A great big monster," said one of them, "stepped on little brother with one of his huge feet!"

"Big, was he!" said the old Frog, puffing herself up. "Was he as big as this?"

"Oh, much bigger!" they cried.

The Frog puffed up still more.

"He could not have been bigger than this," she said.

But the little Frogs all declared that the monster was much, much bigger and the old Frog kept puffing herself out more and more until, all at once, she burst.sarah (story/frogs-and-ox)$ git add .
sarah (story/frogs-and-ox)$ git commit -m "Completed frogs-and-ox story"
[story/frogs-and-ox 53f373f] Completed frogs-and-ox story
 1 file changed, 7 insertions(+), 1 deletion(-)
```
хаха а льва в этой ветке не поправили он некий LIOON так и остался

## 14 / 16

A new git repository is created at the path /home/sarah/website for hosting the story website.
Count the number of branches available in that repository including the master branch.

```
sarah (story/frogs-and-ox)$ cd ../website/
sarah (master)$ git branch
  feature/cart
  feature/checkout
  feature/signout
  feature/signup
* master
```

right answer - "5"

## 15 / 16

Looking at the commit history, try to guess what branch was the feature/signout branch created from?
Checkout branch feature/signout and then use the command git log --graph --decorate to see previous 
commit history along with the branch they were committed on.

```
sarah (master)$ git checkout feature/signout
Switched to branch 'feature/signout'
sarah (feature/signout)$ git log --graph --decorate
* commit 2dd482005cb1f15c76f9d8e08e0a76cdb278e4fb (HEAD -> feature/signout)
| Author: sarah <sarah@example.com>
| Date:   Sun Mar 2 18:21:57 2025 +0000
| 
|     Add signout page
| 
* commit 23fd88387415a8dce5bf5960577f524fb8f2d279 (feature/signup)
| Author: sarah <sarah@example.com>
| Date:   Sun Mar 2 18:21:57 2025 +0000
| 
|     Add signup page
| 
* commit 9de914501d5b148a6d85157da3a4b7b7f112e292 (master)
  Author: sarah <sarah@example.com>
  Date:   Sun Mar 2 18:21:57 2025 +0000
  
      Added main page
```

right answer - feature/signup"

## Here's a fun one! Looking at the commit history of all branches, what's the best graphical representation of the branches in this repository?

Checkout each branch and then use the command git log --graph --decorate to see previous branch.

```
feature/signout        feature/checkout
       |                      |
feature/signup         feature/cart
             \         /
               master	 
```

right answer - "D"

			   









