#
You can’t go back and change the beginning, but you can start where you are and change the ending.

– C.S. Lewis

## 1 / 16
What is a branch in git?

right answer - "pointer to specific commit"

## 1 / 16
What is a branch in git?

right answer - "master"

## 3 / 16
Sarah has been working on a git repo at /home/sarah/story-blog and has written a short story. Check git log command output in that directory to see the activity.

What's the name of the file created by Sarah?

```
sarah (master)$ git log --name-only
commit f3b3c5d813cbeae7243d41f881a6b9a6b8287693 (HEAD -> master)
Author: sarah <sarah@example.com>
Date:   Fri Jul 11 15:13:51 2025 +0000

    Added the lion and mouse story

lion-and-mouse.txt
```

right answer - "lion-and-mouse.txt"

## 4 / 16
To which branch is the 🦁 lion-and-mouse.txt 🐭 file committed to in the git repository?

right answer - "master"

## 5 / 16

Sarah decides to write a new story - 🐸 The Frogs and Ox 🐂. Let's create and checkout a new branch named story/frogs-and-ox
Verify branch

```
sarah (master)$ git checkout -b "story/frogs-and-ox"
Switched to a new branch 'story/frogs-and-ox'
sarah (story/frogs-and-ox)$
```

## 6 / 16
View the output of the git log command and identify the branch to which HEAD is pointing to now.

```
sarah (story/frogs-and-ox)$ git log
commit f3b3c5d813cbeae7243d41f881a6b9a6b8287693 (HEAD -> story/frogs-and-ox, master)
Author: sarah <sarah@example.com>
Date:   Fri Jul 11 15:13:51 2025 +0000

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

ничего не понятно - но очень интересно

## 9 / 16

Max informs Sarah that in her first story there's a typo in the title and needs to be fixed ASAP!
We must go back and fix the story in the master branch. But before we do that, let's commit the new story we have written so far. We don't want to carry our incomplete story to the master branch.
Stage and commit the story with the message Add incomplete frogs-and-ox story

Verify commit

```
sarah (story/frogs-and-ox)$ git add . && git commit -m "Add incomplete frogs-and-ox story"
[story/frogs-and-ox 64bed0e] Add incomplete frogs-and-ox story
 1 file changed, 13 insertions(+)
 create mode 100644 frogs-and-ox.txt
```

## 10 / 16

Now checkout the master branch.
Verify branch 

```
sarah (story/frogs-and-ox)$ git checkout master
Switched to branch 'master'
sarah (master)$
```

## 11 / 16

Let's fix the typo in the lion-and-mouse.txt file. LION 🦁 is mis-spelt as LIOON. Please fix it and then commit the changes.
Commit message: Fix typo in story title
Verify fix and commit

```
sarah (master)$ sed -i 's/LIOON/LION/g' lion-and-mouse.txt
sarah (master)$ git add .
sarah (master)$ git commit -m "Fix typo in story title"
[master 4dace35] Fix typo in story title
 1 file changed, 1 insertion(+), 1 deletion(-)
```

## 12 / 16

Great! Now that it's out of the way, let's finish the 🐸 frogs-and-ox 🐂 story. Switch back to the story/frogs-and-ox branch.
Verify branch

```
sarah (master)$ git checkout story/frogs-and-ox
Switched to branch 'story/frogs-and-ox'
sarah (story/frogs-and-ox)$
```

## 13 / 16
Sarah has now finished her story. Check the changes and commit them with the message Completed frogs-and-ox story

```
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

But the little Frogs all declared that the monster was much, much bigger and the old Frog kept puffing herself out more and more until, all at once, she burst.

sarah (story/frogs-and-ox)$ git add . && git commit -m "Completed frogs-and-ox story"

[story/frogs-and-ox d3f0519] Completed frogs-and-ox story
 1 file changed, 7 insertions(+), 1 deletion(-)
sarah (story/frogs-and-ox)$
```

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
sarah (master)$ git branch | wc -l
5
sarah (master)$
```

right answer - "5"

## 15 / 16

Looking at the commit history, try to guess what branch was the feature/signout branch created from?
Checkout branch feature/signout and then use the command git log --graph --decorate to see previous commit history along with the branch they were committed on

```
sarah (feature/signout)$ git log --graph --decorate
* commit c8136c0262285747ec2147aec29af12159c0bc2e (HEAD -> feature/signout)
| Author: sarah <sarah@example.com>
| Date:   Fri Jul 11 15:13:51 2025 +0000
| 
|     Add signout page
| 
* commit f906f2de8cf8a8f9be25cf9b4bd090c10aaa1f69 (feature/signup)
| Author: sarah <sarah@example.com>
| Date:   Fri Jul 11 15:13:51 2025 +0000
| 
|     Add signup page
| 
* commit bfb287f406a4eed78b6d3eb1c316a1020abfc0f2 (master)
  Author: sarah <sarah@example.com>
  Date:   Fri Jul 11 15:13:51 2025 +0000
  
      Added main page
```

right answer - "feature/signup"

## 16 / 16

Here's a fun one! Looking at the commit history of all branches, what's the best graphical representation of the branches in this repository?

Checkout each branch and then use the command git log --graph --decorate to see previous branch.


не успел:)