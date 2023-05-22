# heredoc
1. need to do every heredoc
2. keep only the last of the pipe block
3. set it as the heredoc
	1. check if there is a previous one in the block
		-> free it
	2. set it

# infile
check if it exists:
	-> if found check it
		-> error : block the cmd block
		-> ok
			-> no previous: get the fd for later
			-> had previous: close the previous one and get the fd
	-> if not found: continue

# how2
- check every infile once at first
- check infiles only in the current cmd block

every file:
	-> go over every file

