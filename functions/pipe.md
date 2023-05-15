`pipe` is a function in C that creates an inter-process communication (IPC) channel between a pair of file descriptors.

---
## Function

The `pipe` function creates a pair of file descriptors that can be used for inter-process communication.

---
## Prototype

```c
int pipe(int pipefd[2]);
```

---
## Library

**unistd** which stands for "Unix Standard".

```c
#include <unistd.h>
```

---
## Arguments

### pipefd

The `pipefd` argument is a pointer to an array of two integers that will be filled in with the file descriptors for the read and write ends of the pipe. The **read** end of the pipe is `pipefd[0]` and the **write** end is `pipefd[1]`.

---
## Returns

- **0** if successful.
- **-1** if an error occurs. (*The error condition can be determined by checking the value of* `errno`).

---
## Example

Here's an example of how to use `pipe` to communicate between parent and child processes:

```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>

#define MSGSIZE 16

int main() {
    int pipefd[2];
    char buf[MSGSIZE];
    pid_t pid;

    if (pipe(pipefd) == -1) {
        perror("pipe");
        exit(EXIT_FAILURE);
    }

    pid = fork();

    if (pid == -1) {
        perror("fork");
        exit(EXIT_FAILURE);
    }

    if (pid == 0) {  // child process
        close(pipefd[1]);  // close write end of pipe
        read(pipefd[0], buf, MSGSIZE);  // read from pipe
        printf("child received message: %s\n", buf);
        close(pipefd[0]);  // close read end of pipe
    } else {  // parent process
        close(pipefd[0]);  // close read end of pipe
        write(pipefd[1], "hello, world!", MSGSIZE);  // write to pipe
        close(pipefd[1]);  // close write end of pipe
    }

    return 0;
}
```

In this example, the `pipe` function is called to create a pipe between the parent and child processes. The `fork` function is then called to create a child process. In the parent process, the write end of the pipe is closed