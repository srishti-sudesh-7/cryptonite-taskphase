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

this challenge was incredibly time-consuming.    
first, as instructed I entered `man man` to find:


```
hacker@man~searching-for-manuals:~$ man man
MAN(1)                    Manual pager utils                    MAN(1)

NAME
       man - an interface to the system reference manuals

SYNOPSIS
       man [man options] [[section] page ...] ...
       man -k [apropos options] regexp ...
       man -K [man options] [section] term ...
       man -f [whatis options] page ...
       man -l [man options] file ...
       man -w|-W [man options] page ...

DESCRIPTION
       man  is the system's manual pager.  Each page argument given to
       man is normally the name of a  program,  utility  or  function.
       The manual page associated with each of these arguments is then
       found and displayed.  A section, if provided, will  direct  man
       to look only in that section of the manual.  The default action
       is to search in all of the available sections following a  pre-
       defined  order  (see DEFAULTS), and to show only the first page
       found, even if page exists in several sections.

       The table below shows the section numbers of  the  manual  fol‐
       lowed by the types of pages they contain.

       1   Executable programs or shell commands
       2   System calls (functions provided by the kernel)
       3   Library calls (functions within program libraries)
       4   Special files (usually found in /dev)
       5   File formats and conventions, e.g. /etc/passwd
       6   Games
       7   Miscellaneous  (including  macro packages and conventions),
--MORE--
```

I thought I needed to find where all the man pages are _stored_, so I searched for the same:

```
/stored
...skipping
       Manual pages are normally stored in nroff(1) format  under  a  directory
       such  as  /usr/share/man.  In some installations, there may also be pre‐
       formatted cat pages to improve performance.  See manpath(5) for  details
       of where these files are stored.
```

I was excited as I already got the path `/usr/share/man`. but I did not know how to use the man command to access this path, so I kept quickly went through the OPTIONS part of the manual and I found this:
```
   Finding manual pages
       -L locale, --locale=locale
              man  will normally determine your current locale by a call to the
              C function setlocale(3) which  interrogates  various  environment
              variables,  possibly including $LC_MESSAGES and $LANG.  To tempo‐
              rarily override the determined value, use this option to supply a
              locale string directly to man.  Note that it will not take effect
              until the search for pages actually begins.  Output such  as  the
              help message will always be displayed in the initially determined
              locale.

       -m system[,...], --systems=system[,...]
              If this system has access  to  other  operating  system's  manual
              pages,  they  can be accessed using this option.  To search for a
              manual page from NewOS's manual page collection, use  the  option
              -m NewOS.

              The  system specified can be a combination of comma delimited op‐
              erating system names.  To include a search of the native  operat‐
              ing system's manual pages, include the system name man in the ar‐
              gument string.  This option will override the $SYSTEM environment
              variable.

       -M path, --manpath=path
              Specify  an  alternate manpath to use.  By default, man uses man‐
              path derived code to determine the path to search.   This  option
              overrides  the $MANPATH environment variable and causes option -m
              to be ignored.

              A path specified as a manpath must be the root of a  manual  page
              hierarchy  structured  into  sections  as described in the man-db
              manual (under "The manual page system").  To  view  manual  pages
              outside such hierarchies, see the -l option.
```
so, I tried using the `-M path` option:
```
hacker@man~searching-for-manuals:/usr/share/man$ man -M  /usr/share/man
What manual page do you want?
For example, try 'man man'.
hacker@man~searching-for-manuals:/usr/share/man$ man /challenge/challenge
man: can't open /challenge/challenge: Permission denied
```

I was lost as to what to do here because I had hit a dead end.

