# Practicing Piping

## Redirecting Output
> = used to redirect output of a command to another file

here I redirected the output of `echo PWN` to a file named `COLLEGE`.

```
hacker@piping~redirecting-output:~$ echo PWN > COLLEGE
Correct! You successfully redirected 'PWN' to the file 'COLLEGE'! Here is your
flag:
pwn.college{gnOyFKYvHRBuxEwfhVy8Cx5ms0y.dRjN1QDLwIzN0czW}
```

## Redirecting More Output

first, I redirected the output `/challenge/run` to `myflag`:

```
hacker@piping~redirecting-more-output:~$ /challenge/run > myflag
[INFO] WELCOME! This challenge makes the following asks of you:
[INFO] - the challenge will check that output is redirected to a specific file path : myflag
[INFO] - the challenge will output a reward file if all the tests pass : /flag

[HYPE] ONWARDS TO GREATNESS!

[INFO] This challenge will perform a bunch of checks.
[INFO] If you pass these checks, you will receive the /flag file.

[TEST] You should have redirected my stdout to a file called myflag. Checking...

[PASS] The file at the other end of my stdout looks okay!
[PASS] Success! You have satisfied all execution requirements.
```
after this all I had to do was concatenate `myflag`
````
hacker@piping~redirecting-more-output:~$ cat myflag

[FLAG] Here is your flag:
[FLAG] pwn.college{sG7M5JOrgJogzKthibb6hrbdY5e.dVjN1QDLwIzN0czW}
````

## Appending Output
>> = attaches the output of a command to the file (used when we need to attach outputs of multiple commands)

I started by redirect output of `/challenge/run` to the file mentioned in the instructions.
```
hacker@piping~appending-output:~$ /challenge/run > /home/hacker/the-flag
[INFO] WELCOME! This challenge makes the following asks of you:
[INFO] - the challenge will check that output is redirected to a specific file path : /home/hacker/the-flag

[HYPE] ONWARDS TO GREATNESS!

[INFO] This challenge will perform a bunch of checks.
[INFO] Good luck!

[TEST] You should have redirected my stdout to a file called /home/hacker/the-flag. Checking...

[HINT] File descriptors are inherited from the parent, unless the FD_CLOEXEC is set by the parent on the file descriptor.
[HINT] For security reasons, some programs, such as python, do this by default in certain cases. Be careful if you are
[HINT] creating and trying to pass in FDs in python.

[PASS] The file at the other end of my stdout looks okay!
[PASS] Success! You have satisfied all execution requirements.
I will write the flag in two parts to the file /home/hacker/the-flag! I'll do
the first write directly to the file, and the second write, I'll do to stdout
(if it's pointing at the file). If you redirect the output in append mode, the
second write will append to (rather than overwrite) the first write, and you'll
get the whole flag!
```
to get the second half, I repeated the same process except that instead of overwriting the first half, I attached the second half to the first half by using `>>`
```
hacker@piping~appending-output:~$ /challenge/run >> /home/hacker/the-flag
[INFO] WELCOME! This challenge makes the following asks of you:
[INFO] - the challenge will check that output is redirected to a specific file path : /home/hacker/the-flag
[HYPE] ONWARDS TO GREATNESS!

[INFO] This challenge will perform a bunch of checks.
[INFO] Good luck!

[TEST] You should have redirected my stdout to a file called /home/hacker/the-flag. Checking...

[HINT] File descriptors are inherited from the parent, unless the FD_CLOEXEC is set by the parent on the file descriptor.
[HINT] For security reasons, some programs, such as python, do this by default in certain cases. Be careful if you are
[HINT] creating and trying to pass in FDs in python.

[PASS] The file at the other end of my stdout looks okay!
[PASS] Success! You have satisfied all execution requirements.
I will write the flag in two parts to the file /home/hacker/the-flag! I'll do
the first write directly to the file, and the second write, I'll do to stdout
(if it's pointing at the file). If you redirect the output in append mode, the
second write will append to (rather than overwrite) the first write, and you'll
get the whole flag!
```

then I just had to `cat` the file.

```
hacker@piping~appending-output:~$ cat /home/hacker/the-flag
 |
\|/ This is the first half:
 v
pwn.college{M0VNMi9RnPkSAOSI051N4oVLpVY.ddDM5QDLwIzN0czW}
                              ^
     that is the second half /|\
                              |

If you only see the second half above, you redirected in *truncate* mode (>)
rather than *append* mode (>>), and so the write of the second half to stdout
overwrote the initial write of the first half directly to the file. Try append
mode!

```

## Redirecting Errors

