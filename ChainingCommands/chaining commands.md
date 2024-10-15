# CHAINING COMMANDS 

## Chaining With Semicolons    

a semicolon ; allows us to type multiple commands at once without entering them individually every time     

for this challenge I ran /challenge/pwn and /challenge/college but seperated them with a semicolon:
```
hacker@chaining~chaining-with-semicolons:~$ /challenge/pwn; /challenge/college
Yes! You chained /challenge/pwn and /challenge/college! Here is your flag:
pwn.college{oX4z5DEsBSbDpNvKRr1J3DAnkuU.dVTN4QDLwIzN0czW}
```

## Your First Shell Script   

if we want to run many commands in a consecutive manner, we can store them in a file called *shell script.*     
shell scripts have suffix .sh     
to invoke the script, we use bash as command.    

to do this task, I referred to https://www.geeksforgeeks.org/how-to-create-a-shell-script-in-linux/ as I didnt know how to create the shell script.      
from this site I learnt that I needed to:    
1. create the script using touch command
2. make it executable by changing mode using chmod command
3. use a text editor (I used nano) to type the commands in the script

first I created the file:
```
hacker@chaining~your-first-shell-script:~$ touch x.sh
hacker@chaining~your-first-shell-script:~$ ls
2        PWN  instructions  myflag        pwn     s    the-flag
COLLEGE  h    my            not-the-flag  pwn_op  tee  x.sh
```

then I changed permissions to make sure it was executable:
```
hacker@chaining~your-first-shell-script:~$ ls -l x.sh
-rw-r--r-- 1 hacker hacker 0 Oct 15 13:30 x.sh
hacker@chaining~your-first-shell-script:~$ chmod ugo+x x.sh
hacker@chaining~your-first-shell-script:~$ ls -l x.sh
-rwxr-xr-x 1 hacker hacker 0 Oct 15 13:30 x.sh
```
then I opened the editor using `nano x.sh` and saved the commands `/challenge/pwn; /challenge/college` in it.   
after this I ran the shell script using bash:
```
hacker@chaining~your-first-shell-script:~$ bash x.sh
Great job, you've written your first shell script! Here is the flag:
pwn.college{IVwwgfGTXWH2W00OmPVmu-2O4Uh.dFzN4QDLwIzN0czW}
```

## Redirecting Script Output     

if we want to redirect multiple outputs to one command's input, we could store them in a script and then pipe the same shell script to the command's input.    

since I had already created the script containing the commands required for this challenge, all I needed to do was pipe it into the input of `/challenge/solve`:
```
hacker@chaining~redirecting-script-output:~$ bash x.sh | /challenge/solve
Correct! Here is your flag:
pwn.college{YNLKWDfBi-nXRvShZ5-9ejITCAz.dhTM5QDLwIzN0czW}
```

## Executable Shell Scripts    

when we use the bash command we're basically telling the shell to read the commands from the argument script.     
here I learnt that if the file is already executable then we can just run it without "bash" ie we just use it's absolute/relative path.    

here I created a script called myscript.sh where I stored the program /challenge/solve. I then used chmod to make it executable and then was able to run it using its relative path.
```
hacker@chaining~executable-shell-scripts:~$ touch myscript.sh
hacker@chaining~executable-shell-scripts:~$ nano myscript.sh
hacker@chaining~executable-shell-scripts:~$ chmod ugo+x myscript.sh
hacker@chaining~executable-shell-scripts:~$ /myscript.sh
ssh-entrypoint: /myscript.sh: No such file or directory
hacker@chaining~executable-shell-scripts:~$ ./myscript.sh
Congratulations on your shell script execution! Your flag:
pwn.college{0f8WlRfFFZW8k9dbQPlJqOlZxRc.dRzNyUDLwIzN0czW}
```
