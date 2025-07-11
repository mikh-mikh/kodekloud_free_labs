# 
Success doesn't come from what you do occasionally. It comes from what you do consistently.

– Marie Forleo

## 1 / 13

We have initialised git repo in /home/sarah/story-blog. Check git log command output in that directory
Simply run cd /home/sarah/story-blog; git log
As we haven't commited any file yet it should show message fatal: your current branch 'master' does not have any commits yet . So lets commit some file in next step.

```
sarah $ cd story-blog/ && git log
fatal: your current branch 'master' does not have any commits yet
```

## 2 / 13

Sarah has written a story lion-and-mouse.txt under /home/sarah/story-blog/. Please commit it to local git repo
Add commit message: Added the lion and mouse story

Verify file committed

```
sarah $ git add . && git commit -m "Added the lion and mouse story"
[master (root-commit) 0903c30] Added the lion and mouse story
 1 file changed, 23 insertions(+)
 create mode 100644 lion-and-mouse.txt
```

## 3 / 13

We have committed lion-and-mouse.txt file in git repo /home/sarah/story-blog. Check git log command output in that directory
Based on the output of the command please answer the next questions

```
sarah (master)$ git log
commit 0903c30926eab3327ba33df5f4ec4af6e72cef47 (HEAD -> master)
Author: sarah <sarah@example.com>
Date:   Thu Jul 10 14:55:30 2025 +0000

    Added the lion and mouse story
```

## 4 / 13

Which info is not displayed in git log?

right answer - "list of changed files"

## 5 / 13

You can list the changed files as well using the --name-only option with the git log command
Run the command git log --name-only	

```
sarah (master)$ git log --name-only
commit 0903c30926eab3327ba33df5f4ec4af6e72cef47 (HEAD -> master)
Author: sarah <sarah@example.com>
Date:   Thu Jul 10 14:55:30 2025 +0000

    Added the lion and mouse story

lion-and-mouse.txt
```

## 6 / 13

Which branch has the changes been committed to?
Branch info can be seen in first line of git log output where (HEAD -> {BRANCH_NAME} ) is displayed.

right answer - "masster"

## 7 / 13
Who is the Author of the commit in git repo?

right answer - "sarah"

## 8 / 13
Another user has committed a new file to the repository now. Identify the user and the new file that was added.

Commit message: Added a new story.

Use the --name-only option to view the files as well

```
sarah (master)$ git log --name-only
commit aaf6f607a7bec1ba3cd71d629819f23146c2e891 (HEAD -> master)
Author: tom <tom@example.com>
Date:   Thu Jul 10 14:59:39 2025 +0000

    Added a new story

frogs-and-ox.txt

commit 0903c30926eab3327ba33df5f4ec4af6e72cef47
Author: sarah <sarah@example.com>
Date:   Thu Jul 10 14:55:30 2025 +0000

    Added the lion and mouse story

lion-and-mouse.txt
```

как то можно вывод наерное делать по коммиту или ещё какому либо признаку но мне конкретно сегодня влом

right answer - "Tom added frogs-and-ox.txt"

## 9 / 13

What is the option for git log command to display the logs in compact way (one log per line)?
If not sure try each one.

```
sarah (master)$ git log --oneline
aaf6f60 (HEAD -> master) Added a new story
0903c30 Added the lion and mouse story
```

right answer - "--oneline"

## 10 / 13

Another git repository that hosts code of an e-commerce application is available at /home/sarah/learning-app-ecommerce.
Explore the repository, check the files, git status, log etc.

```
sarah (master)$ cd ../learning-app-ecommerce/
sarah (master)$ git status
On branch master
Your branch is ahead of 'origin/master' by 3 commits.
  (use "git push" to publish your local commits)

nothing to commit, working tree clean
```

## 11 / 13

The repository has many commits. Can you try to list the last 3 commits alone?
There should be an option in git log to limit the list of outputs. Use git help log. Check hint if not sure.

```
sarah (master)$ git log -n 3
commit acf39b772a0ff5ca1bfaaca260450aacedfddd23 (HEAD -> master)
Author: tej <tej@example.com>
Date:   Thu Jul 10 14:53:19 2025 +0000

    Update color from red to green

commit ad9b6f95f4326987b9a4feffb3a279ba5ce33b4d
Author: sarah <sarah@example.com>
Date:   Thu Jul 10 14:53:19 2025 +0000

    Add instructions to verify application

commit 3a7fa5111f60329957108688f3ec5ea787982949
Author: max <max@example.com>
Date:   Thu Jul 10 14:53:19 2025 +0000

    Increase interval time to 500
```

## 12 / 13
Identify who made the latest commit in the new repository.

right anwser - "Tej"

## 13 / 13

Judging by their actions, can you guess who may be the javascript developer in the team?
Look at the logs and identify the person who made changes to the .js file recently. You have already learned the option to display files associated with a commit

```
sarah (master)$ git log --name-only --all -- '*.js'
commit 3a7fa5111f60329957108688f3ec5ea787982949
Author: max <max@example.com>
Date:   Thu Jul 10 14:53:19 2025 +0000

    Increase interval time to 500

js/theme.js

commit 8f2fe8f2a5b3c91bfd7817ddd7b769a8590de1a1
Author: mmumshad <mmumshad@gmail.com>
Date:   Wed Oct 2 14:48:58 2019 +0800

    First commit

js/bootstrap.min.js
js/jquery-1.12.4.min.js
js/min/emran.min.js
js/min/theme.min.js
js/theme.js
vendors/Counter-Up/jquery.counterup.min.js
vendors/Counter-Up/waypoints.min.js
vendors/jQuery_ui/jquery-ui.min.js
vendors/lightbox/js/lightbox.js
vendors/owl_carousel/owl.carousel.min.js
vendors/stellar/jquery.stellar.js
vendors/wow-js/wow.min.js
```

right answer - "Max" 

(because Mmumshad is only adding files - Max is developer because his commit is "Increase interval time to 500"

 







	