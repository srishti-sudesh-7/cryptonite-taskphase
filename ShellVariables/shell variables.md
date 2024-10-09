# SHELL VARIABLES

## Printing Variables
PWD = variable that always holds the cwd    
we add the prefix $ to the variable name to print it out using echo command.

for this challenge I used `echo $FLAG` to print the FLAG variable.
```
hacker@variables~printing-variables:~$ echo $FLAG
pwn.college{Ap4gwlpTbH5SmrCtsr6O9iBf3KN.ddTN1QDLwIzN0czW}
```

## Setting Variables
use = to assign values to any variable (note: no spaces around the =)
use prefix $ only for access variables    

this task was pretty direct, I assigned the value COLLEGE to variable PWN using = and got the flag.
```
hacker@variables~setting-variables:~$ PWN=COLLEGE
You've set the PWN variable properly! As promised, here is the flag:
pwn.college{4wNDpqeRTqUA5nj09-7w3l7GFTO.dlTN1QDLwIzN0czW}
```

## Multi-Word Variables
to set a variable's value to multiple words or numbers with spaces in between, we need to quote them.

I used this method to set the value of var PWN to COLLEGE YEAH:
```
hacker@variables~multi-word-variables:~$ PWN="COLLEGE YEAH"
You've set the PWN variable properly! As promised, here is the flag:
pwn.college{ctw2pRHgGP0Z3ckYAsIE66-POjT.dBjN1QDLwIzN0czW}
```

## Exporting Variables
exporting is a process by which we allow other commands/programs to use the variable.

as instructed, I first exported var PWN whose vallue is college:
```
hacker@variables~exporting-variables:~$ export PWN=COLLEGE
You've set the PWN variable to the proper value!
```
then I assigned the value PWN to var college, without export:
```
hacker@variables~exporting-variables:~$ COLLEGE=PWN
You've set the PWN variable to the proper value!
You've set the COLLEGE variable to the proper value!
```
then I used the `/challnge/run` program and accessed var PWN using $:
```
hacker@variables~exporting-variables:~$ /challenge/run $PWN
CORRECT!
You have exported PWN=COLLEGE and set, but not exported, COLLEGE=PWN. Great
job! Here is your flag:
pwn.college{UzZOJmhbBTdGIAWRByIpALs8j1c.dJjN1QDLwIzN0czW}
You've set the PWN variable to the proper value!
You've set the COLLEGE variable to the proper value!
```

## Printing Exported Variables

`env` is a command used to print every single exported variable in the shell.

for this challenge, I used it and got a long list of variables, among which FLAG was easy to find: 

