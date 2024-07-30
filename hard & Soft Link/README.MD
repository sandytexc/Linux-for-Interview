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
shashi@linuxtechi ~}$ man ln
ln  - make links between files
```
