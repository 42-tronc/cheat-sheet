The `open` function is used to open a file and obtain a file descriptor. The file descriptor can be used to read from or write to the file.

---
## Prototype

```c
int open(const char *pathname, int flags, mode_t mode);
```

---
## Library

```c
#include <fcntl.h>
``` 

---
## Arguments

### pathname

The `pathname` argument is a string that specifies the path of the file to be opened. The `flags` argument specifies the file access mode, and can include the following values:

### flags

- `O_RDONLY` - open for reading only
- `O_WRONLY` - open for writing only
- `O_RDWR` - open for both reading and writing
- `O_CREAT` - create the file if it does not exist
- `O_APPEND` - append to the end of the file
- `O_TRUNC` - truncate the file to zero length
- `O_EXCL` - fail if the file already exists

### mode

The `mode` argument specifies the file mode and is used only if the `O_CREAT` flag is specified. It should be a bitwise OR of the following values:

- `S_IRUSR` - read permission for the owner
- `S_IWUSR` - write permission for the owner
- `S_IXUSR` - execute permission for the owner
- `S_IRGRP` - read permission for the group
- `S_IWGRP` - write permission for the group
- `S_IXGRP` - execute permission for the group
- `S_IROTH` - read permission for others
- `S_IWOTH` - write permission for others
- `S_IXOTH` - execute permission for others

---
## Returns

- **file descriptor** if successful.
- -1 if an error occurs. (*The error condition can be determined by checking the value of `errno`*).

---
## Example

Here is an example of how to use the `open` function to open a file for writing:

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
    close(fd);

    return 0;
}
```

In this example, the `open` function is called with the `filename`, the flags `O_WRONLY`, `O_CREAT`, and `O_TRUNC`, and the mode `S_IRUSR` and `S_IWUSR`. This opens the file `example.txt` for writing, creates the file if it does not exist, and truncates it to zero length if it already exists. The file mode `S_IRUSR` and `S_IWUSR` grants read and write permissions to the owner of the file. If `open` returns -1, `perror` is called with the argument "open" to print an error message, and the program terminates with a non-zero exit status.p

## Often used with:
- [[close]] - to close the fd that was opened.
- [[Write]]


## Similar functions
- 