```
hacker@variables~printing-exported-variables:~$ env
SHELL=/run/dojo/bin/bash
HOSTNAME=variables~printing-exported-variables
PWD=/home/hacker
DOJO_AUTH_TOKEN=d3e89aec321117fb9931bf9459bdae6116dcb4af69caa6d2d3e87c01af97fbfe
HOME=/home/hacker
LANG=C.UTF-8
LS_COLORS=rs=0:di=01;34:ln=01;36:mh=00:pi=40;33:so=01;35:do=01;35:bd=40;33;01:cd=40;33;01:or=40;31;01:mi=00:su=37;41:sg=30;43:ca=00:tw=30;42:ow=34;42:st=37;44:ex=01;32:*.7z=01;31:*.ace=01;31:*.alz=01;31:*.apk=01;31:*.arc=01;31:*.arj=01;31:*.bz=01;31:*.bz2=01;31:*.cab=01;31:*.cpio=01;31:*.crate=01;31:*.deb=01;31:*.drpm=01;31:*.dwm=01;31:*.dz=01;31:*.ear=01;31:*.egg=01;31:*.esd=01;31:*.gz=01;31:*.jar=01;31:*.lha=01;31:*.lrz=01;31:*.lz=01;31:*.lz4=01;31:*.lzh=01;31:*.lzma=01;31:*.lzo=01;31:*.pyz=01;31:*.rar=01;31:*.rpm=01;31:*.rz=01;31:*.sar=01;31:*.swm=01;31:*.t7z=01;31:*.tar=01;31:*.taz=01;31:*.tbz=01;31:*.tbz2=01;31:*.tgz=01;31:*.tlz=01;31:*.txz=01;31:*.tz=01;31:*.tzo=01;31:*.tzst=01;31:*.udeb=01;31:*.war=01;31:*.whl=01;31:*.wim=01;31:*.xz=01;31:*.z=01;31:*.zip=01;31:*.zoo=01;31:*.zst=01;31:*.avif=01;35:*.jpg=01;35:*.jpeg=01;35:*.mjpg=01;35:*.mjpeg=01;35:*.gif=01;35:*.bmp=01;35:*.pbm=01;35:*.pgm=01;35:*.ppm=01;35:*.tga=01;35:*.xbm=01;35:*.xpm=01;35:*.tif=01;35:*.tiff=01;35:*.png=01;35:*.svg=01;35:*.svgz=01;35:*.mng=01;35:*.pcx=01;35:*.mov=01;35:*.mpg=01;35:*.mpeg=01;35:*.m2v=01;35:*.mkv=01;35:*.webm=01;35:*.webp=01;35:*.ogm=01;35:*.mp4=01;35:*.m4v=01;35:*.mp4v=01;35:*.vob=01;35:*.qt=01;35:*.nuv=01;35:*.wmv=01;35:*.asf=01;35:*.rm=01;35:*.rmvb=01;35:*.flc=01;35:*.avi=01;35:*.fli=01;35:*.flv=01;35:*.gl=01;35:*.dl=01;35:*.xcf=01;35:*.xwd=01;35:*.yuv=01;35:*.cgm=01;35:*.emf=01;35:*.ogv=01;35:*.ogx=01;35:*.aac=00;36:*.au=00;36:*.flac=00;36:*.m4a=00;36:*.mid=00;36:*.midi=00;36:*.mka=00;36:*.mp3=00;36:*.mpc=00;36:*.ogg=00;36:*.ra=00;36:*.wav=00;36:*.oga=00;36:*.opus=00;36:*.spx=00;36:*.xspf=00;36:*~=00;90:*#=00;90:*.bak=00;90:*.crdownload=00;90:*.dpkg-dist=00;90:*.dpkg-new=00;90:*.dpkg-old=00;90:*.dpkg-tmp=00;90:*.old=00;90:*.orig=00;90:*.part=00;90:*.rej=00;90:*.rpmnew=00;90:*.rpmorig=00;90:*.rpmsave=00;90:*.swp=00;90:*.tmp=00;90:*.ucf-dist=00;90:*.ucf-new=00;90:*.ucf-old=00;90:
FLAG=pwn.college{s5KYUxxpH91Lmq-6Tcjgwo5tMzE.dhTN1QDLwIzN0czW}
LESSCLOSE=/usr/bin/lesspipe %s %s
TERM=xterm
LESSOPEN=| /usr/bin/lesspipe %s
SHLVL=1
LC_CTYPE=C.UTF-8
PATH=/run/challenge/bin:/run/workspace/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
_=/run/workspace/bin/env
```

## Storing Command Output

Command Substitution is used to store output of a command in a variable.    
it is indicated by `$()`

here I first stored the output of `/challenge/run` in var PWN using command substitution.
after this, I had to cat PWN using $ to get the flag
```
hacker@variables~storing-command-output:~$ PWN=$(/challenge/run)
Congratulations! You have read the flag into the PWN variable. Now print it out
and submit it!
hacker@variables~storing-command-output:~$ echo $PW
N
pwn.college{kGvge7Iv2dnMd-gRts8tIF5Ckbr.dVzN0UDLwIzN0czW}

```

## Reading Input
read = command used to read user's input (using it with -p argument lets you specify a prompt too)     
to do this challenge, I made the shell read the input of the user and store it in variable PWN, as shown below:
```
hacker@variables~reading-input:~$ read -p "enter value of var PWN: " PWN
enter value of var PWN: COLLEGE
You've set the PWN variable properly! As promised, here is the flag:
pwn.college{kz-4kvs4xEyX6gNo9EBGuBbR7H_.dhzN1QDLwIzN0czW}
```

## Reading Files
here I learnt how to use the `read` command to read files.    
this is done by redirecting the target file to the input variable of the `read` command

here, I redirected the file `/challenge/read_me` to `read PWN` and got the flag.

```
hacker@variables~reading-files:~$ read PWN < /challenge/read_me
You've set the PWN variable properly! As promised, here is the flag:
pwn.college{k1HtABPrSJU-LsbGNdcp0KnaV17.dBjM4QDLwIzN0czW}
```
