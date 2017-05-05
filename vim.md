# VIM - All the things I've learned but can't remember about the best file editor in the world!

---

#### VIM tricks

Get rid of ^M \(Usually found if copying a file from windows\):

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



