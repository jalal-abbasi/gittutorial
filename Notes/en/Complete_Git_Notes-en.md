Github Onramp course by Jadi: Summary of the notes and commands

# Table of Contents
  - [Initializing a Git Project](#Initializing-a-Git-Project)
  - [Checking Git Status](#Checking-Git-Status)
  - [Adding Files to the Staging Area](#Adding-Files-to-the-Staging-Area)
  - [Removing a file from the local repository](#Removing-a-file-from-the-local-repository)
  - [Committing Changes](#Committing-Changes)
  - [Viewing Differences](#Viewing-Differences)
  - [Reseting and Exiting the Staging Area](#Reseting-and-Exiting-the-Staging-Area)
  - [Restoring Files](#Restoring-Files)
  - [Working With Branches](#Working-With-Branches)
  - [Cloning a Remote Repository](#Cloning-a-Remote-Repository)
  - [Adding a Remote Repository](#Adding-a-Remote-Repository)
  - [Tagging](#tagging)
  - [GPG Keys and Signing](#gpg-keys-and-signing)
  - [Debugging Using Git](#debugging-using-git)
  - [Forking and Pull (Merge) Request](#forking-and-pull-merge-request)
  - [Other Git Commands](#other-git-commands)
  - [Unix-Specific Commands](#unix-specific-commands)


# Initializing a Git Project

  A repository (or repo) in Git is a storage location where your project's files, along with their entire version history, are stored. It tracks all changes, allowing you to collaborate, revert, and manage versions effectively.

  To start a new Git repository for your project, use the following command:
  ```
  git init
  ```
  - It creates a hidden .git folder, which stores all the repository’s
  metadata (branches, commits, configurations, etc.).
  - Used when starting a new project or making an existing directory a Git
  repository.

# Checking Git Status

  **The 4 Storage Layers in Git**
  | **Level** | **Where It Lives** | **Purpose** |
  |----|----|----|
  | **Working Directory** | Your actual files | Where you edit code |
  | **Staging Area (index)** | .git/index | Prepares specific changes for commit |
  | **Commit History** | .git/objects/ | Saves permanent snapshots of code |
  | **Remote (Push)** | GitHub, GitLab, etc. | Shares commits with others |

  - To view the current status of your local repository:
    ```
    git status
    ```
   - Tells you which files are modified, staged, or untracked and helps you understand what changes need to be committed.
  
  - To show the log (history) of all the commits you have made:
    ```
    git log
    ```
  - To see the content of a specific commit:
    ```
    git show <commit-hash-string>
    ```

# Adding Files to the Staging Area

  To add files to the staging area to prepare them for commit. You have several options:

  - To add all (the changed) files:
    ```
    git add -A
    ```
  
  - To add specific file types, e.g., all HTML files:
    ```
    git add "*.html"
    ```

  - To add a specific file :
    ```
    git add <file>
    ```

  - To add more than one file at the same time:
    ```
    git add “file1.txt” “file2.txt”
    ```

  - To add any file that has "hello" in its name:
    ```
    git add “hello*”
    ```

# Removing a file from the local repository
  - To remove a file from Git and your project, use:
    ```
    git rm 'file-name'
    ```

  - To remove a folder from the local repository and git:
    ```
    git rm -r 'folder-name'
    ```
    
  - To remove a folder from only git tracking (keeping it in the local repo):
    ```
    git rm -r --cached 'folder-name'
    ```
    - -r: Recursively removes directories and their contents from Git tracking. The term "recursive" means Git goes inside the folder        and applies the command to all its contents, like subfolders and files.
    - --cached: Removes the file(s) from the Git index (staging area) but keeps them in your local filesystem.
      
# Committing Changes

  To save the staged changes as a new snapshot, use the `git commit` command:
  ```
  git commit -m "Your comment about the changes"
  ```
  - `git commit`: You can also write this command (without adding -m "comment") and insert your comment in the editor. 
  - Always include a comment with your commit.

# Viewing Differences

  Git provides several ways to view differences:

  - To see the differences between the unstaged changes vs. the latest commit (HEAD) \> Shows **unstaged** modifications.
    ```
    git diff HEAD
    ```
    - HEAD: is a special pointer that refers to the current branch's latest commit. However, the location of this pointer can be changed to any commit you want. 

  - To see the differences between staged changes vs. latest commit (HEAD) \> Shows **staged** modifications.
    ```
    git diff --staged
    ```

  Example:

  I make one change in the pag1.html, then add it to the stage, then make another change, without adding:

  <table>
  <colgroup>
  <col style="width: 50%" />
  <col style="width: 50%" />
  </colgroup>
  <thead>
  <tr>
  <th style="text-align: center;">$ git diff HEAD</th>
  <th style="text-align: center;">$ git diff --staged</th>
  </tr>
  </thead>
  <tbody>
  <tr>
  <th><p><strong>diff --git a/page1.html b/page1.html</strong></p>
  <p><strong>index d637411..b11a95a 100644</strong></p>
  <p><strong>--- a/page1.html</strong></p>
  <p><strong>+++ b/page1.html</strong></p>
  <p>@@ -2,5 +2,7 @@</p>
  <p>&lt;body&gt;</p>
  <p>project 1!</p>
  <p>Hi there!</p>
  <p>+ I am Jalal.</p>
  <p>+ I love programming!</p>
  <p>&lt;html&gt;</p>
  <p>&lt;body&gt;</p>
  <p>\ No newline at end of file</p></th>
  <td><p><strong>diff --git a/page1.html b/page1.html</strong></p>
  <p><strong>index d637411..b2f8fc6 100644</strong></p>
  <p><strong>--- a/page1.html</strong></p>
  <p><strong>+++ b/page1.html</strong></p>
  <p>@@ -2,5 +2,6 @@</p>
  <p>&lt;body&gt;</p>
  <p>project 1!</p>
  <p>Hi there!</p>
  <p>+ I am Jalal.</p>
  <p>&lt;html&gt;</p>
  <p>&lt;body&gt;</p>
  <p>\ No newline at end of file</p></td>
  </tr>
  </tbody>
  </table>

# Resetting and Exiting the Staging Area

  To manipulate the state of your working directory, staging area, and commit history, you can use the `git reset`
  command:

  - To unstage a file, use:
    ```
    git reset <file>
    ```

  - To move the HEAD pointer to a specific commit and optionally modify the staging area and working directory, use:
    ```
    git reset --soft <commit>
    git reset --mixed <commit>
    git reset --hard <commit>
    ```

# Restoring Files

  To manipulate the state of your working directory and staging area without affecting the commit history, you can use the `git restore` command:

  - To unstage a file, use:
    ```
    git restore --staged <file>
    ```
    - it works similarly to the `(git reset <file>)` command.

  - To restore all staged files:
    ```
    git restore --staged *
    ```

  - To  restore file content back to the latest commit:
    ```
    git restore <file>
    ```

  - To restore a specific file from a previous commit to your working directory, use:
    ```
    git restore --source=<commit> <file>
    ```
    - It restores the content of <file> to match the version from the specified <commit>. This will overwrite the file in your working directory with the version from the given commit, but it won't affect the staging area or commit history.

  - To restore your entire working directory to match a specific commit, use:
    ```
    git restore --source=<commit> .
    ```
    
  - To replace a file with the version from the HEAD (latest commit), use:
    ```
    git checkout -- <file>
    ```
    - If you have not yet committed the changes, it will undo all changes and brings the file back to the previous commit file status. So, it restores all the changes back to the latest commit.
    - `'--'`: Refers to the HEAD (latest commit).


# Working With Branches
  
  When you create a new branch, it **inherits the current state** of your working directory and index. Managing branches is essential for collaboration and project organization. Here are some branch-related commands:

  - To show all branches in the project:
    ```
    git branch
    ```
    - The output highlights your current working branch with an asterisk (\*). 
    Example:
    > \$ git branch
    >
    > fixhtml
    >
    > \* master

  - To create a new branch for your project:
    ```
    git branch 'branch-name'
    ```

  - To delete a branch from the project:
    ```
    git branch -d 'branch-name'
    ```

  - To switch to a different branch and replace all the files in your current branch with those from 'branch-name',
    use:
    ```
    git checkout 'branch-name'
    ```
    - So, let’s say you make a new branch and go to this branch, make some files, and change the contents of the other. If you switch back to the master using checkout, all the files and changes that you have made will disappear from your computer directory!

  - To merge a branch into your current branch, use:
    ```
    git merge 'branch-name'
    ```
    - It merges the changes you made in the new branch into the master branch. Note that before using this command, you have to check out first to the master branch.
    - When you switch from one branch to the other (let’s say from master to a new branch named "linkingpages") the git bash interface will show a message, telling you what is different in your working directory compared to linkingpages after switching. D means deleted, and M means modified.
    In this example, one file has been modified and one has been deleted, comparing the branch content with the working directory:

    > \$ git checkout linkingpages
    >
    > D 2_project.html
    >
    > M Git init.docx
    >
    > D index.txt
    >
    > Switched to branch 'linkingpages'
    - When you make changes in your working directory without staging them and then switch branches, Git will try to preserve your changes, but the behavior depends on whether those changes conflict with the files in the branch you're switching to.
    - Until you merge the branch with the master, you cannot see the changes you made on that branch or in the master.

# Cloning a Remote Repository
  
  Remote refers to a repository on a server, like GitHub or
  GitLab, or even another machine. If you clone a repository from
  GitHub, Git automatically creates a remote reference called origin.

  Origin is the default name given to a remote repository when you
  clone a project. It acts as a shortcut to refer to the original
  repository's URL, so you don’t have to type the full address every
  time.

  In Git, a **remote is a reference** because it's essentially a
  **pointer** or **label** that Git uses to keep track of where a
  repository is located. So, a **remote** is a **reference to the
  location of a repository**—this **location** can be a URL, and Git
  uses that reference to fetch and push data. Technically speaking, Git stores remotes as **configuration entries** in your repository. So, remote is a **configuration entry** stored as plain text in the Git configuration file. Git keeps this information in a special file called .git/config in your local repository.
  For example, a typical section in .git/config looks like this:
    > \[remote "origin"\]
    >
    > url = https://github.com/user/repo.git
    >
    > fetch = +refs/heads/\*:refs/remotes/origin/\*
    >
  This configuration section is where **origin** is the reference, and
  The **URL** (https://github.com/user/repo.git) is the data that Git
  uses to access the remote repository.

  - Cloning a project means making a copy of a remote project from a remote location (like GitHub) to your local directory. To do so, we use this command:
      ```
        git clone <remote repository url>
      ```
  - When you already have the repository cloned and want to update it, you want to fetch and merge the latest changes from a remote branch into your current local branch. This, in Git terminology, is called "pulling". We pull the file from the origin and write it on the master branch:
      ```
        git pull origin master
      ```
  - If you made some changes on your local repository, and want to send committed changes from your local repository to the remote server (usually in the cloud, like GitHub or GitLab), you "push" these changes from your master branch to the origin by:
      ```
        git push origin master
      ```
  - If you want to tell Git to make this push path (from master branch to the origin), as a default pushing path, you need to first write:
      ```
        git push -u origin master
      ```  
      (which -u stands for --set-upstream). The next time you want to do the same thing, you only
      need to write `git push`. 

# Adding a Remote Repository

  - To link a remote address to your current project on your local machine, use:
    ```
    git remote add origin <remote_URL>
    ```
    - For starting a project, you make an empty repository on the cloud and link it to your local repository, to save and push files also on the cloud. 
    - You can add multiple remotes to your projects and push them into different repositories at the same time for increased safety.
    - Origin is the default remote name. You can replace the origin with any name you want in this command.

  - To view the remotes attached to your local repository:
    ```
    git remote
    ```

  - To make the output of the previous command (-v stands for "verbose"): 
    ```
    git remote -v
    ```
    - It will give you the name of the remote and the url, both for pull (fetch) and push.

  - To replace the current remote URL with a new one, use:
    ```
    git remote set-url origin <new_remote_URL>
    ```

  - To fetch and merge changes from the remote server into your default local branch, use:
    ```
    git pull origin master
    ```
    - You can substitute any branch name with master if you want to pull changes to another branch.

  - To push changes from your local default branch to the remote repository:
    ```
    git push origin master
    ```

  - To track a remote branch, use:
    ```
    git branch --set-upstream-to=origin/master master
    ```

  - To push the current branch and set the remote as the upstream branch, use:
    ```
    git push --set-upstream origin <local-branch>
    ```

  **Solving Conflicts**

  So, let’s say I pulled the origin, made changes on one of the files.
  And in the meantime, my colleague pulled and made some changes to the
  same file and pushed the changes. So, it means that the current origin
  state is not the same file when I fetch it. Now, if I want to push, git
  gives mean  error, saying that a conflict has happened and you cannot
  make the changes you want on the origin file because its initial
  state is changed. Usually, it guides you, telling you to pull again.
  When you pull it, it tells you that you have some conflicts in the
  file you have been working on. Git is rather smart, so if you and
  your colleague have changed different lines of that part, it
  automatically merges the two changes, and then it allows you to push.
  However, if different changes have been applied to the same parts of
  the code, it needs you to resolve the conflicts. So, if you use the Vim
  editor, you will see the changed parts highlighted in the file. Your
  changes are between \<\<\<\<\<\<\< Header and =====, and his/her
  changes are between \>\>\>\>\>\> (commit hash id) and =======. You can
  decide which to keep and which to discard. you can also discard all
  the signs (\<\<, \>\> and ===)


# Tagging

  Tags are used to mark specific points in the commit history. 
  **Also, you can make versions for your application**

  - To show all tags:
    ```
    git tag
    ```

  - To create a tag for the last commit:
    ```
    git tag -a <version> -m "Your message"
    ```
    - -a is to make an annotation, which stores the message, the tagger, the commit author and the dates.
    - No need to put the version in the double quotation mark.

  - To create a tag for a specific commit:
    ```
    git tag -a <version> <commit-hash> -m "Your message"
    ```
    - You can use git log to see the history of all commits and then copy the hash of the commit action you want to label. No need to put all the hash, even a few starting characters would work.

  - To show a version with all the meta related to it (the message, the tagger, the dates, and the detail of the last commit before annotating that version):
    ```
      git show <version>
    ```

  - To show all the tags starting with 'v0':
    ```
    git tag -l 'v0*'
    ```

  - To push a specific tag to the remote:
    ```
    git push origin <tag-name>
    ```

  - To push all tags to the remote:
    ```
    git push origin --tags
    ```
    - Tags do not make any changes to the working tree, and nothing will be added to the stage (you can verify this using git status). So, if you just use ```git push origin master```, nothing will be added to the remote.

  - To switch to a Tag:
    ```
    git checkout <tag-name>
    ```
    - It will take you back to the last commit of this version; however, as git also tells you, it does not create a separate branch. So, if you make a new commit, this commit will not be made on this version, but it will be applied directly to the original branch you were working on.

  - To verify your tag:
    ```
    git tag -v <tag-name or version-number>
    ```

# GPG Keys and Signing

  **Asymmetric encryption (PGP)** or **PGP (Pretty Good Privacy) encryption** is based on **public-key
    cryptography (asymmetric encryption)**, which uses **two mathematically
    linked keys**:
  
  1.  **Public Key (Shared with Others)**

      - Used to **encrypt** messages.

      - Anyone can use it to send you encrypted messages.

  2.  **Private Key (Kept Secret)**

      - Used to **decrypt** messages.

      - Only you can use it to read messages encrypted with your public key
        

  Let’s break it down with a **real-world example**:

  **🔹 Encrypting a Message (Sending Securely)**

  1.  Alice wants to send a **secret** message to Bob.

  2.  She gets **Bob’s public key** (which Bob has shared publicly).

  3.  She **encrypts** the message using Bob’s **public key**.

  4.  Alice sends the **encrypted message** to Bob.

  **🔹 Decrypting a Message (Reading Securely)**

  1.  Bob receives the **encrypted message** from Alice.

  2.  Since the message was encrypted using his **public key**, it can
      **only** be decrypted using his **private key**.

  3.  Bob **uses his private key** to decrypt and read the message.

  GP is also used for **digital signatures** to prove identity:

  1.  Bob wants to send an **authentic** message to Alice.

  2.  Bob **signs the message with his private key**.

  3.  Alice **verifies the signature using Bob’s public key** to confirm
      it came from him.

  GPG was for commercial and private companies, so GPG has been developed.
  using the same principles for open-source use.

  Now, you can digitally **sign** tags and commits in git using GPG, so
  fully prove your identity, and make every one sure that the commit or tag
  is done by you! Now, how do I make a key?

  - To generate a new key:
    ```
    gpg --gen-key
    ```
    - Now that you have your key, you give your public key to anyone who wants to see your signatures and keep your private key for signing.

  - To list all your **public keys** in your keyring:
    ```
    gpg --list-keys
    ```
    - Your public key allows others to verify your signature. Without your public key, people can still see your commits/tags, but they can't verify their authenticity. It ensures that no one else has forged your identity to push commits under your name. Anyone can set their Git username and email to pretend to be you: by git config --global user.name "Your Name" and git config --global user.email <your@email.com>. This means someone can fake commits under your name, but if they don't have your private key, they can't sign them.
  
  - To list all your **private (secret) keys** in your keyring:
    ```
    gpg --list-secret-keys --keyid-format LONG
    ```
    - This is your signing key. You’ll get something like this: the highlighted part is your key.

    output example: The highlighted part is your private key.
  
    >
    > sec ed25519/`51D5C682AB1A7B0C` 2025-02-13
    > \[SC\] \[expires: 2028-02-13\]
    >
    > CC22A2B6C514DB471260321E51D5C682AB1A7B0C
    >
    > uid \[ultimate\] Jalal Abbasi \<s.jalalabasi@gmail.com\>
    >
    > ssb cv25519/678FBAE76D47A781 2025-02-13 \[E\] \[expires: 2028-02-13\]

  - To show your private signing key:
    ```
      git config --global user.signingkey
    ```
    - If you have not set any yet in git, it does not show anything.

  - Set your signing key for the current user across all repositories:
    ```
    git config --global user.signingKey 'your-secret-key'
    ```

  - To tag the last commit with your signature:
    ```
      git tag -s <version> -m “message”
    ```
  
  - To commit with your signature: 
    ```
    git commit -S -m “message”
    ```
    - If you use git log, it does not show if it is signed or not.

  - To verify if the <version> is signed:
    ```
      git tag -v <version>
    ```
    - -v here means to verify (do not mistake it with "verbous")
    - If verified, you’ll get a message like: Good signature from "Jalal Abbasi <s.jalalabasi@gmail com>" [ultimate]

  - To see the exact signature characters as a part of the tag message:
    ```
      git show <version>
    ```
    - It is a code between two lines, as below:
        >-----BEGIN PGP SIGNATURE-----
        >
        >iHUEABYKAB0WIQTMIqK2xRTbRxJgMh5R1caCqxp7DAUCZ65O2wAKCRBR1caCqxp7
        >
        >DCIOAQCgjUvfc/cyJc7dlZxhtlJwSBj270Cu+1HXPIIhaLSpYQD+J9FXuqfwUUqK
        >
        >nWWqA7pTgfPWzNeJNPqujussqPns1gA=
        >
        >=/A/w
        >
        >-----END PGP SIGNATURE-----
  

# Debugging Using Git

  - To show all the change history about your file:
    ```
    git blame <file>
    ```
    - It shows who has written which part of this last code and when.
  - To show all the change history about your requested line in the requested file:
    ```
    git blame <file> -Ln
    ```
    - It shows who has written the code in line “n”, in the <file>, in a chronological order, from the latest to the oldest.
  - To show the last person who has modified the code between lines n and m and the date he/she modified it:
    ```
      git blame <file> -Ln,m
    ```
  - Git Blame is useful for tracing the changes made to a file. It helps in understanding who made the changes and when they were made, which can be valuable for tracking alterations, identifying contributors, and understanding the evolution of the codebase.

  **Bisect**

  (binary-search-commits)So, you are in the latest commit, and you have
  a bug in your code, and you want to find it, git helps you to find it iteratively.

  So first, you must go to the highest level of the directory. Then you tell
  git to start the process. Then you say the latest commit is bad. Then
  ask you to determine what was the latest commit was in the history, which was
  working fine. Given these two commits, git goes and finds the commit
  between these two, and asks you to check if it is good or bad. If it is
  good, it means that the bug is present between this middle commit and
  the latest one, and if not, it means that the bug is present between
  this middle commit and that last good commit.

  1.  ```git bisect start```: telling git to start the bisect.

  2.  ```git bisect bad```: telling git that the commit that we are now at
      it, so the latest one, is bad (buggy).

  3.  ```git bisect good <commit-hash>```: Then we have to tell git the last commit in the log, in which the code was working well.

  4.  ITERATIVE: Then git gives you a commit hash and asks you to check if
      it is good or bad. If good, you write git bisect good, else you
      write git bisect bad. Then, git now checks again, between the commit
      it mentioned you, and the last or the last good commit, according to
      your answer, and gives you another commit to check. Then this
      iteration goes on this way.

# Forking and Pull (Merge) Request

  Let’s say someone has a repository in their GitHub or GitLab profile.
  Forking means making a copy of their project and placing it on your
  repository tab, so that you can work on it separately. So, you clone
  this forked project and work on it on your local machine and make some
  changes to it. Then, you push these changes to your own forked project.
  If you want to notify the guy who originally made the project about your
  changes and ask him if he wants to merge these changes also to his own
  project, you send him a pull request (in GitHub) or a merge request (in
  Gitlab). The guy will check your changes and decide whether to accept
  this merge or not.**

# Other Git Commands
  - Differences in using "--":

    1. ```--<name>```: name is a parameter of the command: like ```git diff --staged``` 🡪 checks the staged files

    2. ```-- <name>```: name is a file name: like ```git checkout -- page1.html```

  - To configure git settings on three levels:
      ```
      git config --system/--global/--local <action>
      ```

    | **Level** | **Scope** | **Location** |
    |----|----|----|
    | **System** | Applies to all users on the system | /etc/gitconfig |
    | **Global** | Applies to your user across all repos | ~/.gitconfig or ~/.config/git/config |
    | **Local** | Applies only to the specific repository | .git/config inside the repo |

  - To ask for your system user:
      ```
      git config --global user.name
      ```
  
  - To you, git help:
    ```
      git help <command>
    ```

# Unix-Specific Commands

  - ```touch <file>```: To create an empty file (any type: text, html, etc) on the Git bash.

  - ```diff```: Shows the differences made in the current file

  - ```cat filename.txt```: Shows the content of the file (cat stands for concatenate)

  - ```cat file1.txt file2.txt > combined.txt```: This will **combine** file1.txt and file2.txt into a new file called combined.txt.

  - ```cat > newfile.txt```: This allows you to **create and write** to a new
  file. After running the command, you can type your content and press
  Ctrl+D to save and exit.

  - ```~```: Refers to your home directory in Git Bash (C:\Users\YourUsername)

  - ```vi <file>```: To edit a file in Vim text editor, or create a new one, does not
  exist: 

  **Vim text editor**:  
  It is a widely used **text editor** available in almost all **Unix-based environments**, including **Linux, macOS, and BSD**.

  Here’s a compact table of basic Vi (Vim) commands:

  | **Mode**        | **Command** | **Action**                  |
  |-----------------|-------------|-----------------------------|
  | **Insert Mode** | i           | Insert at cursor            |
  |                 | a           | Append after cursor         |
  |                 | o           | Open a new line below       |
  | **Exit & Save** | Esc → :wq   | Save and exit               |
  |                 | Esc → :x    | Save and exit (same as :wq) |
  |                 | Esc → :q!   | Quit without saving         |
  |                 | Esc → :w    | Save without quitting       |
  | **Navigation**  | h           | Move left                   |
  |                 | l           | Move right                  |
  |                 | j           | Move down                   |
  |                 | k           | Move up                     |
  |                 | gg          | Go to first line            |
  |                 | G           | Go to last line             |
  | **Editing**     | dd          | Delete current line         |
  |                 | yy          | Copy (yank) current line    |
  |                 | p           | Paste after cursor          |
  | **Search**      | /text       | Search for "text"           |
  |                 | n           | Jump to next match          |
  |                 | N           | Jump to previous match      |
  | **Undo/Redo**   | u           | Undo last change            |
  |                 | Ctrl + r    | Redo last undo              |


  

Remember to use these commands as needed in your Git projects. It's important to maintain a clean and organized version
control process for effective collaboration and project management.
