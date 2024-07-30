#### How to Create Hard and Soft (symlink) Links on Linux Systems



## Soft-link :

Soft link as the name suggests is a just a new link created to the new file. In this case the new file’s inode number will be pointing to the old file.

## Hard Link :
In this case the old and new file both will be pointing to same inode number.

## Symbolic Link :
In some Unix/Linux flavors both the symbolic and soft links are treated as same. But actual difference is that both the inode numbers of new and old file will be pointing to a new inode number. This will be completely depending on the implementation.


- Usage of “ln” command for creating hard links and soft links



## Creating Hard Link

1) “man ln” command will provide the following output.

```
sandeep@root ~}$ man ln
ln  - make links between files
```

2) When “ln” command is passed without any arguments, “missing file operand” error is thrown.
```
sandeep@root ~}$ln
ln: missing file operand
Try 'ln --help' for more information.
```

3) Creating the hard link between two files. First check for any existing files if any, else create the file/files freshly and then link them. Following  is  the step-by-step approach,
```
sandeep@root ~}$ ls -la
total 24
drwx------  4 root root 4096 Feb  6 15:23 .
drwxr-xr-x 23 root root 4096 Jan 25 16:39 ..
-rw-r--r--  1 root root 3122 Jan 25 16:41 .bashrc
drwx------  2 root root 4096 Feb  6 15:23 .cache
-rw-r--r--  1 root root    0 Jan 25 16:41 .hushlogin
-rw-r--r--  1 root root  148 Aug 17  2015 .profile
drwxr-xr-x  2 root root 4096 Jan 25 16:41 .ssh
```

i)  Create the file using “touch” command
```
sandeep@root ~}$ touch 123.txt
sandeep@root ~}$ ls -l
total 0
-rw-r--r-- 1 root root 0 Feb  6 15:51 123.txt
```

ii) Enter contents into the file using “cat” command, and hit “ctrl+c” to save and exit.
```
sandeep@root ~}$ cat > 123.txt
Welcome to this World!
^C
```

iii) Create the hard link between the files “123.txt” and “321.txt”. In this case the “123.txt” already existed with contents “Welcome to this World”.
```
sandeep@root ~}$ ln 123.txt 321.txt
sandeep@root ~}$ ls -l
total 8
-rw-r--r-- 2 root root 23 Feb  6 15:52 123.txt
-rw-r--r-- 2 root root 23 Feb  6 15:52 321.txt
```

iv) Check the inode(index node) numbers of the files. For both the files the inode number is same and which is 794583. Also check the contents of new file “321.txt” which is also same as “123.txt”.
```
sandeep@root ~}$ ls -li
total 8
794583 -rw-r--r-- 2 root root 23 Feb  6 15:52 123.txt
794583 -rw-r--r-- 2 root root 23 Feb  6 15:52 321.txt
$ cat 321.txt
Welcome to this World!
```

- Note 2:- Inode number is a unique index number generated for any file that is being created in Linux/unix Operating systems. These inode numbers are stored in directory/file attributes in /proc directory. But in case of links these inode numbers are shared b/w the files and only path is updated in file table.

v) Create one more file called “456.txt” and link this using ln command to “321.txt”. Now all the three files have the same inode numbers. Contents of “456.txt” will be as same as that of original file.
```
sandeep@root ~}$  ls -li
total 12
794583 -rw-r--r-- 3 root root 23 Feb  6 15:52 123.txt
794583 -rw-r--r-- 3 root root 23 Feb  6 15:52 321.txt
794583 -rw-r--r-- 3 root root 23 Feb  6 15:52 456.txt
$ cat 456.txt
Welcome to this World!
sandeep@root ~}$   ls -l
total 12
-rw-r--r-- 3 root root 23 Feb  6 15:52 123.txt
-rw-r--r-- 3 root root 23 Feb  6 15:52 321.txt
-rw-r--r-- 3 root root 23 Feb  6 15:52 456.
```

vi)  When the source file or any of these files are removed, it will not impact other files. The source file can be removed using “rm” command. Contents of other file will not have any impact either.
```
sandeep@root ~}$ rm 123.txt
sandeep@root ~}$ ls -l
total 8
-rw-r--r-- 2 root root 23 Feb  6 15:52 321.txt
-rw-r--r-- 2 root root 23 Feb  6 15:52 456.txt
sandeep@root ~}$ ls -li
total 8
794583 -rw-r--r-- 2 root root 23 Feb  6 15:52 321.txt
794583 -rw-r--r-- 2 root root 23 Feb  6 15:52 456.txt
sandeep@root ~}$ cat 456.txt
Welcome to this World!
```

