# UNTANGLING USERS

## Becoming Root with su

su = switch user command, it has the ability to run as the root therefore, it can start a root shell.   
it will ask for a password from the user before allowing them to use the terminal as the root.    

since the root password was given for this challenge, all I did was use `su` and then enter the password.
```
hacker@users~becoming-root-with-su:~$ su
Password:
root@users~becoming-root-with-su:/home/hacker# cat /flag
pwn.college{86KRuGniF_FjjTUs5_uzL00FrpB.dVTN0UDLwIzN0czW}
```

## Other Users with su
without an argument, su switches to the root.     
but if another user is given as an argument for su, we can switch to that user too.    

to switch to zardus, I entered it as an argument to su and then ran /challenge/run.
```
hacker@users~other-users-with-su:~$ su zardus
Password:
zardus@users~other-users-with-su:/home/hacker$ /challenge/run
Congratulations, you have become Zardus! Here is your flag:
pwn.college{ctoCeIDMR1QBym7pWRY7xbeQFvf.dZTN0UDLwIzN0czW}
```

## Cracking Passwords   

passwords of different users are stored in `/etc/shadow`    
these passwords are encrypted via hashing and then stored.    
to crack use: `john /path_of_password`

first I cracked the password using the john command
```
hacker@users~cracking-passwords:~$ john /challenge/shadow-leak
Created directory: /home/hacker/.john
Loaded 1 password hash (crypt, generic crypt(3) [?/64])
Press 'q' or Ctrl-C to abort, almost any other key for status
aardvark         (zardus)
1g 0:00:00:20 100% 2/3 0.04921g/s 286.5p/s 286.5c/s 286.5C/s Johnson..buzz
Use the "--show" option to display all of the cracked passwords reliably
Session completed
```
I understood that aardvark was the password, so I used it for switching to zardus and then ran /challenge/run
```
hacker@users~cracking-passwords:~$ su zardus
Password:
zardus@users~cracking-passwords:/home/hacker$ /challenge/run
Congratulations, you have become Zardus! Here is your flag:
pwn.college{gsUXSw1cVqDhHe0JL06XPrHV28t.ddTN0UDLwIzN0czW}
```

## Using sudo  

sudo = superuser do, is a command used to run a command as the root specifically     
here, we don't completely switch users, instead we run the command as root temporarily   

since the flag is always in /flag I catted it using sudo:
```
hacker@users~using-sudo:~$ cat /flag
cat: /flag: Permission denied
hacker@users~using-sudo:~$ sudo cat /flag
pwn.college{AaXrjcQpCsfkJ0cmu3KBzEQIhGU.dhTN0UDLwIzN0czW}
```
