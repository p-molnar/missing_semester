# Solution

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

	```
	echo "#!/bin/sh" > semester
	echo "curl --head --silent https://missing.csail.mit.edu" >> semester
	```

 5. Try to execute the file, i.e. type the path to the script (`./semester`)into your shell and press enter. Understand why it doesn't work by consulting the output of `ls` (hint: look at the permission bits of the file).
 
	```
	./semester
	ls -l
	```
	By default the shell tries to execute the file with a suitable program, but it does not have the permission to do so, since `semester` lacks execution bit.

5. Run the command by explicitly starting the `sh` interpreter, and giving it the file `semester` as the first argument, i.e. `sh semester`. Why does this work, while `./semester` didn't?

	```
	sh semester
	```
	In this case the shell executes the `sh` that takes `semester` as an argument. The shell in such scenario only handles the execution of the `sh` program, but does not deal with the rest, hence we are not thrown an error.

7. Look up the `chmod` program (e.g. use `man chmod`).
   
	```
	man chmod
	```

8. Use `chmod` to make it possible to run the command `./semester` rather than having to type `sh semester`. How does your shell know that the file is supposed to be interpreted using `sh`? See this page on the [shebang](https://en.wikipedia.org/wiki/Shebang_(Unix)) line for more information.

	```
	chmod u=+rwx semester
	```

	The program loader mechanism parses the rest of the file's initial line as an interpreter directive. The loader executes the specified interpreter program, passing to it as an argument using the path that was initially used when attempting to run the script, so that the program may use the file as input data.

9. Use `|` and `>` to write the "last modified" date output by `semester` into a file called `last-modified.txt` in your home directory.
	```
	ls -l semester | awk '{ printf("%s %s %s\n", $6, $7, $8) }' > last-modified.txt
	```
