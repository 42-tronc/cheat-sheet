# heredoc
1. need to do every heredoc and keep the last only (maybe do something like)
   ```
```

# infile
check if it exists:
	-> if found check it
		-> error : block the cmd block
		-> ok
			-> no previous: get the fd for later
			-> had previous: close the previous one and get the fd
	-> if not found: continue

check every infile at first or only the one in the cmd block?

every file:
	-> go over every file

