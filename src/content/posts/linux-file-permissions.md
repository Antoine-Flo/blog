---
title: "Linux File Permissions"
published: 2025-07-07
draft: false
toc: true
description: 'Understanding Linux file permissions and user access control—how to secure your files and directories properly.'
series: 'Linux'
tags: ['security']
---

Linux offers a powerful set of tools for managing user rights and permissions. We give minimum rights to users and processes to limit potential damage.

## The three kind of rights

1. Read (r): Allows a user to view the contents of a file or directory.
2. Write (w): Allows a user to modify or delete a file or directory.
3. Execute (x): Allows a user to run a file or access a directory.


## The three permission groups

### Users
Each individual user on a Linux system has a unique user ID (UID) and associated permissions. User accounts can be created, modified, and deleted using various command-line tools.

There is one special user named rot. The root user has unrestricted access to all commands and files on a Linux system. As a best practice, it is recommended to use the root account only when absolutely necessary.

### Group
You can organize users into groups to manage permissions more easily. Each file and directory has an associated group, and users can be added to or removed from these groups.

A user can be in multiple groups. In that case, the user inherits the permissions of all groups they belong to.

A file always has an owner (user) and a group owner. The owner has full permissions, while the group and others have limited permissions.


### Others
Others refer to all users who are not the owner of a file or a member of the file's group. They have the least amount of permissions.

## Manage group and user

### Get infos about user and group

```bash
cut -d: -f1 /etc/passwd  # List all users
cut -d: -f1 /etc/group  # List all groups

id [username]  # Get user ID (uid), group ID (gid), and group memberships
groups [username]  # List all groups the user is a member of
```

### Create a user

```bash
sudo useradd [username]
```

### Create a group

```bash
sudo groupadd [groupname]
```

### Add a user to a group

```bash
# When creating a new user
sudo useradd -m -G [groupname] [username]  # -m creates home directory
# Add an existing user to a group
sudo usermod -aG [groupname] [username] # -a append, keep the previous groups
```

### Delete a user or a group

```bash
sudo userdel [username]  # Delete a user
sudo groupdel [groupname]  # Delete a group
sudo userdel -r [username]  # Delete a user and their home directory
```

### Set password for a user

```bash
sudo passwd [username]
sudo chpasswd [username]  # Change password
```

## Manage rights

### Check rights 

#### Symbolic notation

You can check the permissions of a file or directory using the `ls -l` command. This will display a list of files and directories along with their permissions, owners, and groups.

```bash
-rw-r--r-- 1 user group 0 Jul  7 12:00 file.txt
-rwxr-xr-x 1 bob devops 0 Jul  7 12:00 script.sh
 \ /\ /\ /
  v  v  v
  |  |  droits des autres utilisateurs (o)
  |  |
  |  droits des utilisateurs appartenant au groupe (g)
  |
  droits du propriétaire (u)
 
r : read | w : write | x : execute
```

The rights are divided 3 by 3. The first character represents the file type '-' for file, 'd' for directory, and 'l' for symbolic link. The first three characters represent the owner's permissions, the second three the group's permissions, and the last three others' permissions.

For the `file.txt`, the owner (user) has `rw-` read and write permissions, the group has read permissions `r--`, and others have read permissions. For the `script.sh`, the owner has read, write, and execute permissions, the group has read and execute permissions, and others have read and execute permissions.

#### Octal notation

In addition to the previous notation, Linux also supports octal notation for file permissions. In this notation, each permission is represented by a number:

- Read (r) is represented by 4
- Write (w) is represented by 2
- Execute (x) is represented by 1

To calculate the octal representation, you simply add up the values for each permission. For example:

- `rw-` (read and write) is 4 + 2 + 0 = 6
- `r--` (read only) is 4 + 0 + 0 = 4
- `rwx` (read, write, and execute) is 4 + 2 + 1 = 7

Using octal notation, the permissions for the files in our example would be:

```bash
644 file.txt
755 script.sh
```


### Update rights

#### chmod

To add or remove permissions :

```bash
chmod [who][+|-|=][permissions] file
```

- `who` can be `u` (user/owner), `g` (group), or `o` (others).
- `+` adds the specified permissions, while `-` removes them.
- `permissions` is the permission to add or remove (r, w, x).

For example, to add execute permission for the user on `script.sh`, you would run:

```bash
chmod u+x script.sh
chmod u+x,g-w script.sh # Assign multiple permissions
chmod o=r-- script.sh
```

To change permissions using octal notation :

```bash
chmod [permissions] file
```

For example, to set the permissions of `file.txt` to `644`, you would run:

```bash
chmod 644 file.txt
```

#### Change owner

The `chown` command is used to change the owner and group of a file or directory :

```bash
sudo chown [new_owner]:[new_group] file
```

For example, to change the owner of `file.txt` to `alice` and the group to `dev`, you would run:

```bash
sudo chown alice:dev file.txt
```

#### Change groupe

The `chgrp` command is used to change the group ownership of a file or directory :

```bash
sudo chgrp [new_group] file
```

```bash
sudo chgrp dev file.txt
```

## Useful commands

### sudo

The `sudo` command is used to execute a command with superuser (root) privileges. This is useful for performing administrative tasks that require elevated permissions. `sudo` is a group so you must add a new user to the `sudo` group to grant them the access to this command.

```bash
sudo [command]
```

For example, to edit a system file with a text editor :

```bash
sudo nano /etc/hosts
```

### Update a user

`usermod` command is used to modify a user account. You can change various attributes of the user, such as their home directory, shell, or group memberships.

```bash
sudo usermod -d /new/home/dir alice  # Change home directory
sudo usermod -s /bin/zsh alice  # Change default shell to zsh
sudo usermod -L alice  # Lock the user account
sudo usermod -U alice  # Unlock the user account
```

### Check user group

```bash
id -ng

id -Gn # List all groups the user is a member of
```
> devops dev