File Descriptor (FD) number is basically a number assigned to each type of channel, through which the user can specify which channel of communication is to be used.   
> is equivalent to 1 > (stdout)
note: 0=stdin, 1=stdout, 2=stderr

here all I had to do was redirect the flag from `/challenge/run` to `myflag` and its errors to `instructions`
```
hacker@piping~redirecting-errors:~$ /challenge/run 1> myflag 2> instructions
hacker@piping~redirecting-errors:~$ cat myflag

[FLAG] Here is your flag:
[FLAG] pwn.college{MJ1iOsiG8S8qWBBEeZeiU-LJy5N.ddjN1QDLwIzN0czW}
```
## Redirecting Input

< is used to redirect input to a program

this one was simple, the instructions said PWN would have to containt COLLEGE and then /chalenge/run would have to be redirected to PWN, as shown below: 

```
hacker@piping~redirecting-input:~$ echo COLLEGE > PWN
hacker@piping~redirecting-input:~$ /challenge/run < PWN
Reading from standard input...
Correct! You have redirected the PWN file into my standard input, and I read
the value 'COLLEGE' out of it!
Here is your flag:
pwn.college{g99E5pfZ64aRydNcypdCi7t-a1E.dBzN1QDLwIzN0czW}
```

## Grepping Stored Results

first I redirected the output of `/challenge/run` as instructed.
```
hacker@piping~grepping-stored-results:~$ /challenge/run >  /tmp/data.txt
[INFO] WELCOME! This challenge makes the following asks of you:
[INFO] - the challenge will check that output is redirected to a specific file path : /tmp/data.txt
[INFO] - the challenge will output a reward file if all the tests pass : /challenge/.data.txt

[HYPE] ONWARDS TO GREATNESS!

[INFO] This challenge will perform a bunch of checks.
[INFO] If you pass these checks, you will receive the /challenge/.data.txt file.

[TEST] You should have redirected my stdout to a file called /tmp/data.txt. Checking...

[HINT] File descriptors are inherited from the parent, unless the FD_CLOEXEC is set by the parent on the file descriptor.
[HINT] For security reasons, some programs, such as python, do this by default in certain cases. Be careful if you are
[HINT] creating and trying to pass in FDs in python.

[PASS] The file at the other end of my stdout looks okay!
[PASS] Success! You have satisfied all execution requirements.
```
after that I grepped for the keyword `pwn` and got the flag:
```
hacker@piping~grepping-stored-results:~$ grep pwn /tmp/data.txt
pwned
pwn
pwning
pwns
pwn.college{sEhWLcs9ExFE2qA2wkK650lJvc3.dhTM4QDLwIzN0czW}
```

## Grepping Live Output
| = pipe operator, pipes stdout from left side to stdin of command on the right side    

this challenge was pretty straightforward. 
I used the pipe operator to pipe the outputs of `/challenge/run` to the input of the `grep` command and used the keyword pwn along with it.
```
hacker@piping~grepping-live-output:~$ /challenge/run | grep pwn
[INFO] WELCOME! This challenge makes the following asks of you:
[INFO] - the challenge checks for a specific process at the other end of stdout : grep
[INFO] - the challenge will output a reward file if all the tests pass : /challenge/.data.txt

[HYPE] ONWARDS TO GREATNESS!

[INFO] This challenge will perform a bunch of checks.
[INFO] If you pass these checks, you will receive the /challenge/.data.txt file.

[TEST] You should have redirected my stdout to another process. Checking...
[TEST] Performing checks on that process!

[INFO] The process' executable is /nix/store/xpq4yhadyhazkcsggmqd7rsgvxb3kjy4-gnugrep-3.11/bin/grep.
[INFO] This might be different than expected because of symbolic links (for example, from /usr/bin/python to /usr/bin/python3 to /usr/bin/python3.8).
[INFO] To pass the checks, the executable must be grep.

[PASS] You have passed the checks on the process on the other end of my stdout!
[PASS] Success! You have satisfied all execution requirements.
pwn.college{UZv9mkSILnURVPy6taLqBRIJOZ7.dlTM4QDLwIzN0czW}
pwns
pwn
pwned
pwning
```
## Grepping Errors

| can only pipe standard outputs ie it won't function for standard errors, so if we use a `>&` operator first, then followed by |, we can first redirect the stderr to stdout and then use the | operator normally.

Here I first redirected the stderr of `/challenge/run` to stdout and then used `grep` using |


