---
title: Git
description: 
published: true
date: 2020-10-13T10:05:18.150Z
tags: github, git
editor: markdown
dateCreated: 2020-06-04T18:23:52.812Z
---

# Git

## Commands

- `git push`:
Pushes the code(text) to your (remote) repository.
---

- `git pull`:
Pulls the code(text) from your (remote) repositry.
---

- `git status`:
Show your changes you will made with an `git commit`.
---

- `git commit -m`:
Gives an comment (-m) to your (push) commit
---

- `git fetch`:
Fetches all 'unknown/new' commits, without the merge which `git pull` will automatically do for you.
---

- `git merge`:
will combine multiple sequences of commits into one unified history.

---

- `git rev-parse (HEAD / FETCH_HEAD)`:
Get's the SHA1 hashed from the current commit or the new 'fetch' commit
---

- `git diff (--name-only)`:
Shows the changes between commits
---

- `git stash`
*Record the current state of the working directory and the index, but want to go back to a clean working directory. The command saves your local modifications away and reverts the working directory to match the HEAD commit.*
---

- `git log`
Show commit logs
---

## Custom SSH key name
> on windows you need to use the config file in the .ssh directory of your userprofile.
{.is-info}

make in `$env:UserProfile\.ssh` folder a file named `config`

content of the file should be:

```powershell
# Comment (optional)
Host github.com
	HostName github.com
	User git
	IdentityFile C:\Users\Example\.ssh\privateSSHkey {path to private ssh key}
```


