The `close` function is used to close a file descriptor and free the associated resources.

---

## Prototype

```c
int close(int fd);
```

---
## Library

```c
#include <unistd.h>
```

----
## Arguments

The `fd` argument is the file descriptor to be closed.

---
## Returns

The `close` function returns zero if successful, or -1 if an error occurs.

---
## Example

Here is an example of how to use the `close` function to close a file descriptor:

```c
#include <stdio.h>
#include <stdlib.h>
#include <fcntl.h>
#include <unistd.h>

int main() {
    const char *filename = "example.txt";
    int fd = open(filename, O_WRONLY | O_CREAT | O_TRUNC, S_IRUSR | S_IWUSR);

    if (fd == -1) {
        perror("open");
        exit(EXIT_FAILURE);
    }

    // write to the file
    const char *message = "Hello, world!\n";
    write(fd, message, strlen(message));

    // close the file
    if (close(fd) == -1) {
        perror("close");
        exit(EXIT_FAILURE);
    }

    return 0;
}
```

In this example, the `open` function is called to obtain a file descriptor for the file `example.txt`, and the `write` function is used to write a message to the file. The `close` function is then called to close the file descriptor. If `close` returns -1, `perror` is called with the argument "close" to print an error message, and the program terminates with a non-zero exit status.

---
## Often used with

- [[open]] - to obtain a file descriptor for the file to be closed
- [[dup]] - to duplicate a file descriptor before closing it, so that it can be used later

---
## Similar functions

- [[fclose]] - a similar function used to close a stream (rather than a file descriptor) in the C standard library