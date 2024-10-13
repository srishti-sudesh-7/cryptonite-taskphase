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
hacker@permissions~groups-and-files:~$ chgrp hacker /flag
hacker@permissions~groups-and-files:~$ cat /flag
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
hacker@permissions~fun-with-groups-names:~$ chgrp grp8251 /flag
hacker@permissions~fun-with-groups-names:~$ cat /flag
pwn.college{wUqk-KIc7-9rMZuuG0Yxq-qpuMy.dJzNyUDLwIzN0czW}
```

## Changing Permissions

when we `ls -l` a file, we get 10 characters denoting the permissions. here:   
first character represents file type. after that, three sets of three characters each are present.   
first set - permissions of owning user      
second set - permissions of owning group     
third set - permissions of other users and groups      
the characters with their meanings are given below:
- r = they can read the file or list the directory
- w = they can modify a file or create/delete file in directory
- x = they can execute the file or enter the directory
- dash(-) = nothing

  
chmod is a command by which we can change the permissions of a file
format: chmod [options] MODE file    
here MODE is has the format who±what (who = user/group/others, what=r/w/x, + -s add, - is remove... here ± only add/remove permissions, they wont overwrite the already existing ones)   

for this task, I first used `ls-l` to see the permissions of /flag.
```
hacker@permissions~changing-permissions:~$ ls -l /flag
-r-------- 1 root root 58 Oct 13 10:09 /flag
```
since I am not the owner, I made it so that all others can read the program by using `chmod`:
```
hacker@permissions~changing-permissions:~$ chmod o+r /flag
```
then I did `cat /flag` and got the flag:
```
hacker@permissions~changing-permissions:~$ cat /flag
pwn.college{smN3FVABiVU2PyOjoCI5fYBmfSi.dNzNyUDLwIzN0czW}
```

## Executable Files

here, I first listed the permissions of /challenge/run:
```
hacker@permissions~executable-files:~$ ls -l /challenge/run
-r--r--r-- 1 hacker hacker 32 Jul  4 06:37 /challenge/run
```
to make it executable by everyone I used chmod with the mode ugo+x and then executed the program:
```
hacker@permissions~executable-files:~$ chmod ugo+x /challenge/run
hacker@permissions~executable-files:~$ /challenge/run
Successful execution! Here is your flag:
pwn.college{s06mG4Gb9mvN_T6iFMhr6aNPVBK.dJTM2QDLwIzN0czW}
```
## Permissions Tweaking Practice

I first ran `/challenge/run` to get the instructions:
```
hacker@permissions~permission-tweaking-practice:~$ /challenge/run
Round 0 (of 8)!

Current permissions of "/challenge/pwn": rw-r--r--
* the user does have read permissions
* the user does have write permissions
- the user doesn't have execute permissions
* the group does have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
* the world does have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions

Needed permissions of "/challenge/pwn": -w-------
- the user doesn't have read permissions
* the user does have write permissions
- the user doesn't have execute permissions
- the group doesn't have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
- the world doesn't have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions
```
I then removed the reading permission from u, g and o:
```
hacker@permissions~permission-tweaking-practice:~$ chmod ugo-r /challenge/pwn
You set the correct permissions!
Round 1 (of 8)!

Current permissions of "/challenge/pwn": -w-------
- the user doesn't have read permissions
* the user does have write permissions
- the user doesn't have execute permissions
- the group doesn't have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
- the world doesn't have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions

Needed permissions of "/challenge/pwn": -w-r-----
- the user doesn't have read permissions
* the user does have write permissions
- the user doesn't have execute permissions
* the group does have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
- the world doesn't have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions
```
then I added reading permission to group:
```
hacker@permissions~permission-tweaking-practice:~$ chmod g+r /challenge/
pwn
You set the correct permissions!
Round 2 (of 8)!

Current permissions of "/challenge/pwn": -w-r-----
- the user doesn't have read permissions
* the user does have write permissions
- the user doesn't have execute permissions
* the group does have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
- the world doesn't have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions

Needed permissions of "/challenge/pwn": -w-r-x---
- the user doesn't have read permissions
* the user does have write permissions
- the user doesn't have execute permissions
* the group does have read permissions
- the group doesn't have write permissions
* the group does have execute permissions
- the world doesn't have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions
```
then I added executing permission to group:
```
hacker@permissions~permission-tweaking-practice:~$ chmod g+x /challenge/
pwn
You set the correct permissions!
Round 3 (of 8)!

