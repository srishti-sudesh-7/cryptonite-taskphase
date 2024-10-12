# Processes and Jobs

## Listing Processes

ps = command to list running processes (process snapshot / process status)    

arguments that can be used:      
* standard syntax:
  * -e = lists every process     
  * -f = full format output
  * -ef = combination of first two arguments
* BSD syntax (without use of -) (BSD = Berkeley Software Distribution)
  * a = lists processes for all users
  * x = lists processes that aren't runnning in the terminal currently
  * u = user readable output
  * aux = combination of these three

to do this challenge I used `ps -ef` and got the following list:
```
hacker@processes~listing-processes:~$ ps -ef
UID          PID    PPID  C STIME TTY          TIME CMD
root           1       0  0 15:00 ?        00:00:00 /sbin/docker-init -- /nix/var/nix/profiles/
root           7       1  0 15:00 ?        00:00:00 /run/dojo/bin/sleep 6h
root          68       1  0 15:00 ?        00:00:00 /challenge/21941-run-2403
root          72      68  0 15:00 ?        00:00:00 sleep 6h
hacker        73       0  0 15:00 pts/0    00:00:00 /run/dojo/bin/ssh-entrypoint
hacker        91      73  0 15:01 pts/0    00:00:00 ps -ef
```
in this, I ran the only file that was in `/challenge` and got the flag
```
hacker@processes~listing-processes:~$  /challenge/21941-run-2403
Yahaha, you found me! Here is your flag:
pwn.college{AszQKLHkxXk_mm13RUV3Ttnu82Y.dhzM4QDLwIzN0czW}
```

## Killing Processes

kill = command used to terminate a process.     
this command must be passed with a process identifier ie PID which can be found by using `ps`

for this, first I used `ps aux` to list the running processes and to find the PID of `/challenge/dont_run`
```
hacker@processes~killing-processes:~$ ps aux
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root           1  0.2  0.0   1056   640 ?        Ss   15:25   0:00 /sbin/docker-init -- /nix/var/nix/profiles/default/bin/dojo-ini
root           7  0.0  0.0   5052  2560 ?        S    15:25   0:00 /run/dojo/bin/sleep 6h
root          71  0.0  0.0   4732  3200 ?        S    15:25   0:00 su -c /challenge/.launcher hacker
hacker        73  0.0  0.0   4976  3200 ?        Ss   15:25   0:00 /challenge/dont_run
hacker        74  0.0  0.0   5052  2560 ?        S    15:25   0:00 sleep 6h
hacker        75  0.2  0.0   5360  3840 pts/0    Ss   15:25   0:00 /run/dojo/bin/ssh-entrypoint
hacker        92  0.0  0.0   7868  3200 pts/0    R+   15:25   0:00 ps aux
```
I found that the required PID is 73, so I used it to pass the `kill` command.
```
hacker@processes~killing-processes:~$ kill 73
hacker@processes~killing-processes:~$ /challenge/run
Great job! Here is your payment:
pwn.college{8M3kfnFYLN-CGZqrmXgDZtdRHEP.dJDN4QDLwIzN0czW}
```

## Interrupting Processes

CTRL+C will interrupt a process, ie it allows the process to cleanly exit.

here I first ran `/challenge/run` and then interrupted it, as instructed:
```
hacker@processes~interrupting-processes:~$ /challenge/run
I could give you the flag... but I won't, until this process exits. Remember,
you can force me to exit with Ctrl-C. Try it now!
^C
Good job! You have used Ctrl-C to interrupt this process! Here is your flag:
pwn.college{oPPhEDpsFmDMRs05VsK7Wf2J2lJ.dNDN4QDLwIzN0czW}
```

## Suspending Processes

CTRL+Z can suspend a process ie it pauses it and pushes it to the background

I first ran `/challenge/run` and then suspended it using ^Z:
```
hacker@processes~suspending-processes:~$ /challenge/run
I'll only give you the flag if there's already another copy of me running in
this terminal... Let's check!

UID          PID    PPID  C STIME TTY          TIME CMD
root          82      65  0 15:49 pts/0    00:00:00 bash /ch
root          84      82  0 15:49 pts/0    00:00:00 ps -f

I don't see a second me!

To pass this level, you need to suspend me and launch me again! You can
background me with Ctrl-Z or, if you're not ready to do that for whatever
reason, just hit Enter and I'll exit!


^Z
[1]+  Stopped                 /challenge/run
```
I then ran it again to get the flag:
```
hacker@processes~suspending-processes:~$ /challenge/run
I'll only give you the flag if there's already another copy of me running in
this terminal... Let's check!

UID          PID    PPID  C STIME TTY          TIME CMD
root          82      65  0 15:49 pts/0    00:00:00 bash /ch
root          89      65  0 15:50 pts/0    00:00:00 bash /ch
root          91      89  0 15:50 pts/0    00:00:00 ps -f

Yay, I found another version of me! Here is the flag:
pwn.college{cPi3StqzdZwZair-itj3spT0rs4.dVDN4QDLwIzN0czW}
```

