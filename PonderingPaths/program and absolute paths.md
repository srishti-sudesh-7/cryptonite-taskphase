# Program and Absolute Paths

absolute path: a path that starts from the root directory     

here to get the flag, I needed to reach the program called "run" which was inside the challenge directory, which in turn is inside the root directory /.    
so the path I used is `/challenge/run`

flag: 
`pwn.college{8qKcb4rm02rP1LJbhOy2pwMJIft.dVDN1QDLwIzN0czW}`

# The Root

in order to get the flag, I needed to reach a program called pwn which was in /.   
*note: directories start from / ie it is the root of the filesystem*    
to reach any program, all we need to do is put in its path. so that's what I did.     
since we know that pwn is in /, its path becomes: `/pwn`

on typing /pwn, I got the flag: 
`pwn.college{kTSRHi16X8q0H5NAjsEm1hIrghr.dhzN5QDLwIzN0czW}`

