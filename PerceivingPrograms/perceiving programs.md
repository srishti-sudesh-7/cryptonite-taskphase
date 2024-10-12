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
I noticed that I needed to change ownership of not-the-flag because it was pointing to `/flag. so I did the same and then catted it:
```
hacker@permissions~changing-file-ownership:~$ chown hacker not-the-flag
hacker@permissions~changing-file-ownership:~$ cat not-the-flag
pwn.college{MknADwgCJwDR9uuw4Nqb8sVJirI.dFTM2QDLwIzN0czW}
```


