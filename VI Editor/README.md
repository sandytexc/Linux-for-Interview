## here are some common Vi (and Vim) commands that might come up in an interview:
#### Entering Insert Mode:
```
i: Enter insert mode before the cursor.
I: Enter insert mode at the beginning of the current line.
a: Enter insert mode after the cursor.
A: Enter insert mode at the end of the current line.
o: Open a new line below the current line and enter insert mode.
O: Open a new line above the current line and enter insert mode.
```
#### Exiting Insert Mode:
```
Esc: Exit insert mode.
```
#### Navigation:
```
h, j, k, l: Move left, down, up, right respectively.
w: Move to the beginning of the next word.
b: Move to the beginning of the previous word.
0: Move to the beginning of the current line.
$: Move to the end of the current line.
gg: Move to the first line of the file.
G: Move to the last line of the file.
<line number>G: Move to a specific line number.
```

#### Editing:
```
x: Delete character under the cursor.
dd: Delete the current line.
dw: Delete from the cursor to the beginning of the next word.
db: Delete from the cursor to the beginning of the previous word.
yy: Yank (copy) the current line.
p: Paste the yanked or deleted text after the cursor.
P: Paste the yanked or deleted text before the cursor.
```
#### Searching:
```
/: Search forward for a pattern.
?: Search backward for a pattern.
n: Move to the next occurrence of the search pattern.
N: Move to the previous occurrence of the search pattern.
```

#### Replacing:
```
r: Replace the character under the cursor.
cw: Change (replace) the current word.
:%s/search/replace/g: Replace all occurrences of "search" with "replace" in the entire file.
```

#### Saving and Quitting:
```
:w: Save the file.
:q: Quit (close) the file.
:q!: Quit without saving (force quit).
:wq or ZZ: Save and quit.
```
