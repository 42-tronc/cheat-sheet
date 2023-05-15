`dup2` is a function in C that duplicates an existing file descriptor to a specified new file descriptor. This is useful when you want to redirect input or output to a file or another file descriptor.

---
## Prototype

```c
int dup2(int oldfd, int newfd);
```

---
## Library

**unistd** which stands for "Unix Standard".

```c
#include <unistd.h>
```

---
## Arguments

### oldfd

The `oldfd` argument is the file descriptor that is to be duplicated.

### newfd

The `newfd` argument is the file descriptor to which `oldfd` is to be duplicated.
	Note: If `newfd` is already open, it will be closed first.


---
## Returns

- **file descriptor** if successful.
- **-1** if an error occurs. (*The error condition can be determined by checking the value of* `errno`).

---
## Example

Here's an example of how to use `dup2` to redirect output to a file:

```c
#include <stdio.h>
#include <stdlib.h>
#include <fcntl.h>
#include <unistd.h>

int main() {
    const char *filename = "output.txt";
    int fd = open(filename, O_WRONLY | O_CREAT | O_TRUNC, S_IRUSR | S_IWUSR);

	# If problem opening
    if (fd == -1) {
        perror("open");
        exit(EXIT_FAILURE);
    }

    // Redirect stdout to the file
    int newfd = dup2(fd, STDOUT_FILENO);
    if (newfd == -1) {
        perror("dup2");
        exit(EXIT_FAILURE);
    }

    printf("This text will be redirected to the file %s\n", filename);

    // Close the file and restore stdout
    close(fd);
    close(newfd);

    return 0;
}
```

In this example, the `open` function is called to obtain a file descriptor for the file `output.txt`. The `O_WRONLY`, `O_CREAT`, and `O_TRUNC` flags are used to open the file for writing, create the file if it does not exist, and truncate it to zero length if it already exists. The file mode `S_IRUSR` and `S_IWUSR` grants read and write permissions to the owner of the file.

Then, the `dup2` function is called to duplicate the file descriptor obtained from `open` to the file descriptor `STDOUT_FILENO`, which is the standard output file descriptor. This redirects the output of the `printf` function to the file instead of the console.

Finally, the file descriptors are closed using the `close` function.

## Often used with

- [[open]] - to obtain a file descriptor for the file to which we want to redirect input or output.
- [[close]] - to close the file descriptor that was duplicated.

## Similar functions

- [[dup]] - duplicates a file descriptor to the lowest available file descriptor number, instead of a specified new file descriptor.