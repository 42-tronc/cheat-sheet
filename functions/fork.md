`fork` is a function in C that creates a new process by duplicating the calling process. The new process, known as the child process, is an exact copy of the calling process, known as the parent process.

---
## Prototype

```c
pid_t fork(void);
```

---
## Library

**unistd** which stands for "Unix Standard".

```c
#include <unistd.h>
```

---
## Arguments

None.

---
## Returns

- **0** to the child process if the fork is successful.
- **pid of the child process** to the parent process if the fork is successful.
- **-1** if an error occurs. (*The error condition can be determined by checking the value of* `errno`).

---
## Example

Here's an example of how to use `fork` to create a new process:

```c
#include <stdio.h>
#include <unistd.h>

int main() {
    pid_t pid = fork();

    if (pid == -1) {
        perror("fork");
        return -1;
    }

    if (pid == 0) {
        // This code is executed by the child process
        printf("Child process, pid=%d\n", getpid());
    } else {
        // This code is executed by the parent process
        printf("Parent process, pid=%d, child pid=%d\n", getpid(), pid);
    }

    return 0;
}
```

In this example, the `fork` function is called to create a new process. If `fork` returns a value of 0, this indicates that the code is executing in the child process. If `fork` returns a value greater than 0, this indicates that the code is executing in the parent process, and the value returned by `fork` is the process ID of the child process.

The code in the if/else statements is executed by the child and parent processes respectively.

---
## Often used with

- [[wait]] - to wait for the child process to terminate.
- [[minishell - exec]] - to replace the child process with a new program.

---
## Similar functions

- [[vfork]] - creates a new process without duplicating the parent process's memory space. This is more efficient than `fork`, but requires more care to avoid undefined behavior.