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