## Resuming Processes
fg = command to resume a suspended process and bring it to the foreground of the shell

I first ran `/challenge/run` which then gave me the exact steps to follow to get the flag:
```
hacker@processes~resuming-processes:~$ /challenge/run
Let's practice resuming processes! Suspend me with Ctrl-Z, then resume me with
the 'fg' command! Or just press Enter to quit me!
^Z
[1]+  Stopped                 /challenge/run
hacker@processes~resuming-processes:~$ fg
/challenge/run
I'm back! Here's your flag:
pwn.college{0z2tSqJqlDvRPtueOVKxQCky0Hb.dZDN4QDLwIzN0czW}
```

## Backgrounding Processes
bg = command to resume processes but in the background, ie the terminal can still take more commands while the program runs in the back     

notes:     
- ps -o command invokes STAT column
- in STAT column:
  - T = suspended
  - S = sleeping 
  - R = actively running
  - plus (+) = in foreground

to do this, the logic i followed was: run `/challenge/run` > suspend it > resume it in background > run it again.
```
hacker@processes~backgrounding-processes:~$ /challenge/run
I'll only give you the flag if there's already another copy of me running *and
not suspended* in this terminal... Let's check!

UID          PID STAT CMD
root          82 S+   bash /challenge/run
root          84 R+   ps -o user=UID,pid,stat,cmd

I don't see a second me!

To pass this level, you need to suspend me, resume the suspended process in the
background, and then launch a new version of me! You can background me with
Ctrl-Z (and resume me in the background with 'bg') or, if you're not ready to
do that for whatever reason, just hit Enter and I'll exit!
^Z
[1]+  Stopped                 /challenge/run
hacker@processes~backgrounding-processes:~$ bg
[1]+ /challenge/run &

Yay, I'm now running the background! Because of that, this text will probably
overlap weirdly with the shell prompt. Don't panic; just hit Enter a few times
to scroll this text out.
hacker@processes~backgrounding-processes:~$ /challenge/run
I'll only give you the flag if there's already another copy of me running *and
not suspended* in this terminal... Let's check!

UID          PID STAT CMD
root          82 S    bash /challenge/run
root          92 S    sleep 6h
root          93 S+   bash /challenge/run
root          95 R+   ps -o user=UID,pid,stat,cmd

Yay, I found another version of me running in the background! Here is the flag:
pwn.college{04QvTiajMnbK1Tdro-Y6EhZSC7s.ddDN4QDLwIzN0czW}
```

## Foregrounding Processes
fg command can also bring a background process to the foreground    

since this challenge didnt elaborate on any instructions, I ran `/challenge/run` as done in most previous tasks. this is the message I got:
```
hacker@processes~foregrounding-processes:~$ /challenge/run
To pass this level, you need to suspend me, resume the suspended process in the
background, and *then* foreground it without re-suspending it! You can
background me with Ctrl-Z (and resume me in the background with 'bg') or, if
you're not ready to do that for whatever reason, just hit Enter and I'll exit!
^Z
```
I followed the instructions and suspended the process first:
```
[1]+  Stopped                 /challenge/run
```
then I resumed it in the backrground:
```
hacker@processes~foregrounding-processes:~$ bg
[1]+ /challenge/run &

Yay, I'm now running the background! Because of that, this text will probably
overlap weirdly with the shell prompt. Don't panic; just hit Enter a few times
to scroll this text out. After that, resume me into the foreground with 'fg';
I'll wait.
```
on running it in the foreground, I got the flag:
```
hacker@processes~foregrounding-processes:~$ fg
/challenge/run
YES! Great job! I'm now running in the foreground. Hit Enter for your flag!

pwn.college{kE3R8cb3GNxGZ7mw5gVWu__A_SO.dhDN4QDLwIzN0czW}
```

## Starting Backgrounded Processes

to start a process in the background itself, just attach a & at the end.

I did the same to run `/challenge/run` in the background:
```
hacker@processes~starting-backgrounded-processes:~$ /challenge/run &
[1] 82

Yay, you started me in the background! Because of that, this text will probably
overlap weirdly with the shell prompt, but you're used to that by now...

Anyways! Here is your flag!
pwn.college{kPcRz6_JmGjYYq-pTe9_NELqc0Q.dlDN4QDLwIzN0czW}
[1]+  Done                    /challenge/run
```

## Process Exit Codes

every process has it's own exit code when it terminates and it can be seen using `$?`     
commands that succeed return 0 whereas others return a non-zero value     

first I ran `/challenge/get-code` and then used `$?` to get its code.
```
hacker@processes~process-exit-codes:~$ /challenge/get-code
Exiting with an error code!
hacker@processes~process-exit-codes:~$ $?
ssh-entrypoint: 36: command not found
```
after this, I used 36 as an argument with `/challenge/submit-code`
```
hacker@processes~process-exit-codes:~$ /challenge/submit-code 36
CORRECT! Here is your flag:
pwn.college{Uikr3_ugQIWBe1hyTt90GNyBqBF.dljN4UDLwIzN0czW}
```

