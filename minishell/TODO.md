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
- [ ] make functions static
- [ ] ./minishell in ./minishell `cat` not found
- [ ] error codes
	- [ ] make them consistent
	- [ ] fetch them and do appropriate action with such
- [ ] check malloc
- [ ] check exit codes


# subshell exec
- command_path
- command_args
- env array

void create_subshell(t_data *data, t_token *input, int block)
`data->cmd_block[0].cmd_path`
`data->cmd_block[0].cmd_arg`
`data.env`