```
hacker@piping~grepping-errors:~$ /challenge/run 2>& 1 | grep pwn
[INFO] WELCOME! This challenge makes the following asks of you:
[INFO] - the challenge checks for a specific process at the other end of stderr : grep
[INFO] - the challenge will output a reward file if all the tests pass : /challenge/.data.txt

[HYPE] ONWARDS TO GREATNESS!

[INFO] This challenge will perform a bunch of checks.
[INFO] If you pass these checks, you will receive the /challenge/.data.txt file.

[TEST] You should have redirected my stderr to another process. Checking...
[TEST] Performing checks on that process!

[INFO] The process' executable is /nix/store/xpq4yhadyhazkcsggmqd7rsgvxb3kjy4-gnugrep-3.11/bin/grep.
[INFO] This might be different than expected because of symbolic links (for example, from /usr/bin/python to /usr/bin/python3 to /usr/bin/python3.8).
[INFO] To pass the checks, the executable must be grep.

[PASS] You have passed the checks on the process on the other end of my stderr!
[PASS] Success! You have satisfied all execution requirements.
pwn.college{MPQbH6rO08M8n3FfgcZdaKezUCX.dVDM5QDLwIzN0czW}
pwn
pwning
pwned
pwns
```

## Duplicating Piped Data with Tee
tee = command to duplicate the data that's being piped.

at first, I was confused on how to use the `tee` command but the second example in the website helped me realise that I needed to make a temporary file `pwn_op` to debug it:

```
hacker@piping~duplicating-piped-data-with-tee:~$ /challenge/pwn | tee pwn_op  | /challenge/college
Processing...
WARNING: you are overwriting file pwn_op with tee's output...

The input to 'college' does not contain the correct secret code! This code
should be provided by the 'pwn' command. HINT: use 'tee' to intercept the
output of 'pwn' and figure out what the code needs to be.
```
then I used `cat` to see what was going wrong:
```
hacker@piping~duplicating-piped-data-with-tee:~$ cat pwn_op
Usage: /challenge/pwn --secret [SECRET_ARG]

SECRET_ARG should be "8Ktjvrco"
```
this gave me the correct usage of the `/challenge/run` command and now all that was left was to pipe the right command to `/challenge/college`
```
hacker@piping~duplicating-piped-data-with-tee:~$ /challenge/pwn --secret 8Ktjvrco | /challenge/college
Processing...
Correct! Passing secret value to /challenge/college...
Great job! Here is your flag:
pwn.college{8KtjvrcoJ1jEy__ab32GToxnKNe.dFjM5QDLwIzN0czW}
hacker@piping~duplicating-piped-data-with-tee:~$

```


## Writing to Multiple Programs

process substitution is a method used to transfer the output of one command to the input of multiple other commands.   
it basically treats the output of any command as a file, which is given a file name aka a named pipe.    
the >() operator signified proces substitution ie anything inside it is treated like a file.

I used https://sysxplore.com/process-substitution-in-bash/ to understand this concept better.

to do this challenge, I needed to split the output of `/challenge/hack` to both `/challenge/tee` and `/challenge/planet`. therefore, `tee` is required in between the two pipes, to create the splitting.

with the `tee` command, I used the `>(/challenge/the)` to take the output of the initial program and use it as the stdin here.

```
hacker@piping~writing-to-multiple-programs:~$ /challenge/hack |tee >(/challenge/the) | /challenge/planet
Congratulations, you have duplicated data into the input of two programs! Here
is your flag:
pwn.college{42wSUaKsH91Wm6g89LQCpWvU9q4.dBDO0UDLwIzN0czW}
```

## Split Piping stderr and stdout

this task was pretty hard and took a lot of trial and error:

my first try was this:
```
hacker@piping~split-piping-stderr-and-stdout:~$ /challenge/hack | tee 2>(/challenge/the) | /challenge/planet
```
but this was not working.      
I realised that I couldn't use the FD 2 along with the tee command in this manner and process substitiution can't occur.    

I tried a few more methods but they didn't work. eventually I realised why: it's because I kept using 2 pipes.   
it also didn't make sense to use two pipes, since the input for `/challenge/the` and `/challenge/planet` is not the same.

so first, I redirected the stderr using > and then used a pipe, followed by `tee` for which it finally worked:

```
hacker@piping~split-piping-stderr-and-stdout:~$ /challenge/
hack 2> >(/challenge/the) | tee >(/challenge/planet)
This secret data must directly make it to /challenge/planet over my stdout.
Don't try to copy-paste it; it changes too fast.
6681625630145341
Congratulations, you have learned a redirection technique that even experts
struggle with! Here is your flag:
pwn.college{g-OucMoJ4TTtXA1p1R4Hu1V70Rd.dFDNwYDLwIzN0czW}
```

