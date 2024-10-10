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
