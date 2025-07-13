To master a new technology, you will have to play with it.

– Jordan Peterson

## 1 / 9

Let's proceed with where we left off in the previous lab. Sarah's local repository should be available at /home/sarah/story-blog
How many stories are currently available in the master branch?

```
sarah $ cd story-blog/ && git branch
  master
* story/frogs-and-ox
sarah (story/frogs-and-ox)$
sarah (story/frogs-and-ox)$ git checkout master
Switched to branch 'master'
sarah (master)$ ls
lion-and-mouse.txt
```

right answer - "1"

## 2 / 9
What's the name of the story in the master branch?

right answer - "The Lion and the Mouse"

## 3 / 9
How many branches does the repository currently have?

right answer - "2"

## 4 / 9

The new story Sarah wrote is in the story/frogs-and-ox branch. It's time to merge the branch and bring it to the master branch.
But before that look at the log of the master and story/frogs-and-ox branches and identify how many commits there have been in the past on each branch.

```
sarah (master)$ git checkout story/frogs-and-ox
Switched to branch 'story/frogs-and-ox'
sarah (story/frogs-and-ox)$ git log
commit 399781b31c61fee3ec07b62bb70dd768eaf63dc6 (HEAD -> story/frogs-and-ox)
Author: sarah <sarah@example.com>
Date:   Sun Jul 13 10:17:42 2025 +0000

    Completed frogs-and-ox story

commit b75dac408e7f69e86a8ebd20dc7ae9270d605ae2
Author: sarah <sarah@example.com>
Date:   Sun Jul 13 10:17:42 2025 +0000

    Add incomplete frogs-and-ox story

commit 8d83675be4fdf42525369e74bd63d9efd1303d6e
Author: sarah <sarah@example.com>
Date:   Sun Jul 13 10:17:42 2025 +0000

    Added the lion and mouse story
sarah (story/frogs-and-ox)$ git checkout master
Switched to branch 'master'
sarah (master)$ git log
commit 692d3befcccd8cedb2bbaf8c101cf6c9000dc0b2 (HEAD -> master)
Author: sarah <sarah@example.com>
Date:   Sun Jul 13 10:17:42 2025 +0000

    Fix typo in story title

commit 8d83675be4fdf42525369e74bd63d9efd1303d6e
Author: sarah <sarah@example.com>
Date:   Sun Jul 13 10:17:42 2025 +0000

    Added the lion and mouse story
```
	
right answer - "msater 2 commits \ story/frogs-and-ox 3 commits"

## 5 / 9

Correct! First sarah committed the 🦁 Lion and Mouse 🐭 story in the master branch and then created a new branch for the 🐸 Frogs and ox 🐂 story, 
then went back and fixed typo in the 🦁 Lion and Mouse 🐭 story and then went back and finished the 🐸 Frogs and ox 🐂 story.
Next we will merge the new story into the master to have all stories in the master branch.

## 6 / 9

While in the master branch merge the story/frogs-and-ox branch. If prompted for a commit message leave it to the default and quit the editor.
Check merge

```
sarah (master)$ git merge story/frogs-and-ox
Merge made by the 'recursive' strategy.
 frogs-and-ox.txt | 19 +++++++++++++++++++
 1 file changed, 19 insertions(+)
 create mode 100644 frogs-and-ox.txt
 sarah (master)$ git log
commit 7065f5ce181ca06398f4b25f4ed283502af38e6f (HEAD -> master)
Merge: 692d3be 399781b
Author: sarah <sarah@example.com>
Date:   Sun Jul 13 10:29:44 2025 +0000

    Merge branch 'story/frogs-and-ox'

commit 692d3befcccd8cedb2bbaf8c101cf6c9000dc0b2
Author: sarah <sarah@example.com>
Date:   Sun Jul 13 10:17:42 2025 +0000

    Fix typo in story title

commit 399781b31c61fee3ec07b62bb70dd768eaf63dc6 (story/frogs-and-ox)
Author: sarah <sarah@example.com>
Date:   Sun Jul 13 10:17:42 2025 +0000

    Completed frogs-and-ox story

commit 8d83675be4fdf42525369e74bd63d9efd1303d6e
Author: sarah <sarah@example.com>
Date:   Sun Jul 13 10:17:42 2025 +0000

    Added the lion and mouse story

commit b75dac408e7f69e86a8ebd20dc7ae9270d605ae2
Author: sarah <sarah@example.com>
Date:   Sun Jul 13 10:17:42 2025 +0000

    Add incomplete frogs-and-ox story
```

## 	7 / 9
Check the log of the master branch and see how many commits are seen now

right answer - "5"

## 8 / 9

Git merged all the commits we made in the story/frogs-and-ox branch to the master branch. 
But since we made an additional commit on the master (fixing the typo from LIOON to LION) git created a new merge commit

## 9 / 9

List the files in the master branch and make sure both the stories are visible.

```
sarah (master)$ ls
frogs-and-ox.txt    lion-and-mouse.txt
```

