![image](https://github.com/user-attachments/assets/bd8d434d-e625-4589-8337-0def76bbaa11)# PP5

## Goal

In this exercise you will:

* Use Git **locally** on your own machine: create branches, make commits, and merge them back.
* Set up and interact with a **bare** Git repository on an SSH‐accessible server (e.g. **vorlesungsserver**, or any machine you have SSH access to).
* Push and pull to/from **GitHub** and the **THGA GitLab** server.
* Practice **forking** an existing repo, making changes, and submitting a **Pull Request** (on GitHub) or **Merge Request** (on GitLab).

**Important:** Start a stopwatch when you begin and work uninterruptedly for **90 minutes**. Once time is up, stop immediately and document exactly where you had to pause.

---

## Workflow

1. **Fork** this repository
2. **Modify & commit** your solution
3. **Submit your link for Review**

---

## Prerequisites

* Several starter repos are available here:
  [https://github.com/orgs/STEMgraph/repositories?q=Git%3A](https://github.com/orgs/STEMgraph/repositories?q=Git%3A)
* Ensure you have **SSH access** to a remote server (e.g., “vorlesungsserver”).
* Throughout, consult Git’s built-in man-pages (`git help <command>`) for explanations and options.

---

## Tasks

### Task 1: Local Git – Branching & Merging

1. Create a new directory in your home directory and initialize a repository in it. 
2. In one of your cloned repos, initialize a new branch called `feature-1`.
3. On `feature-1`, create a file `feature.txt` containing a short description of what you’re doing.
4. Commit your changes, then switch back to `master` (or `main`), and merge `feature-1` into your `master`.
5. Resolve any merge conflicts (if they arise) by hand, then commit the merge. 

**Your Commands & Output**

```bash
# Paste here the sequence of git commands you ran
•	mkdir PPT5 (neues directory anlegen)
•	cd PPT5 (wechseln in directory PPT5)
•	git init (Initialisierung des Projekts PPT5/Umwandlung in ein Git-Repository)
•	git checkout -b feature-1 (Anlegen/initialisieren der neuen branch ,,feature-1‘‘) 
•	touch feature.txt (Erstellen der Datei ,,feature.txt‘‘)
•	vim feature.txt (Öffnen der Datei ,,feature.txt‘‘ im vim-Editor und Eintragung von Änderungen)
•	git add feature.txt (Stagen der Änderungen an Datei ,,feature.txt‘‘ in branch ,,feature-1‘‘)
•	git commit (committen der Änderungen)
•	git checkout master (Wechseln in branch master)
•	git merge feature-1 (Änderungen aus branch feature-1 in branch master überführen)

# and the relevant terminal output (e.g., branch listing, merge messages)

•	nachdem die Änderungen an der Datei feature.txt vorgenommen wurden:
o	git status

On branch feature-1

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        feature.txt

nothing added to commit but untracked files present (use "git add" to track)
![TASK 1 - Ausgabe 1](https://github.com/user-attachments/assets/a93018fb-9c67-42a3-8af1-6ab971797567)

 

•	nach git add feature.txt
o	git status

On branch feature-1

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   feature.txt

![TASK 1 - Ausgabe 2](https://github.com/user-attachments/assets/b8bf43ab-f2ca-4332-aaab-feea92a55e74)

 

•	nach git commit (und Eingabe der Commit Message „Initial commit‘‘ über den Text editor nano)
o	Ausgabe:

[feature-1 (root-commit) 3dd6ecc] ''Initial commit''
 1 file changed, 7 insertions(+)
 create mode 100644 feature.txt
![TASK 1 - Ausgabe 3](https://github.com/user-attachments/assets/42b9b6b3-cf0d-4acb-b9a6-fbb132dc8f33)

 

•	Nach git merge feature-1 und git log –online
o	Ausgabe:

3dd6ecc (HEAD -> master, feature-1) ''Initial commit''
![TASK 1 - Ausgabe 4](https://github.com/user-attachments/assets/3d09c7e1-138b-4ea6-9b5e-0f98aa75ee41)

 

```

---

### Task 2: Bare Repository on an SSH Server

1. On your SSH server (e.g., “vorlesungsserver”), create a **bare** repo at `~/repos/myproject.git`:

   ```bash
   ssh youruser@vorlesungsserver \
     "mkdir -p ~/repos/myproject.git && cd ~/repos/myproject.git && git init --bare"
   ```
2. On your local machine, add it as a remote named `origin-ssh`:

   ```bash
   git remote add origin-ssh youruser@vorlesungsserver:~/repos/myproject.git
   ```
3. Push your `master` branch to `origin-ssh`, then clone it into a fresh directory to verify.

**Your Commands & Output**

```bash
# Paste here the push & clone commands and outputs

•	Push command und zugehörige Ausgabe:

kami@DESKTOP-H0USJ60:~/PPT5_Task2$ git push origin-ssh master
user48@128.140.85.215's password:
Enumerating objects: 6, done.
Counting objects: 100% (6/6), done.
Delta compression using up to 8 threads
Compressing objects: 100% (4/4), done.
Writing objects: 100% (6/6), 545 bytes | 68.00 KiB/s, done.
Total 6 (delta 0), reused 0 (delta 0), pack-reused 0
To 128.140.85.215:~/repos/myproject.git
 * [new branch]      master -> master

![Task 2 Push command und output](https://github.com/user-attachments/assets/9135de13-b33a-418b-b31b-7f329e4bb9b6)

•	Clone command und zugehörige Ausgabe:

kami@DESKTOP-H0USJ60:~$ mkdir myproject-clone
kami@DESKTOP-H0USJ60:~$ cd myproject-clone
kami@DESKTOP-H0USJ60:~/myproject-clone$ git clone user48@128.140.85.215:~/repos/myproject.git
Cloning into 'myproject'...
user48@128.140.85.215's password:
remote: Enumerating objects: 6, done.
remote: Counting objects: 100% (6/6), done.
remote: Compressing objects: 100% (4/4), done.
remote: Total 6 (delta 0), reused 0 (delta 0), pack-reused 0
Receiving objects: 100% (6/6), done.
kami@DESKTOP-H0USJ60:~/myproject-clone$ cd myproject
kami@DESKTOP-H0USJ60:~/myproject-clone/myproject$ git log
commit 65d6059ed438b253292a2bab065191b78ed7db5f (HEAD -> master, origin/master, origin/HEAD)
Author: Kai Mischke <kai-timo.mischke@stud.thga.de>
Date:   Wed May 21 23:18:12 2025 +0200

    Quick commit

commit 14af5885b359b558ed0a4a2878570ffe11456cd6
Author: Kai Mischke <kai-timo.mischke@stud.thga.de>
Date:   Wed May 21 21:11:08 2025 +0200

    Quick commit

![Task 2 clone command und output](https://github.com/user-attachments/assets/070f6a9d-2b17-4eaf-9592-0967a311897d)

```

---

### Task 3: GitHub & THGA GitLab

1. On [GitHub](github.com), create a new empty repo under your account named `myproject-gh`.
2. On [THGA GitLab](gitlab.thga.de), create a new project named `myproject-gl`.
3. In your local repository, add these as remotes:

   ```bash
   git remote add github  git@github.com:YOUR_USERNAME/myproject-gh.git
   git remote add gitlab  git@gitlab.thga.de:YOUR_USERNAME/myproject-gl.git
   ```
4. Push your `master` branch to both `github` and `gitlab` remotes.

> Hint: You are just adding two more bare-remotes to your already existing repository!

**Your Commands & Output**

```bash
# Paste here the remote‐adding & push outputs

Beim Versuch die THGA GitLab Seite zu öffnen kommt folgende Meldung:

![Page not found](https://github.com/user-attachments/assets/a846e426-46cb-467c-9f35-de983057f11d)


```

---

### Task 4: Fork, Modify, and Pull/Merge Request

1. On GitHub, **fork** one of the repos from the STEMgraph org.
2. Clone your fork locally, create a branch `pp5-changes`, and make a small change (e.g., update the README).
3. Commit and push `pp5-changes` to **your** fork, then open a **Pull Request** against the original repo.
4. Repeat on THGA GitLab: fork another students repository, clone, branch, change, push, and open a **Merge Request**. If your peers opened a merge request to your repository, review and merge or decline it!

**Your PR/MR Links & Descriptions**

* GitHub PR: *paste URL and a one-sentence summary*
* GitLab MR: *paste URL and a one-sentence summary*

---

**Remember:** Stop working after **90 minutes** and record where you stopped!
