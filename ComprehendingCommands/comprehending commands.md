# COMPREHENDING COMMANDS

## Cat: not the pet, but the command!

cat - concatenate
this command reads the file put as the argument. we can put multiple arguments too.


for this task all I had to do was put the command `cat` and argument `flag`, as given in the instructions. 


```````
hacker@commands~cat-not-the-pet-but-the-command:~$ cat flag
pwn.college{QA2D907V6m9wr53XIjqPCEmpurN.dFzN1QDLwIzN0czW}
```````

## Catting Absolute Paths

given that the absolute path is `/flag`, this task becomes easy, as cat can also read absolute paths.

therefore, I entered `cat /flag` while in the home directory and got the flag.

`````
hacker@commands~catting-absolute-paths:~$ cat /flag
pwn.college{cn6ugyLbq3tyEmXXW2Qv3ZK2CxJ.dlTM5QDLwIzN0czW}

````````````



## More Catting Practice

on opening my terminal, the absolute path to be used was mentioned. it was `/opt/capstone/windows/flag`.        
so I used the cat command with this argument and got the flag.

```````
You cannot use the 'cd' command in this level, and must retrieve the flag by
absolute path. Plus, I hid the flag in a different directory! You can find it
in the file /opt/capstone/windows/flag. Go cat it out **without** cding into
that directory!
hacker@commands~more-catting-practice:~$ cat /opt/capstone/windows/flag
pwn.college{A6unAi8Yvt73k99K2Ib2tVZeNhZ.dBjM5QDLwIzN0czW}
`````````

## Grepping for a Needle in a Haystack

grep - global regular expression print

grep is used to filter out stuff from very huge files and give us only the parts of it we need. 
to get the flag from `/challenge/data.txt` I typed `grep pwn.college /challenge/data.txt` because this will display only the lines of code within the file that contain "pwn.college"
      
``````
hacker@commands~grepping-for-a-needle-in-a-haystack:~$ grep pwn.college /challenge/data.txt
pwn.college{UlwxTNU-QIGRlIfODS6PhKsPR-p.ddTM4QDLwIzN0czW}
``````

## Listing Files

ls - lists files within the directory







