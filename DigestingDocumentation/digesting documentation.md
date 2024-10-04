# Digesting Documentation

## Learning From Documentation

this one was pretty easy, all i had to do was pass the argument properly in the following manner:
  
``````
hacker@man~learning-from-documentation:~$ /challenge/challenge --giveflag
Correct argument! Here is your flag:
pwn.college{4J8Vs_QaIyW-YYJ-HKhCes2Uiqo.dRjM5QDLwIzN0czW}
````````
## Learning Complex Usage

here, it's been mentioned that using `/challenge/challenge --printfile` along with the correct argument will give the flag.    
to determine the correct argument, I ha to find the path to the flag.
for this, I first used the `find` command:
````
hacker@man~learning-complex-usage:~$ find / -name flag
find: ‘/root’: Permission denied
find: ‘/proc/1/task/1/fd’: Permission denied
find: ‘/proc/1/task/1/fdinfo’: Permission denied
find: ‘/proc/1/task/1/ns’: Permission denied
find: ‘/proc/1/fd’: Permission denied
find: ‘/proc/1/map_files’: Permission denied
find: ‘/proc/1/fdinfo’: Permission denied
find: ‘/proc/1/ns’: Permission denied
find: ‘/proc/7/task/7/fd’: Permission denied
find: ‘/proc/7/task/7/fdinfo’: Permission denied
find: ‘/proc/7/task/7/ns’: Permission denied
find: ‘/proc/7/fd’: Permission denied
find: ‘/proc/7/map_files’: Permission denied
find: ‘/proc/7/fdinfo’: Permission denied
find: ‘/proc/7/ns’: Permission denied
find: ‘/var/log/private’: Permission denied
find: ‘/var/log/apache2’: Permission denied
find: ‘/var/log/mysql’: Permission denied
find: ‘/var/cache/ldconfig’: Permission denied
find: ‘/var/cache/apt/archives/partial’: Permission denied
find: ‘/var/cache/private’: Permission denied
find: ‘/var/lib/apt/lists/partial’: Permission denied
find: ‘/var/lib/php/sessions’: Permission denied
find: ‘/var/lib/mysql-files’: Permission denied
find: ‘/var/lib/private’: Permission denied
find: ‘/var/lib/mysql-keyring’: Permission denied
find: ‘/var/lib/mysql’: Permission denied
find: ‘/tmp/tmp.XvrUsDZh8M’: Permission denied
find: ‘/run/mysqld’: Permission denied
find: ‘/run/sudo’: Permission denied
find: ‘/etc/ssl/private’: Permission denied
/usr/local/lib/python3.8/dist-packages/pwnlib/flag
/usr/local/share/radare2/5.9.5/flag
/opt/pwndbg/.venv/lib/python3.8/site-packages/pwnlib/flag
/opt/radare2/libr/flag
/flag
/nix/store/pmvk2bk4p550w182rjfm529kfqddnvh3-python3.11-pwntools-4.12.0/lib/python3.11/site-packages/pwnlib/flag
/nix/store/1yagn5s8sf7kcs2hkccgf8d0wxlrv5sz-radare2-5.9.0/share/radare2/5.9.0/flag
````

the `/flag` path stood out to me immediately as it seemed the most direct, so I used it as my argument and got the flag.

```
hacker@man~learning-complex-usage:~$ /challenge/challenge --printfile /f
lag
Correct argument! Here is the /flag file:
pwn.college{0yjPXaw1GEPzpS6dk4fUal8s6Gc.dVjM5QDLwIzN0czW}
````

## Reading Manuals

man = command that displays the manual for the argument (which will be another command)

for this challenge, first I typed in `man challenge` as given in the instructions. 
the manual read as follows:

````
CHALLENGE(1)               Challenge Commands              CHALLENGE(1)

NAME
       /challenge/challenge - print the flag!

SYNOPSIS
       challenge OPTION

DESCRIPTION
       Output the flag when called with the right arguments.

       --fortune
              read a fortune

       --version
              output version information and exit

       --cvgwoa NUM
              print the flag if NUM is 351

AUTHOR
       Written by Zardus.

REPORTING BUGS
       The   repository   for  this  dojo:  <https://github.com/pwncol‐
       lege/linux-luminarium/>

SEE ALSO
       man(1) bash-builtins(7)

pwn.college                     May 2024                   CHALLENGE(1)
````
out of the options, it was obvious that the third one had to be used, since it says it can be used to print the flag.
therefore, in place of NUM, i typed in 351 and got the flag.

```
hacker@man~reading-manuals:~$ /challenge/challenge --cvgwoa 351
Correct usage! Your flag: pwn.college{cv_3gC5w14o55a_1fPu2UBmeF2s.dRTM4QDLwIzN0czW}
```

## Searching Manuals

in man page:    
arrows/PgUp+PgDown - scroll  
/ - search    
n - next result   
N - previous result    
? - search backwards     

for this challenge, first I opened the manual of the challenge command.
```

CHALLENGE(1)               Challenge Commands               CHALLENGE(1)

NAME
       /challenge/challenge - print the flag!

SYNOPSIS
       challenge OPTION


DESCRIPTION
       Output the flag when called with the right argument.

       --fortune
              read a fortune

       --version
              output version information and exit

       --zmeq A neat argument, but not the right one.

       --sxbt A neat argument, but not the right one.

       --neci A neat argument, but not the right one.

       --gredg
              A neat argument, but not the right one.

       --jyydr
              A neat argument, but not the right one.

       -d     A neat argument, but not the right one.

       --pmhfvi
              A neat argument, but not the right one.

       --qxpy A neat argument, but not the right one.

```
and so on.....

out of this large list of options, to find the correct argument, i typed `/flag`. first it showed the "flag" present in the NAME and first line of the DESCRIPTION. to move to the next search i typed `n` and that's when I got:
`-f     This argument will give you the flag!`

after this, I directly got the flag by using this argument with the `/challenge/challenge` command
```
hacker@man~searching-manuals:~$ /challenge/challenge -f
Initializing...
Correct usage! Your flag: pwn.college{UIqucUyM7sNx7Av5evukZl3PnEv.dVTM4QDLwIzN0czW}
```

## Searching For Manuals






/stored
...skipping
       Manual pages are normally stored in nroff(1) format  under  a  directory
       such  as  /usr/share/man.  In some installations, there may also be pre‐
       formatted cat pages to improve performance.  See manpath(5) for  details
       of where these files are stored.


       

