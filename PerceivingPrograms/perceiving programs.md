## PERCEIVING PROGRAMS

`ls -l` allows you to see the permissions of a directory/file

## Changing File Permission
we use the `chown` command to change owner of a file.   
format: chown [user name] [file name]     
this can be used only by the root user usually

first I used `ls -l` to see all the permissions:
```
hacker@permissions~changing-file-ownership:~$ ls -l
total 44
-rw-r--r-- 1 hacker hacker 147 Oct  8 18:00 2
-rw-r--r-- 1 hacker hacker   4 Oct  8 12:00 COLLEGE
-rw-r--r-- 1 hacker hacker   8 Oct  8 13:10 PWN
-rw-r--r-- 1 root   hacker  58 Oct  2 05:34 h
-rw-r--r-- 1 hacker hacker 829 Oct  8 13:01 instructions
-rw-r--r-- 1 hacker hacker   0 Oct  8 13:00 my
-rw-r--r-- 1 hacker hacker  93 Oct  8 13:01 myflag
lrwxrwxrwx 1 hacker hacker   5 Oct  6 14:27 not-the-flag -> /flag
-rw-r--r-- 1 root   hacker  77 Oct  8 16:34 pwn
-rw-r--r-- 1 root   hacker  77 Oct  8 16:44 pwn_op
-rw-r--r-- 1 root   hacker  58 Oct  2 05:34 s
-rw-r--r-- 1 hacker hacker  46 Oct  8 18:05 tee
-rw-r--r-- 1 hacker hacker 435 Oct  8 12:35 the-flag
```
I noticed that I needed to change ownership of not-the-flag because it was pointing to `/flag` . so I did the same and then catted it:
```
hacker@permissions~changing-file-ownership:~$ chown hacker not-the-flag
hacker@permissions~changing-file-ownership:~$ cat not-the-flag
pwn.college{MknADwgCJwDR9uuw4Nqb8sVJirI.dFTM2QDLwIzN0czW}
```

## Groups and Files
group = collection of many users     
a user can be part of many groups    
id = command that lets user see the groups they are part of    
chgrp = command to change group of user

first I used `ls-l /flag` to see  permissions of /flag

```
hacker@permissions~groups-and-files:~$ ls -l /flag
-r--r----- 1 root root 58 Oct 13 06:00 /flag
```
as instructed, I changed the group of the file to hacker and then catted it to get the flag:
```
hacker@permissions~groups-and-files:~$ chgrp hacker not-the-flag
hacker@permissions~groups-and-files:~$ cat not-the-flag
pwn.college{8KFG_2NzHcqH95lEZILyunofsA1.dFzNyUDLwIzN0czW}
```

## Fun with Groups Names

for this challenge, I firstused the id command to see which group hacker belongs to:
```
hacker@permissions~fun-with-groups-names:~$ id hacker
uid=1000(hacker) gid=1000(grp8251) groups=1000(grp8251)
```
I then used ls -l with ``/flag as the argument to find /flag permissions:
```
hacker@permissions~fun-with-groups-names:~$ ls -l /flag
-r--r----- 1 root root 58 Oct 13 05:59 /flag
```
after this, I changed the group of not-the-flag to grp8251 using `chgrp` and then used the `cat` command:
```
hacker@permissions~fun-with-groups-names:~$ chgrp grp8251 not-the-flag
hacker@permissions~fun-with-groups-names:~$ cat not-the-flag
pwn.college{wUqk-KIc7-9rMZuuG0Yxq-qpuMy.dJzNyUDLwIzN0czW}
```

## Changing Permissions
