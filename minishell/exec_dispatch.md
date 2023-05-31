1. checks heredoc
2. checks infile
3. checks outfile
4. [[#checks if there is a pipe following that cmd block]]
5. checks command
6. [[#jump to the next block]]


# jump to the next block
use cmd_block_count which displays the current block
block displays the block being checked

```c
block++;
// now we need to align pip
while (block > input->pipe_block && input->next)
	input = input->next;
```

# checks