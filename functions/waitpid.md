`waitpid` is a function in C that provides more flexibility in waiting for child processes to terminate. It allows the parent process to specify which child process to wait for and provides additional options for controlling the waiting behavior.

---
## Function

The `waitpid` function suspends the execution of the calling process until a specific child process terminates or until a specific event occurs.

---
## Prototype

```c
pid_t waitpid(pid_t pid, int *status, int options);
```

---
## Library

**sys/wait** which provides declarations for wait-related functions and macros.

```c
#include <sys/wait.h>
```

---
## Arguments

### pid

The `pid` argument specifies which child process to wait for based on its process ID:

- **< -1**: The function waits for any child process whose process group ID is equal to the absolute value of `pid`.
- **-1**: The function waits for any child process.
- **0**: The function waits for any child process whose process group ID is equal to that of the calling process.
- **> 0**: The function waits for the child process with the specified process ID.

### status

The `status` argument is a pointer to an integer variable where the termination status of the child process will be stored. If `status` is not `NULL`, the exit status of the terminated child process is stored in the variable pointed to by `status`.

### options

The `options` argument allows additional control over the waiting behavior. It can be set to 0 or a combination of the following flags:

- **WCONTINUED**: The function returns for a child process that was stopped and has been continued.
- **WNOHANG**: The function returns immediately if no child process has terminated. It avoids blocking if there are no terminated child processes.
- **WUNTRACED**: The function returns for a child process that was stopped but not traced.

---
## Returns

- **process ID** of the terminated child process if successful.
- **0** if `WNOHANG` option is specified and no child process has terminated yet.
- **-1** if an error occurs. (*The error condition can be determined by checking the value of* `errno`).

---
## Example

Here's an example of how to use `waitpid` to wait for a specific child process:

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
        pid_t terminated_pid = waitpid(pid, &status, 0);

        if (terminated_pid == -1) {
            perror("waitpid");
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
In this example, the `fork` function is called to create a child process. The child process performs some work (in this case, a sleep of 2 seconds) and then exits with a success status using `exit`.

In the parent process, the `waitpid` function is called to wait for the termination of the specific child process specified by its process ID `pid`. The termination status of the child process is stored in the `status` variable.

The `WIFEXITED` and `WEXITSTATUS` macros are used to check if the child process terminated normally and retrieve its exit status. If the child process terminated by a signal, the `WIFSIGNALED` and `WTERMSIG` macros can be used to obtain information about the terminating signal.

The `waitpid` function provides additional options, such as `WNOHANG`, to control the waiting behavior. For example, if the `WNOHANG` option is specified, and the child process has not yet terminated, the `waitpid` function returns immediately with a return value of 0.

---
## Often used with

- [[fork]] - to create child processes that can be waited for.
- [[exec]] - to replace the child process with a new program after forking.

---
## Similar functions

- [[wait]] - a simpler version of [[waitpid]] that waits for any child process to terminate.
- [[wait3]] and [[wait4]] - provide more fine-grained control over the retrieval of termination status and resource usage information.