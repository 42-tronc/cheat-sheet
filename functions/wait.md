`wait` is a function in C that suspends the execution of the calling process until one of its child processes terminates. It allows the parent process to synchronize its execution with the termination of child processes and retrieve their exit status.

---
## Function

The `wait` function suspends the execution of the calling process until one of its child processes terminates. It collects the termination status and resource usage information of the terminated child process.

---
## Prototype

```c
pid_t wait(int *status);
```

---
## Library

**sys/wait** which provides declarations for wait-related functions and macros.

```c
#include <sys/wait.h>
```

---
## Arguments

### status

The `status` argument is a pointer to an integer variable where the termination status of the child process will be stored. If `status` is not `NULL`, the exit status of the terminated child process is stored in the variable pointed to by `status`. This information can be used to determine how the child process terminated.

---
## Returns

- **process ID** of the terminated child process if successful.
- **-1** if an error occurs. (*The error condition can be determined by checking the value of* `errno`).

---
## Example

Here's an example of how to use `wait` to synchronize with child processes:

```c
#include <stdio.h>
#include <stdlib.h>
#include <sys/wait.h>
#include <unistd.h>

int main() {
    pid_t pid = fork();

    if (pid == -1) {
        perror("fork");
        exit(EXIT_FAILURE);
    }

    if (pid == 0) {  // child process
        printf("Child process running\n");
        sleep(2);
        printf("Child process exiting\n");
        exit(EXIT_SUCCESS);
    } else {  // parent process
        printf("Parent process waiting for child to terminate...\n");
        int status;
        pid_t terminated_pid = wait(&status);

        if (terminated_pid == -1) {
            perror("wait");
            exit(EXIT_FAILURE);
        }

        if (WIFEXITED(status)) {
            printf("Child process terminated normally with exit status: %d\n", WEXITSTATUS(status));
        } else if (WIFSIGNALED(status)) {
            printf("Child process terminated by signal: %d\n", WTERMSIG(status));
        } else {
            printf("Child process terminated abnormally\n");
        }
    }

    return 0;
}
```

In this example, the `fork` function is called to create a child process. In the child process, some work is performed (in this case, a sleep of 2 seconds) and then the child process exits with a success status using `exit`.

In the parent process, the `wait` function is called to wait for the termination of the child process. The termination status of the child process is stored in the `status` variable.

The `WIFEXITED` and `WEXITSTATUS` macros are used to check if the child process terminated normally and retrieve its exit status. If the child process terminated by a signal, the `WIFSIGNALED` and `WTERMSIG` macros can be used to obtain information about the terminating signal.

---
## Often used with

- [[fork]] - to create child processes that can be waited for.
- [[exec]] - to replace the child process with a new program after forking.

---
## Similar functions

- [[waitpid]] - provides more flexibility in waiting for specific child processes and additional options for controlling the waiting behavior.