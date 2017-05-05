# VIM - All the things I've learned but can't remember about the best file editor in the world!

---

#### Tricks

Get rid of ^M \(Usually found if copying a file from windows\):

```
:ed ++ff=dos %

OR

:%s/\r//g
```

sort a file:

```
:%!sort
```

show end of line:

```
:set list
```

---

#### Plugin Manager Setup

Setup plugin manager:

```

```

---

#### Plugins I use

Nerdtree:

```
Lets open some windows
s open new vertical split window
i open new horizontal spilt window

The next question I had was how do I switch back and forth between NERDTree and the other windows. 
All window commands start with ctrl+w

ctrl+ww cycle though all windows
crtl+wh takes you left a window
crtl+wj takes you down a window
crtl+wk takes you up a window
crtl+wl takes you right a window

Lets open some tabs
t open new tab
T open new tab while staying in current tab
gt cycle though all tabs
gT cycle though all tabs (moves to the left)

Toggle NerdTree
Fn+F2

Toggle paste from insert
Fn+F2

Toggle line numbers
con

Create a new file
ma

Hidden Files toggle
I

Set tree root
C

Directories
o: open & close
O: recurs­ively open
x: close parent
X: close all children recurs­ively
e: explore selected dir
```



