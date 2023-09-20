The `read` function in C is used to read data from a file descriptor (`fd`) into a buffer (`buf`). It provides a low-level mechanism for reading data from files, pipes, sockets, or other input sources.

---
## Prototype

```c
ssize_t read(int fd, void *buf, size_t count);
```

---
## Library

**unistd** which stands for "Unix Standard".

```c
#include <unistd.h>
```

---
## Arguments

### fd

The `fd` argument is an integer file descriptor representing the source from which to read data. It can be a file descriptor obtained from `open`, `socket`, or other file-related functions.

### buf

The `buf` argument is a pointer to a buffer where the read data will be stored.

### count

The `count` argument is the maximum number of bytes to read.

---
## Returns

- On success, the `read` function returns the number of bytes read.

- On error, it returns -1, and `errno` is set to indicate the error.

- If `read` reaches the end of the file (EOF), it returns 0.

---
## Example

Here's an example of how to use the `read` function to read data from a file:

```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <fcntl.h>

int main() {
    int fd;
    char buffer[100];
    ssize_t bytes_read;

    // Open a file for reading
    fd = open("example.txt", O_RDONLY);

    if (fd == -1) {
        perror("Error opening file");
        exit(EXIT_FAILURE);
    }

    // Read data from the file into the buffer
    bytes_read = read(fd, buffer, sizeof(buffer));

    if (bytes_read == -1) {
        perror("Error reading file");
        close(fd);
        exit(EXIT_FAILURE);
    }

    // Null-terminate the buffer to treat it as a string
    buffer[bytes_read] = '\0';

    printf("Read %zd bytes from the file:\n%s\n", bytes_read, buffer);

    // Close the file descriptor
    close(fd);

    return 0;
}
```

