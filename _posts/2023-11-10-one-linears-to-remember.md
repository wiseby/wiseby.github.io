---
layout: post
title: "Code & Command Vault"
categories: ["Programming"]
---

### Git

#### Local exlusion of files

Useful when you have files that never should be updated from remote nor be pushed to remote, but is source controlled.

Add the files to your _.git/info/exclude_ file with the same syntax as any gitignore file.

If the files is already tracked locally you have to update the index to make this do effect. Do that with the following command: 

```git update-index --assume-unchanged <file-list>```

### Powershell

- Creating symlinks:
  
  `New-Item -ItemType SymbolicLink -Path <destination ex (./media)> -Target <path to media folder>`
