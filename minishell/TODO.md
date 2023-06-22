- [x] get return of checks (infile, outfile, cmd)
- [x] fix built ins with outputs
	- [x] env
	- [x] export
		- [x] if null and value alr dont remove it
	- [x] echo
- [x] pass block id in exec_cmd
- [ ] create a free all
- [x] handle signals
- [x] echo output
- [ ] SHLVL
- [ ] default env vars
- [ ] make functions static
- [x] ./minishell in ./minishell `cat` not found
- [x] error codes
	- [x] make them consistent
	- [x] fetch them and do appropriate action with such
- [ ] check malloc
- [ ] check exit codes
- [x] fix export with null values
- [x] heredoc
- [ ] reorder files


# subshell exec
- command_path
- command_args
- env array

void create_subshell(t_data *data, t_token *input, int block)
`data->cmd_block[0].cmd_path`
`data->cmd_block[0].cmd_arg`
`data.env`

if `pipe[0/1] > 0` it means that it is created so you can send something to it
else dont send it to the pipe and to the stdout or get stdin