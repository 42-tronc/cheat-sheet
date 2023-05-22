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

Need to know:
1. in which block it is (could get it from the pipe_bloc in data?)
2. fd is -2 if none was found before

### if found (`block.in_fd != -2`)
1. need to close the one before
2. check the current
3. set it as the new infile in `block.in_fd`

need to be a loop for every file

# how2
- check every infile once at first
- check infiles only in the current cmd block
	- do something like `while pipe_block = block`

checks could return something, 1 if found, 0 if not found, -1 if error?
could do 
```c
while(input)
{
	// check_heredoc
	%%while(check_infile(tokens, block=i)) // not possible unless it returns the element checked%%
	
		
	// check outfile
	// check command
	input = input.next
}



```

every file:
	-> go over every file

