# kodekloud free labs git - initialize repository

The secret of success is to do the common things uncommonly well.

– John D. Rockefeller

## 1 / 21
What is the command to initialize a git repository?

right answer - git init

## 2 / 21

Initialize a git repository at /home/sarah/story-blog
Create directory if it doesn't already exist.

```
sarah $ git init /home/sarah/story-blog
hint: Using 'master' as the name for the initial branch. This default branch name
hint: is subject to change. To configure the initial branch name to use in all
hint: of your new repositories, which will suppress this warning, call:
hint: 
hint:   git config --global init.defaultBranch <name>
hint: 
hint: Names commonly chosen instead of 'master' are 'main', 'trunk' and
hint: 'development'. The just-created branch can be renamed via this command:
hint: 
hint:   git branch -m <name>
Initialized empty Git repository in /home/sarah/story-blog/.git/
sarah $ ls -la
total 32
drwxr-sr-x    1 sarah    sarah         4096 Mar  2 10:51 .
drwxr-xr-x    1 root     root          4096 Nov  9  2021 ..
-rw-r--r--    1 sarah    sarah          202 Nov  9  2021 .bashrc
-rw-r--r--    1 sarah    sarah           50 Nov  9  2021 .vimrc
drwxr-sr-x   10 sarah    sarah         4096 Mar  2 10:50 learning-app-ecommerce
drwxr-sr-x    3 sarah    sarah         4096 Mar  2 10:51 story-blog
sarah $ cd story-blog/
sarah $ git status
On branch master

No commits yet

nothing to commit (create/copy files and use "git add" to track)
```

директория сама создалась

## 3 / 21

Which hidden folder gets created after initializing a git repository?
Explore the repository created in the previous step

right answer - .git

## 4 / 21

Let's test some of the concepts we learned so far in our lectures.
Once a git repository has been initialized, which stage contains the active changes in your local git repository?

right answer - working area

## 5 / 21

Let’s add a file to our project inside /home/sarah/story-blog
File name: lion-and-mouse.txt
File content: A Lion lay asleep in the forest

```
sarah $ pwd
/home/sarah/story-blog
sarah $ echo "A Lion lay asleep in the forest" > lion-and-mouse.txt
```

## 6 / 21

Which stage contains new changes that will soon be committed to local git repo ?

right answer - staging area

## 7 / 21

Now that we've added a text file, let's see if git detected the change we made. Although we haven't done anything with git yet, 
we initialized a git repository in this project, so git is aware of all our files and changes.
You can see the status of git by executing the git status command.
Answer next few questions based on the git status command output.

```
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        lion-and-mouse.txt

nothing added to commit but untracked files present (use "git add" to track)
```

## 8 / 21
What commits are listed in the git repository?

right answer - No commits

## 9 / 21
What's the status of the lion-and-mouse.txt file in the repository?

right answer - untracked 

## 10 / 21
Which area of the local git repository is the lion-and-mouse.txt file in ?

right answer - working area	

## 11 / 21
Stage the file lion-and-mouse.txt to make it available for commit.

```
sarah $ git add .
sarah $ git status
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   lion-and-mouse.txt

```

## 12 / 21

Now, it's time to commit our change! A commit records the change in the repository compared to its previous state. 
But before that we must configure the git user who will be the owner of the commit.
Set git username as sarah and user email as sarah@example.com using the below commands.

```
git config user.email sarah@example.com
git config user.name sarah 
```

## 13 / 21

Let's commit our change! In this case, we didn't have any previous commits,
so the addition of the file lion-and-mouse.txt is a change compared to its previous state.
Commit the files that are currently in the staging area.
First check the status of the file using the command git status. Then commit using the commit message as Added the lion and mouse story

```
sarah $ git status
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   lion-and-mouse.txt

sarah $ git commit -m "Added the lion and mouse story"
[master (root-commit) e6d9cae] Added the lion and mouse story
 1 file changed, 1 insertion(+)
 create mode 100644 lion-and-mouse.txt
```

## 14 / 21

Sarah created a new file named notes.txt where she plans to write down ideas about the story for personal purposes.
She does not want git to track this file or share it with her team mates.
What is the current status of the notes.txt file? 

```
sarah (master)$ git status
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        notes.txt

nothing added to commit but untracked files present (use "git add" to track)
```

right answer - Untracked

## 15 / 21

It is good that the file is untracked. But it is still under GIT's radar. 
If you run the "git add ." command accidentally git will start to track this file.
Let's configure git to ignore this file permanently.

```
sarah (master)$ echo "notes.txt" >> .gitignore
sarah (master)$ git status
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        .gitignore

nothing added to commit but untracked files present (use "git add" to track)
```

## 16 / 21
What's the status of the file notes.txt now in the git status command's output.

right answer - Not listed at all

## 17 / 21
As you might have noticed the .gitignore file itself may be listed as untracked. It is a good practice to track the .gitignore file with git.

## 18 / 21

Let's explore another git repository. We have a repository used for the development of an application cloned at /home/sarah/learning-app-ecommerce.
Identify the state of the git repository. How many files are staged and how many are not?

```
sarah (master)$ cd ../learning-app-ecommerce/
sarah (master)$ git status
On branch master
Your branch is ahead of 'origin/master' by 1 commit.
  (use "git push" to publish your local commits)

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   README.md

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   js/theme.js
```

right answer - 1 staged 1 modified

## 19 / 21

You are asked to commit the README.md file with the commit message Add instructions for verification and the js/theme.js 
file with the message Increase time from 400 to 500
Note that the README.md file is already staged. So you just have to commit it. The file js/theme.js is to be committed as part of another commit.

```
sarah (master)$ git commit -m "Add instructions for verification"
[master 883a0b3] Add instructions for verification
 1 file changed, 1 insertion(+)
sarah (master)$ git add .
sarah (master)$ git commit -m "Increase time from 400 to 500"
[master c39643f] Increase time from 400 to 500
 1 file changed, 1 insertion(+), 1 deletion(-)
sarah (master)$ git status
On branch master
Your branch is ahead of 'origin/master' by 3 commits.
  (use "git push" to publish your local commits)

nothing to commit, working tree clean
```

## 20 / 21
What files are configured to be ignored by this repository?

```
sarah (master)$ cat .gitignore 
.DS_Store
.idea/
```

right answer - idea (?) странно, это скрытая директория которой нет, и был еще скрытый файл ".DS_Store" - наверное перепутали задания\среды

## 21 / 21

.idea/ is a directory created by the IntelliJ Idea IDE. 
These are personal to the user and we don't want these to be checked in to the git repository along with our code.