Current permissions of "/challenge/pwn": -w-r-x---
- the user doesn't have read permissions
* the user does have write permissions
- the user doesn't have execute permissions
* the group does have read permissions
- the group doesn't have write permissions
* the group does have execute permissions
- the world doesn't have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions

Needed permissions of "/challenge/pwn": -wxrwx-wx
- the user doesn't have read permissions
* the user does have write permissions
* the user does have execute permissions
* the group does have read permissions
* the group does have write permissions
* the group does have execute permissions
- the world doesn't have read permissions
* the world does have write permissions
* the world does have execute permissions
```
then I added writing and exuting permissions to user, group and world:
```
hacker@permissions~permission-tweaking-practice:~$ chmod ugo+wx /challen
ge/pwn
You set the correct permissions!
Round 4 (of 8)!

Current permissions of "/challenge/pwn": -wxrwx-wx
- the user doesn't have read permissions
* the user does have write permissions
* the user does have execute permissions
* the group does have read permissions
* the group does have write permissions
* the group does have execute permissions
- the world doesn't have read permissions
* the world does have write permissions
* the world does have execute permissions

Needed permissions of "/challenge/pwn": -wxrwx-w-
- the user doesn't have read permissions
* the user does have write permissions
* the user does have execute permissions
* the group does have read permissions
* the group does have write permissions
* the group does have execute permissions
- the world doesn't have read permissions
* the world does have write permissions
- the world doesn't have execute permissions
```
now I had to remove execute permission from others:
```
hacker@permissions~permission-tweaking-practice:~$ chmod o-x /challenge/
pwn
You set the correct permissions!
Round 5 (of 8)!

Current permissions of "/challenge/pwn": -wxrwx-w-
- the user doesn't have read permissions
* the user does have write permissions
* the user does have execute permissions
* the group does have read permissions
* the group does have write permissions
* the group does have execute permissions
- the world doesn't have read permissions
* the world does have write permissions
- the world doesn't have execute permissions

Needed permissions of "/challenge/pwn": -wx-w--w-
- the user doesn't have read permissions
* the user does have write permissions
* the user does have execute permissions
- the group doesn't have read permissions
* the group does have write permissions
- the group doesn't have execute permissions
- the world doesn't have read permissions
* the world does have write permissions
- the world doesn't have execute permissions
```
then,  I removed permissions for reading and executing from group:
```
hacker@permissions~permission-tweaking-practice:~$ chmod g-rx /challenge
/pwn
You set the correct permissions!
Round 6 (of 8)!

Current permissions of "/challenge/pwn": -wx-w--w-
- the user doesn't have read permissions
* the user does have write permissions
* the user does have execute permissions
- the group doesn't have read permissions
* the group does have write permissions
- the group doesn't have execute permissions
- the world doesn't have read permissions
* the world does have write permissions
- the world doesn't have execute permissions

Needed permissions of "/challenge/pwn": -wx-wx-w-
- the user doesn't have read permissions
* the user does have write permissions
* the user does have execute permissions
- the group doesn't have read permissions
* the group does have write permissions
* the group does have execute permissions
- the world doesn't have read permissions
* the world does have write permissions
- the world doesn't have execute permissions
```
then I added executive permissions for group:
```
hacker@permissions~permission-tweaking-practice:~$ chmod g+x /challenge/
pwn
You set the correct permissions!
Round 7 (of 8)!

Current permissions of "/challenge/pwn": -wx-wx-w-
- the user doesn't have read permissions
* the user does have write permissions
* the user does have execute permissions
- the group doesn't have read permissions
* the group does have write permissions
* the group does have execute permissions
- the world doesn't have read permissions
* the world does have write permissions
- the world doesn't have execute permissions

Needed permissions of "/challenge/pwn": rwx-wxrw-
* the user does have read permissions
* the user does have write permissions
* the user does have execute permissions
- the group doesn't have read permissions
* the group does have write permissions
* the group does have execute permissions
* the world does have read permissions
* the world does have write permissions
- the world doesn't have execute permissions
```
Then I added reading permissions to both user and world:
```
hacker@permissions~permission-tweaking-practice:~$ chmod uo+r /challenge
/pwn
You set the correct permissions!
You've solved all 8 rounds! I have changed the ownership
of the /flag file so that you can 'chmod' it. You won't be able to read
it until you make it readable with chmod!

