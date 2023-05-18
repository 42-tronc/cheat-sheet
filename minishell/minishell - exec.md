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


## infile
check if it exists:
	-> if found check it
		-> error : block the cmd block
		-> ok
			-> no previous: get the fd for later
			-> had previous: close the previous one and get the fd
	-> if not found: continue

cmd_block[pipe_count - 1]
		infile fd[nb de infile]
		outfile fd[nb de outfile]
		here doc