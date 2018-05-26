---
layout: post
cover: false
title: Linux Tutorial - Understanding User and Group
date: 2018-05-26 23:18:00
tags: Linux
subclass: 'post tag-linux'
categories: 'iqbaladan'
navigation: True
#logo: 'assets/images/iqbal.png'
#cover: 'assets/images/cover8.png'
disqus: true
---

![Workspace edit.png](https://cdn.utopian.io/posts/07772c5e6cc8640938fc19ec3b13859d829dWorkspace_edit.png)

## Introduction
Linux is a multiuser operating system, which means that Linux is an operating system that is designed to be used by many users simultaneously. This requires Linux to impose restrictions so that user A can not see or delete user B's data and vice versa.

#### What Will I Learn?
- You will learn what User and Group are in Linux operating system (in this case Debian 9) with explanations
- You will learn how to add User and Group along with the necessary settings and configurations
- You will learn how to manage User and Group properties for everyday work in a Linux environment

#### Requirements
To follow this tutorial, users are expected to be familiar with;

- Linux Operating System (Debian-based)
- Basic understanding and using of Linux Command Line Interface (CLI).

#### Difficulty

- Basic

#### Tutorial Content
This time I will discuss and show you what and how to manage users, groups and a couple of things should be considered about User ang Group in Linux.

## User Account
Linux users, usually know only two User Accounts for instance `iqbaladan` or `utopian` account and `root` account. In addition to `root` and regular user accounts. Actually, Linux also automatically creates other accounts that have their respective tasks and principal functions. Generally, user account on Linux is divided into 3 groups only, namely:

* __root account__
This account has highest access privileges, can do anything from installing, creating documents, reading files, even able to delete anything. There is only one root account on the system and it can not be deleted, but we still can change its name to e.g: iqbaladan, this action is strongly discouraged.

* __Normal user account__
This is a normal or regular account with limited permissions created manually in accordance with the criteria allowed by the root account above. This account can be created using Graphical User Interface or with Command Line Interface.

* __System account__
The last are special accounts created automatically with their each tasks. We can not log in with this type of account. For example the account `lp`. This account is used by the process of printing documents to the printer. In addition to the `lp` account, there are many more such system accounts with their specific tasks and functions such as `daemon`, `adm`, `bin` and so on.

One thing should be remembered and noted that the username in Linux distinguish lowercase and uppercase, case sensitive. `Utopian`, `utopian` and `utoPian` are three different users, usually naming this username using all lowercase letters to avoid confusion.

### Understanding `/etc/passwd`
The user accounts in Linux are stored in a plain text in `/etc/passwd`. You can see it using the `cat` command.

![user@debian: ~_002.png](https://cdn.utopian.io/posts/a0d32eb03e79c5d088cc5b31b72c52a7c47fuser@debian:_~_002.png)

```
user@debian:~$ cat /etc/passwd
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
sys:x:3:3:sys:/dev:/usr/sbin/nologin
sync:x:4:65534:sync:/bin:/bin/sync
games:x:5:60:games:/usr/games:/usr/sbin/nologin
.
.
.
avahi:x:114:119:Avahi mDNS daemon,,,:/var/run/avahi-daemon:/bin/false
colord:x:115:120:colord colour management daemon,,,:/var/lib/colord:/bin/false
saned:x:116:121::/var/lib/saned:/bin/false
Debian-gdm:x:117:122:Gnome Display Manager:/var/lib/gdm3:/bin/false
user:x:1000:1000:Debian Live user,,,:/home/user:/bin/bash
```

It appears that there are other users besides the root user as I have discussed above all of which are system accounts.

The file in this `/etc/passwd` does not only store the user name and also the user's password, but also other information about the account. Each line of the `/etc/passwd` file consists of 7 columns/sections separated by a colon`:`.

`iqbaladan:x:500:500:iqbal adan utopian:/root:/bin/bash`

| No |       Column       |                                                                                            Explanation                                                                                           |
|:--:|:------------------:|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|
|  1 |      iqbaladan     | Used for log in, it is strongly recommended to use lowercase                                                                                                                                     |
|  2 |          x         | Encrypted root password, if the sign is `x` as in the above example, it means that this encrypted password is stored in `/etc/shadow`. If it contains a `(*)` sign, the account is not activated |
|  3 |         500        | User Id (UID) of the related account                                                                                                                                                             |
|  4 |         500        | Group Id (GID) of the related account                                                                                                                                                            |
|  5 | iqbal adan utopian | a description column containing the full name of the user                                                                                                                                        |
|  6 |   /home/iqbaladan  | location of the home directory owned by the user                                                                                                                                                 |
|  7 |      /bin/bash     | Shell provided to users at login or using text mode                                                                                                                                              |

### Understanding Password Storage File at `/etc/shadow`
This file is an additional file that can only be read by the root account so that it can not be read by anyone, so the existing application still runs fine, while the `/etc/shadow` file can only be read and accessed by the root account.

![user@debian: ~_003.png](https://cdn.utopian.io/posts/81f473a2a56fb8f6986c06d75c3a37b34bfduser@debian:_~_003.png)

```
root@debian:~# cat /etc/shadow
root:*:17541:0:99999:7:::
daemon:*:17509:0:99999:7:::
bin:*:17509:0:99999:7:::
sys:*:17509:0:99999:7:::
sync:*:17509:0:99999:7:::
games:*:17509:0:99999:7:::
.
.
.
avahi:*:17509:0:99999:7:::
colord:*:17509:0:99999:7:::
saned:*:17509:0:99999:7:::
Debian-gdm:*:17509:0:99999:7:::
user:8Ab05sVQ4LLps:17541:0:99999:7:::
```

Similar to the `/etc/passwd` file, the `/etc/shadow` file also includes some pieces of information separated by a colon `:`.

`iqbaladan:8Ab05sVQ4LLps:17541:0:99999:7:::`

| No |     Column    |                                                                                    Explanation                                                                                   |
|:--:|:-------------:|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|
|  1 |   iqbaladan   | Name used for login, same as in `/etc/passwd`                                                                                                                                    |
|  2 | 8Ab05sVQ4LLps | encrypted login password                                                                                                                                                         |
|  3 |     17541     | number of days since password changed. Calculated since January 01, 1970                                                                                                         |
|  4 |       0       | Minimum lifespan for an account to change the password (calculated in days). If filled with 3 then you can just change the password on Thursday if previously replaced on Monday |
|  5 |     99999     | The maximum age of a password, calculated in days, if you fill 60 days, then every 60 days you must change the new password                                                      |
|  6 |       7       | Users will be reminded to change their password 7 days before the maximum age of the password is passed                                                                          |
|  7 |    (Empty)    | How long does it take to not to change the password after the maximum age limit of a password is passed. If this time is passed, then the account will be automatically disabled |
| 8  | (Empty)       | How long will it take for no login at all, starting from January 1, 1970. The account will be disabled if this time elapses                                                      |
| 9  |    (Empty)    | Not used                                                                                                                                                                         |

## Group
Each Linux account can be a member of one group or multiple groups at once. Information about each group and its members are stored in `/etc/group`'s file.

![user@debian: ~_004.png](https://cdn.utopian.io/posts/4f2042b34293f8d9b2185713f4d93732a232user@debian:_~_004.png)

```
user@debian:~$ cat /etc/group
root:x:0:
daemon:x:1:
bin:x:2:
sys:x:3:
adm:x:4:
tty:x:5:
disk:x:6:
lp:x:7:
mail:x:8:
.
.
.
ssh:x:113:
bluetooth:x:114:user
geoclue:x:115:
pulse:x:116:
pulse-access:x:117:
scanner:x:118:saned,user
avahi:x:119:
colord:x:120:
saned:x:121:
Debian-gdm:x:122:
user:x:1000:
```

As in the `/etc/ passwd` file, the `/etc/group` file also consists of several parts separated by a colon`:`.

`root:x:0:`

| No |  Column |                                                                         Explanation                                                                        |
|:--:|:-------:|:----------------------------------------------------------------------------------------------------------------------------------------------------------:|
|  1 |   root  | Group name. This name is displayed as the file owner group in the command `ls -l`                                                                          |
|  2 |    x    | password for the group, which is almost never used. The `x` character indicates that the password is stored in `/etc/gshadow`                              |
|  3 |    0    | Group ID (GID), or unique code from each group. This code is shown in `/etc/passwd`'s file. By default the Gropu ID (GID) is the same as the User ID (UID) |
|  4 | (Empty) | The username which is a member of the group. Some usernames can be included into a group with comma characters as separator marks.                         |

## Creating Users and Groups
User and group accounts can be created using text mode and GUI. Each way has advantages and disadvantages. GUI offers a nice and easy to use way but you need to be more patient because it has to wait for the menu to show up and a slower process.

### Adding User Accounts with GUI
Adding a user account with Graphical User Interface (GUI) is the easiest way. It can be done by hover over the _Setting -> System -> Users_. 

![All Settings_007.png](https://cdn.utopian.io/posts/3343c6eabc0a2b27b8d62c7dd965ecae7dd7All_Settings_007.png)

Next step is to hit the blue _Add User_ button, then fill in the desired name. As we can see, the user created is `utopia` this because user` utopian` is already exists. Creating user with GUI also gives some setting options.

![Add User_008.png](https://cdn.utopian.io/posts/0a96803ab0b217d47fee70c0fb1ac164038fAdd_User_008.png)


### Adding User Accounts with Command Line
Adding a user account with the command line can be done using `useradd` or` adduser`. The actual command is `useradd`, while `adduser` is a soft link to the `useradd` command. The `useradd` command adds a user account without providing a password, so you need to add a password for the newly created account with the command `/usr/bin/passwd`.

```
root@debian:~# useradd utopian
root@debian:~# passwd utopian
Enter new UNIX password:
Retype new UNIX password:
passwd: password updated successfully
```

![user@debian: ~_005.png](https://cdn.utopian.io/posts/832ef1c0fbd6abd77712ad15599222d3eb54user@debian:_~_005.png)

In the above example, after adding a utopian user with the command `useradd utopian`, I provide the password on that account with the command 'passwd utopian`.

To manipulate groups, often use `groupadd [groupname]` to add a group, `usermod -G [groupname] [username]` command to add user into group and `groupdel [groupname]` to delete a group.

```
root@debian:~# useradd utopian
root@debian:~# groupadd steemit
root@debian:~# usermod -G steemit utopian
root@debian:~# tail -2 /etc/group
utopian:x:1001:
steemit:x:1002:utopian
root@debian:~# groupdel steemit
```

![user@debian: ~_006.png](https://cdn.utopian.io/posts/e959bfc0b8584a4af54deb585055591a9333user@debian:_~_006.png)

Here are the  explanation of the above commands;
* `useradd utopian` -> create a new user with utopian name. This command also automatically adds a gruop with utopian name.
* `groupadd steemit` -> create a new group called steemit.
* `usermod -G steemit utopian` -> add a utopian user into steemit group.
* `tail -2 /etc/group` -> see the last 2 groups created, utopian and steemit. It appears that steemit has a utopian as a member.
* `groupdel steemit` -> delete steemit group.

### Set User Property
We've already discussed the use of `useradd` to add a user account and create a group for that user. So how to set the validity of the account as I explain in the discussion of `/etc/shadow` can be done? You can do it in three ways:

__The first way__ is to use the `usermod` command. This command can be used to set the validity time of an account, in this case `utopian`;

```
root@debian:~# useradd utopian
root@debian:~# usermod -e 5/30/2019 utopian
```

which mean the `utopian` user will expire on 5/30/2019, after this time limit, the `utopian` user can no longer be used.

With `usermod`, you can also disable (lock) or enable the user, change the `home` directory, change the shell, change the UID, and so forth. As usual, you can run the command `man usermod` or `usermod --help` to get more explanations of the parameters of this command.

__The second__ way is to provide additional parameters when account is created with `useradd`. There are dozens of additional parameters you can use to manage user creation. You can use the manual of this command with `man useradd`. The parameters used to set the validity of an account are `-e`, for instance;

`root@debian:~# useradd -e 5/30/2019 utopian`

__The third way__ is to change the default behavior of `useradd`. You can do this by editing the `/etc/login.defs` and `/etc/default/useradd`'s files. To know more information and purpose of this parameter, it can be seen through command `man login.defs`. I use the `grep` command after `cat` to remove only blank lines, or comments (comment lines in the configuration file usually start with #).

```
root@debian:~# cat /etc/default/useradd | grep -v "^#"
root@debian:~# cat /etc/login.defs |grep -v "^&"|grep -v "^#"
```

## Conclusion
We have discussed about Users and Groups in the Linux operating system, as well as how to add and delete Users and Groups on Linux operating system along with some settings and configurations. Hopefully this tutorial is useful for Linux users to gain more understanding about User and Group in Linux operating system.

Best regards, @iqbaladan.