vii) Hard link creation across directories is not allowed.
```
sandeep@root ~}$ls -l
total 8
-rw-r--r-- 2 root root 23 Feb  6 15:52 321.txt
-rw-r--r-- 2 root root 23 Feb  6 15:52 456.txt
sandeep@root ~}$ mkdir abc
sandeep@root ~}$ ln abc def
ln: abc: hard link not allowed for directory
```

viii) Any changes to the content of one file will impact and change the content of other file accordingly, following are the steps explained,
```
sandeep@root ~}$ vi 321.txt
Welcome to this World!
You are welcomed to this new world
:wq
sandeep@root ~}$ ls -l
total 12
-rw-r--r-- 2 root root   59 Feb  6 16:24 321.txt
-rw-r--r-- 2 root root   59 Feb  6 16:24 456.txt
drwxr-xr-x 2 root root 4096 Feb  6 16:18 abc
sandeep@root ~}$ cat 456.txt
Welcome to this World!
You are welcomed to this new world
```

###### Creating Soft Link:

1)  Create the file “src.txt” using “touch” command and enter contents as “Hello World” using cat command and then hit “ctrl+c” to save and exit.
```
sandeep@root ~}$ touch src.txt
sandeep@root ~}$ cat > src.txt
Hello World
^C
sandeep@root ~}$ ls -l
total 4
-rw-r--r-- 1 root root 12 Feb  6 16:32 src.txt
```

2)  Create the destination file as “dst.txt” and using “ln -s” command line options create the symbolic link (also called as soft link). Check the contents of “dst.txt” file and same contents as that of “src.txt” can be seen.
```
sandeep@root ~}$ ln -s src.txt dst.txt
sandeep@root ~}$  ls -l
total 4
lrwxrwxrwx 1 root root  7 Feb  6 16:33 dst.txt -> src.txt
-rw-r--r-- 1 root root 12 Feb  6 16:32 src.txt
sandeep@root ~}$  cat dst.txt
Hello World
```

3)  In case of symbolic links the inode number of source file and destination file differs. Also, in the permissions letter “l” appears indicating that these are links. “dst.txt–>src.txt” will be the new link established now.
```
sandeep@root ~}$  ls -li
total 4
794584 lrwxrwxrwx 1 root root  7 Feb  6 16:33 dst.txt -> src.txt
794583 -rw-r--r-- 1 root root 12 Feb  6 16:32 src.txt
```

4) Symbolic creation for directories is allowed. This is explained as below in the steps
```
sandeep@root ~}$ mkdir abc
sandeep@root ~}$ ln -s abc def
$ ls -l
total 8
drwxr-xr-x 2 root root 4096 Feb  6 16:34 abc
lrwxrwxrwx 1 root root    3 Feb  6 16:34 def -> abc
lrwxrwxrwx 1 root root    7 Feb  6 16:33 dst.txt -> src.txt
-rw-r--r-- 1 root root   12 Feb  6 16:32 src.txt
```
5) Inode number for all the files/directories (source and destination are different)
```
sandeep@root ~}$  ls -li
total 8
794585 drwxr-xr-x 2 root root 4096 Feb  6 16:34 abc
794586 lrwxrwxrwx 1 root root    3 Feb  6 16:34 def -> abc
794584 lrwxrwxrwx 1 root root    7 Feb  6 16:33 dst.txt -> src.txt
794583 -rw-r--r-- 1 root root   12 Feb  6 16:32 src.txt
```

6) Symbolic links can be created for directories as explained earlier. Once these directories with symbolic link are created, inside these directories files can be created. This will make it more interesting to know how this behaves now.  When the files are created in the source directory, the same is reflected in destination directory as well. The following steps explains this clearly.
```
sandeep@root ~}$ $ cd abc
sandeep@root ~}$  touch 123.txt
sandeep@root ~}$  vi 123.txt
Hello
:wq!
sandeep@root ~}$  touch 456.txt
sandeep@root ~}$  cd ..
sandeep@root ~}$  ls -l
total 8
drwxr-xr-x 2 root root 4096 Feb  6 16:36 abc
lrwxrwxrwx 1 root root    3 Feb  6 16:34 def -> abc
lrwxrwxrwx 1 root root    7 Feb  6 16:33 dst.txt -> src.txt
-rw-r--r-- 1 root root   12 Feb  6 16:32 src.txt
sandeep@root ~}$ cd def
sandeep@root ~}$ ls -l
total 4
-rw-r--r-- 1 root root 6 Feb  6 16:37 123.txt
-rw-r--r-- 1 root root 0 Feb  6 16:36 456.txt
sandeep@root ~}$ cat 123.txt
Hello
```

- Note 3:- We can have any number of nested links. But the user/admin who creates these symbolic  links should be aware of the fact that these will lead to confusion. Sometimes may be  forgotten and may create unwanted results. So they have to be careful.

- Note 4:-  There are some possibilities of “symbolic” or “soft” link pointing to a non-existing link. This is called as “Dangling link”. This will be pointing to no-where.