Since I had no other methods of trial, I went back and read the OPTIONS carefully, once again.     
that's when I realised what I needed to do:
```
   Main modes of operation
       -f, --whatis
              Equivalent to whatis.  Display a short description  from
              the  manual  page,  if available.  See whatis(1) for de‐
              tails.

       -k, --apropos
              Equivalent to apropos.  Search the short manual page de‐
              scriptions  for  keywords  and display any matches.  See
              apropos(1) for details.

       -K, --global-apropos
              Search for text in all manual pages.  This is  a  brute-
              force  search,  and  is likely to take some time; if you
              can, you should specify a section to reduce  the  number
              of  pages that need to be searched.  Search terms may be
              simple strings (the default), or regular expressions  if
              the --regex option is used.

```
it's mentioned that using `-k` helps to search manual pages based on keywords. I thought flag would be a good keyword to use so I tried that out:
```
hacker@man~searching-for-manuals:~$ man -k
apropos what?
hacker@man~searching-for-manuals:~$ man -k flag
dpkg-buildflags (1)  - returns build flags to use during package build
Dpkg::BuildFlags (3perl) - query build flags
fegetexceptflag (3)  - floating-point rounding and exception handling
fesetexceptflag (3)  - floating-point rounding and exception handling
i386 (8)             - change reported architecture in new program en...
ioctl_iflags (2)     - ioctl() operations for inode flags
linux32 (1)          - change reported architecture in new program en...
linux64 (1)          - change reported architecture in new program en...
pcap-config (1)      - write libpcap compiler and linker flags to sta...
security_compute_av_flags (3) - query the SELinux policy database in ...
security_compute_av_flags_raw (3) - query the SELinux policy database...
set_matchpathcon_flags (3) - set flags controlling the operation of m...
set_matchpathcon_invalidcon (3) - set flags controlling the operation...
set_matchpathcon_printf (3) - set flags controlling the operation of ...
setarch (1)          - change reported architecture in new program en...
setarch (8)          - change reported architecture in new program en...
wyriutgcox (1)       - print the flag!
x86_64 (8)           - change reported architecture in new program en...

````
I finally found the man page with "print the flag!" all i had to do was use the `man` command with it as the argument:
```
hacker@man~searching-for-manuals:~$ man wyriutgcox

CHALLENGE(1)              Challenge Commands              CHALLENGE(1)

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

       --wyriut NUM
              print the flag if NUM is 479

AUTHOR
       Written by Zardus.

REPORTING BUGS
       The   repository  for  this  dojo:  <https://github.com/pwncol‐
       lege/linux-luminarium/>

SEE ALSO
       man(1) bash-builtins(7)

pwn.college                    May 2024                   CHALLENGE(1)
```

now it resembled the previosu task, except I replaced NUM with 479 this time.
```
hacker@man~searching-for-manuals:~$ /challenge/challenge --wyriut 479
Correct usage! Your flag: pwn.college{wyriEutgcoRZESZ4xhiXcrE7uW9.dZTM4QDLwIzN0czW}
```

## Helpful Programs

-h or --help or -? = arguments that give info about how to run the particular command

since so far, all the flags were invoked using the `/challenge/challenge` command, I decided I'd use it along with `--help`. this is what I got:
```
hacker@man~helpful-programs:/challenge$ /challenge/challenge -h
usage: a challenge to make you ask for help [-h] [--fortune] [-v]
                                            [-g GIVE_THE_FLAG] [-p]

optional arguments:
  -h, --help            show this help message and exit
  --fortune             read your fortune
  -v, --version         get the version number
  -g GIVE_THE_FLAG, --give-the-flag GIVE_THE_FLAG
                        get the flag, if given the correct value
  -p, --print-value     print the value that will cause the -g option to
                        give you the flag
```
from here it was clear that I had to use the `-p` argument followed by the `-g GIVE_THE_FLAG` argument:
```
hacker@man~helpful-programs:/challenge$ /challenge/challenge -p
The secret value is: 69
hacker@man~helpful-programs:/challenge$ /challenge/challenge -g 69
Correct usage! Your flag: pwn.college{0Ej6j9cyft8lax5k04IZmZ2rJhG.ddjM4QDLwIzN0czW}
```


## Help For Builtins

builtins are commands that are built into the shell itself.     

help = builtin that shows list of shell builtins       

to do this challenge, I started off by using `help challenge` as given in the description.

```
hacker@man~help-for-builtins:~$ help challenge
challenge: challenge [--fortune] [--version] [--secret SECRET]
    This builtin command will read you the flag, given the right arguments!

    Options:
      --fortune         display a fortune
      --version         display the version
      --secret VALUE    prints the flag, if VALUE is correct

    You must be sure to provide the right value to --secret. That value
    is "4nmMlKGQ".
```

the answer was pretty direct, I replaced VALUE with 4nmMlKGQ and passed the right argument:

````
hacker@man~help-for-builtins:~$  challenge --secret 4nmMlKGQ
Correct! Here is your flag!
pwn.college{4nmMlKGQPLiQktKsIFp-uuS1TIw.dRTM5QDLwIzN0czW}
````