Current permissions of "/flag": ---------
- the user doesn't have read permissions
- the user doesn't have write permissions
- the user doesn't have execute permissions
- the group doesn't have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
- the world doesn't have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions
```

to make /flag readable, I gave the permissions to user, group and others. then I was able to read it:
```
hacker@permissions~permission-tweaking-practice:~$  chmod ugo+r /flag
hacker@permissions~permission-tweaking-practice:~$ cat /flag
pwn.college{gkLmzCI8pToREw1QsyCEPNKZyu6.dBTM2QDLwIzN0czW}
```

## Permissions Setting Practice    
when setting MODE while using `chmod`, if we want to overwrite old permissions, we use =.
for example if a file /files has permissions -rwx------ and we use command `chmod u=r /files` then its permission gets modified into -r--------      
we can do multiple modifications at once using ,      

first I ran /challenge/run:
```
hacker@permissions~permissions-setting-practice:~$ /challenge/run
Round 0 (of 8)!

Current permissions of "/challenge/pwn": rw-r--r--
* the user does have read permissions
* the user does have write permissions
- the user doesn't have execute permissions
* the group does have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
* the world does have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions

Needed permissions of "/challenge/pwn": r---w-r-x
* the user does have read permissions
- the user doesn't have write permissions
- the user doesn't have execute permissions
- the group doesn't have read permissions
* the group does have write permissions
- the group doesn't have execute permissions
* the world does have read permissions
- the world doesn't have write permissions
* the world does have execute permissions
```
I needed to give user only reading permission, give group only writing permissions and add executing permissions to others:
```
hacker@permissions~permissions-setting-practice:~$ chmod u=r,g=w,o+x /challenge/pwn
You set the correct permissions!
Round 1 (of 8)!

Current permissions of "/challenge/pwn": r---w-r-x
* the user does have read permissions
- the user doesn't have write permissions
- the user doesn't have execute permissions
- the group doesn't have read permissions
* the group does have write permissions
- the group doesn't have execute permissions
* the world does have read permissions
- the world doesn't have write permissions
* the world does have execute permissions

Needed permissions of "/challenge/pwn": r-x------
* the user does have read permissions
- the user doesn't have write permissions
* the user does have execute permissions
- the group doesn't have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
- the world doesn't have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions
```
so I added execute perm. to user and set perms. of world and group to none

```
hacker@permissions~permissions-setting-practice:~$ chmod u+x,go=- /challenge/pwn
You set the correct permissions!
Round 2 (of 8)!

Current permissions of "/challenge/pwn": r-x------
* the user does have read permissions
- the user doesn't have write permissions
* the user does have execute permissions
- the group doesn't have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
- the world doesn't have read permissions
- the world doesn't have write permissions
- the world doesn't have execute permissions

Needed permissions of "/challenge/pwn": r----xrwx
* the user does have read permissions
- the user doesn't have write permissions
- the user doesn't have execute permissions
- the group doesn't have read permissions
- the group doesn't have write permissions
* the group does have execute permissions
* the world does have read permissions
* the world does have write permissions
* the world does have execute permissions
```
then I removed x from user, and set group and world permissions as specified in the instructions:
```
hacker@permissions~permissions-setting-practice:~$ chmod u-x,g=x,o=rwx /challenge/pwn
You set the correct permissions!
Round 3 (of 8)!

Current permissions of "/challenge/pwn": r----xrwx
* the user does have read permissions
- the user doesn't have write permissions
- the user doesn't have execute permissions
- the group doesn't have read permissions
- the group doesn't have write permissions
* the group does have execute permissions
* the world does have read permissions
* the world does have write permissions
* the world does have execute permissions

Needed permissions of "/challenge/pwn": -wxr--rw-
- the user doesn't have read permissions
* the user does have write permissions
* the user does have execute permissions
* the group does have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
* the world does have read permissions
* the world does have write permissions
- the world doesn't have execute permissions
```

```
hacker@permissions~permissions-setting-practice:~$ chmod u=wx,g=r,o-x /challenge/pwn
You set the correct permissions!
Round 4 (of 8)!

Current permissions of "/challenge/pwn": -wxr--rw-
- the user doesn't have read permissions
* the user does have write permissions
* the user does have execute permissions
* the group does have read permissions
- the group doesn't have write permissions
- the group doesn't have execute permissions
* the world does have read permissions
* the world does have write permissions
- the world doesn't have execute permissions

Needed permissions of "/challenge/pwn": -----xrwx
- the user doesn't have read permissions
- the user doesn't have write permissions
- the user doesn't have execute permissions
- the group doesn't have read permissions
- the group doesn't have write permissions
* the group does have execute permissions
* the world does have read permissions
* the world does have write permissions
* the world does have execute permissions
```

