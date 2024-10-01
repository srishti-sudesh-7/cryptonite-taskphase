# PONDERING PATHS 
## The Root

in order to get the flag, I needed to reach a program called pwn which was in /.   
*note: directories start from / ie it is the root of the filesystem*    
to reach any program, all we need to do is put in its path. so that's what I did.     
since we know that pwn is in /, its path becomes: `/pwn`

on typing /pwn, I got the flag: 
`pwn.college{kTSRHi16X8q0H5NAjsEm1hIrghr.dhzN5QDLwIzN0czW}`



## Program and Absolute Paths

absolute path: a path that starts from the root directory     

here to get the flag, I needed to reach the program called "run" which was inside the challenge directory, which in turn is inside the root directory /.    
so the path I used is `/challenge/run`

flag: 
`pwn.college{8qKcb4rm02rP1LJbhOy2pwMJIft.dVDN1QDLwIzN0czW}`

## Position Thyself
at first I typed in `/challenge/run` but i got an error. 

it said that I had to change directory to `/usr/share/zoneinfo/posix/Asia` directory       
once I did that, I tried entering the first path I entered and this time it worked!

```````
hacker@paths~position-thy-self:~$ cd /challenge/run   
ssh-entrypoint: cd: /challenge/run: Not a directory
hacker@paths~position-thy-self:~$ /challenge/run
Incorrect...
You are not currently in the /usr/share/zoneinfo/posix/Asia directory.
Please use the `cd` utility to change directory appropriately.
hacker@paths~position-thy-self:~$ cd /usr/share/zoneinfo/posix/Asia
hacker@paths~position-thy-self:/usr/share/zoneinfo/posix/Asia$ /challenge/run
Correct!!!
/challenge/run is an absolute path, invoked from the right directory!
Here is your flag:
pwn.college{Y4K4l34JRaa1-NONTNp4oL82HGx.dZDN1QDLwIzN0czW}
`````````



## Position Elsewhere

here, the logic is the same as _Position Thyself._ 

I tried `/challenge/run` first, which did not work. It showed me that i needed to reach the `/usr/bin` directory, for which i used the cd command.
on rerunning the initial command, I got the desired result.

````````
hacker@paths~position-elsewhere:/$ /challenge/run
Incorrect...
You are not currently in the /usr/bin directory.
Please use the `cd` utility to change directory appropriately.
hacker@paths~position-elsewhere:/$ cd /usr/bin
hacker@paths~position-elsewhere:/usr/bin$ /challenge/run
Correct!!!
/challenge/run is an absolute path, invoked from the right directory!
Here is your flag:
pwn.college{kghhw7kO8uRBeYzjyuJDL2iQ6el.ddDN1QDLwIzN0czW}

``````````````


## Position Yet Elsewhere
this also uses the same logic as the previous two.

on trying `/challenge/run` I was directed to the /var/log directory, from where I reran my first command and got the output.

``````````
hacker@paths~position-yet-elsewhere:~$ /challenge/run
Incorrect...
You are not currently in the /var/log directory.
Please use the `cd` utility to change directory appropriately.
hacker@paths~position-yet-elsewhere:~$ cd /var/log
hacker@paths~position-yet-elsewhere:/var/log$ /challenge/run
Correct!!!
/challenge/run is an absolute path, invoked from the right directory!
Here is your flag:
pwn.college{Ao5LYsnI_oQn_1IttthRwJoB56k.dhDN1QDLwIzN0czW}
`````````````


## Implicit Relative Paths, from /

relative path: path not beginning at root ie it is taken wrt the cwd (current working directory).

on trying `/challenge/run`, the system prompted me to go the the root / directory. I did this using the `cd` command. using the hint given (relative path begins with c), I figured out that it must be just `challenge/run` since we're already inside the / directory. 

``````````
hacker@paths~implicit-relative-paths-from-:~$ /challenge/run
Incorrect...
You are not currently in the / directory.
Please use the `cd` utility to change directory appropriately.
hacker@paths~implicit-relative-paths-from-:~$ cd /
hacker@paths~implicit-relative-paths-from-:/$ challenge/run
Correct!!!
challenge/run is a relative path, invoked from the right directory!
Here is your flag:
pwn.college{4XYtm_pY0-ilpsPXTlTOEfhgsAI.dlDN1QDLwIzN0czW}


`````````````


## Explicit Relative Paths, from /

learnt that `.` and `..` are implicit and can be referenced in paths. they refer to the same directory itself.

once I ran the `challenge/run` command (while cwd is /), the message said that the relative path must being with a `.`, therefore I used `./challenge/run`



````
srishti_7@DESKTOP-DEOL9I4:~$ ssh -i ./key hacker@dojo.pwn.college
Connected!
hacker@paths~explicit-relative-paths-from-:~$ cd /
hacker@paths~explicit-relative-paths-from-:/$ challenge/run
Incorrect...
This challenge must be called with a relative path that explicitly starts with a `.`!
hacker@paths~explicit-relative-paths-from-:/$ ./challenge/run
Correct!!!
./challenge/run is a relative path, invoked from the right directory!
Here is your flag:
pwn.college{Q_QABb8XIZgEWWngpIrT8eSy9N0.dBTN1QDLwIzN0czW}
````````

##
