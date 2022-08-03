# Solutions

1. Create a new directory called `missing` under `/tmp`.
	```
	mkdir missing
	```

2. Look up the `touch` program. The `man` program is your friend.

	```
	man touch
	```

3. Use `touch` to create a new file called `semester` in `missing`.

	```
	touch semester
	```

4. Write the following into that file, one line at a time:
    ```
    #!/bin/sh
    curl --head --silent https://missing.csail.mit.edu
    ```
    The first line might be tricky to get working. It's helpful to know that
    `#` starts a comment in Bash, and `!` has a special meaning even within
    double-quoted (`"`) strings. Bash treats single-quoted strings (`'`)
    differently: they will do the trick in this case. See the Bash
    [quoting](https://www.gnu.org/software/bash/manual/html_node/Quoting.html)
    manual page for more information.