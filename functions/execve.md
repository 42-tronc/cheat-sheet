`execve` is a function in C that replaces the current process with a new process. It loads and executes a new program from a specified file path and provides a flexible mechanism for passing command-line arguments and environment variables to the new program.

---
## Function

The `execve` function replaces the current process image with a new process image specified by the given file path.

---
## Prototype

```c
int execve(const char *path, char *const argv[], char *const envp[]);
```

---
## Library

**unistd** which stands for "Unix Standard".

```c
#include <unistd.h>
```

---
## Arguments

### path

The `path` argument is a pointer to a null-terminated string that specifies the path to the executable file of the new program.

### argv

The `argv` argument is an array of pointers to null-terminated strings representing the command-line arguments passed to the new program. The first element (`argv[0]`) should typically be the name of the program itself.

### envp

The `envp` argument is an array of pointers to null-terminated strings representing the environment variables passed to the new program. It provides additional configuration and settings for the new program.

---
## Returns

- **-1** if an error occurs. (*The error condition can be determined by checking the value of* `errno`). The current process image remains unchanged in this case.

---
## Example

Here's an example of how to use `execve` to replace the current process with a new program:

```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>

int main() {
    char *const argv[] = {"/bin/ls", "-l", NULL};
    char *const envp[] = {NULL};

    if (execve("/bin/ls", argv, envp) == -1) {
        perror("execve");
        exit(EXIT_FAILURE);
    }

    // This code will only be executed if execve fails
    printf("This line will not be reached\n");

    return 0;
}
```

In this example, the `execve` function is used to execute the `/bin/ls` command with the `-l` option. The `argv` array specifies the command-line arguments, where the first element is the program itself (`"/bin/ls"`) and the second element is the option (`"-l"`). The `envp` array is set to `NULL`, indicating that no environment variables are passed to the new program.

If `execve` succeeds, the current process image is replaced by the `/bin/ls` program, and the code following the `execve` call will not be executed. If `execve` fails, it returns -1 and an error message is printed using `perror`.

---
## Often used with

- [[fork]] - to create a new process before calling `execve`.
- [[wait]] - to wait for the termination of the newly executed program.

---
## Similar functions

- [[execvp]] - similar to `execve`, but searches for the executable file in the directories listed in the `PATH` environment variable.