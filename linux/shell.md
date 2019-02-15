---
description: Shell scripting tips and tricks
---

# shell

#### Cause shell script to report error code if ANY command in script fails.  Default behavior is to report status code of last command in script.

```text
#!/bin/sh –xe
```

#### reads in a file and breaks the file up on a keyword:

```text
cat test.txt | awk '/toby/ {n++} {print > "test"n".out"}'
```

#### This is the contents of test.txt

```text
toby
this is a test
robbie
toby
to try out something


```

#### The command above breaks the file at toby and creates a file for each break:

#### Test1.out contains:

```text
toby
this is a test
Robbie
```

#### Test2.out:

```text
toby
to try out something
```

