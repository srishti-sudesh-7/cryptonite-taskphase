# FILE GLOBBING
globbing is a method to refer to files without typing their whole path

## Matching with *

* = used to match already existing filenames (will match anything except / or leading .)

this one was direct. I used the exact syntax given in the instructions to find `/challenge` and then used the same argument `/c*` while I used the command `cd`.

```
hacker@globbing~matching-with-:~$ echo look: /c*
look: /challenge
hacker@globbing~matching-with-:~$ cd /c*
hacker@globbing~matching-with-:/challenge$ /challenge/run
You ran me with the working directory of /challenge! Here is your flag:
pwn.college{0UcmaKQcMU5RAn6baJ3njd3CP5J.dFjM4QDLwIzN0czW}
```

## Matching with ?

? - during search, it will replace only one character. can use multiple ? for multiple characters.

here I replaced the c and l with ? to get the flag:


```
hacker@globbing~matching-with-:~$ echo look: /?ha??enge
This challenge resets your working directory to /home/hacker unless you change
directory properly...
look: /challenge
This challenge resets your working directory to /home/hacker unless you change
directory properly...
hacker@globbing~matching-with-:~$ cd /?ha??enge
hacker@globbing~matching-with-:/challenge$ /challenge/run
You ran me with the working directory of /challenge! Here is your flag:
pwn.college{c8k_jK2hgksL_SCMbCehExMGj6o.dJjM4QDLwIzN0czW}
```

## Matching with []

[xyz] = matches for characters x, y, z

first I change directory to `/challenge/files` and listed its contents:

```
hacker@globbing~matching-with-:~$ cd /challenge/files
hacker@globbing~matching-with-:/challenge/files$ ls
file_a  file_d  file_g  file_j  file_m  file_p  file_s  file_v  file_y
file_b  file_e  file_h  file_k  file_n  file_q  file_t  file_w  file_z
file_c  file_f  file_i  file_l  file_o  file_r  file_u  file_x
```

after this I ran `/challenge/run` using the argument `file_[bash]` and got the flag

```
hacker@globbing~matching-with-:/challenge/files$ /challenge/run file_[bash]
You got it! Here is your flag!
pwn.college{QBD0r6iaPixYqnBU8iWROYOWt-b.dNjM4QDLwIzN0czW}
```

## Matching paths with []

to do this challenge, first I needed to figure out the right argument, which I did using the `echo` command: 

```
hacker@globbing~matching-paths-with-:~$ echo look: /challenge/files/file_[bash]
look: /challenge/files/file_a /challenge/files/file_b /challenge/files/file_h /challenge/files/file_s
```
then I used the `/challnge/run` command with this argument to get the flag
```
hacker@globbing~matching-paths-with-:~$ /challenge/run /challenge/files/file_[bash]
You got it! Here is your flag!
pwn.college{w48bd3fU4vw4uYujHsYg4Czwdja.dRjM4QDLwIzN0czW}
```


## Mixing Globs

I first went to the `/challenge/files` directory and listed its contents
```
hacker@globbing~mixing-globs:~$ cd /challenge/files
hacker@globbing~mixing-globs:/challenge/files$ ls
amazing      fantastic   kind        pwning     uplifting   zesty
beautiful    great       laughing    queenly    victorious
challenging  happy       magical     radiant    wonderful
delightful   incredible  nice        splendid   xenial
educational  jovial      optimistic  thrilling  youthful
```
I noticed they were in alphabetical order so each word had a unique intial.

when i tried to read them in the following manner, it was successful:
```
hacker@globbing~mixing-globs:/challenge/files$ echo look: /challenge/files/c* e* p*
look: /challenge/files/challenging educational pwning
```

however this method was not working with the `/challenge/run` command:
```
hacker@globbing~mixing-globs:/challenge/files$ /challenge/run c* e* p*
Error: you called this command with more than 1 argument (pre-globbing)! Please
call me with one argument.
```
I realised I can't use spaces as it can take only one argument. so I tried it with no spaces:
```
hacker@globbing~mixing-globs:/challenge/files$ /challenge/run c*e*p*
Error: you did not use a square bracket glob...
```
I then tried it with [] but that was more than 6 characters:
```
hacker@globbing~mixing-globs:/challenge/files$ /challenge/run [c*e*p*]
Error: your argument is too long! It must be 6 characters or less.
```
to reduce the number of characters, I used the * outside the brackets and this method worked.
```
hacker@globbing~mixing-globs:/challenge/files$ /challenge/run [cep]*
You got it! Here is your flag!
pwn.college{gSkUpCdP602df6LYdd0QmWJvcBL.dVjM4QDLwIzN0czW}
```

## Exclusionary Globbing

[^xyz] or [!xyz] = it excludes x, y, and z during matching. 

I first changed directory to `/challenge/files`.      
here I used ! as the first characer within [] followed by pwn. 
I also added * outside the brackets to make sure the complete words are matched.
```
hacker@globbing~exclusionary-globbing:/challenge/files$ /challenge/run [!pwn]*
You got it! Here is your flag!
pwn.college{oZT73xZCN3cj1Wegj-JhbFeZuui.dZjM4QDLwIzN0czW}
hacker@globbing~exclusionary-globbing:/challenge/files$
```
