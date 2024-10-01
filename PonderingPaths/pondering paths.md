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









##
