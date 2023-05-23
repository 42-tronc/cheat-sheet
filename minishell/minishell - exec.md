When creating pipe, check if it failed
```c
if (id == -1)
	do something;
```

1. Define fd
2. Create pipe and check if `= -1`
3. Define id (or pid)
4. Create fork and check if `= -1`
5. Do something with the child (pid = 0)

# execve
1. check for each command if `built-in` or not
2. if not a `built-in`, send it to execve
	1. checks the path with just the `command`
		1. if not found `free and quit?`
	2. fills an array with `command` and `args`
	3. (maybe have the envp ?)
	4. get the output to somewhere if there's one (so we can have it for the next pipe)


`ls < infile -l > outfile -a`
1. heredoc (launch it first)
2. infile
3. outfile
4. cmd


# how
1. enter the **cmd block**
2. check [[files]] (heredoc, infile, outfile)
3. check if there is another cmd block following
4. check cmd
5. execve
6. go to the next block