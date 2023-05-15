`readline` is a function in C that reads a line of input from a file stream or from the user via the console. It provides a convenient way to read input one line at a time, handling memory allocation and input buffering automatically.

---
## Prototype

```c
char *readline(const char *prompt);
```

---
## Library

**readline** which stands for "GNU readline".

```c
#include <readline/readline.h>
```

---
## Arguments

### prompt

The `prompt` argument is a string that is displayed to the user before reading input from the console. It can be set to NULL if no prompt is desired.

---
## Returns

- **a pointer to a string** containing the input line if successful.
- **NULL** if an error occurs or if the end of input is reached.

---
## Example

Here's an example of how to use `readline` to read input from the user via the console:

```c
#include <stdio.h>
#include <readline/readline.h>

int main() {
    char *input = readline("Enter a string: ");

    if (input == NULL) {
        printf("No input provided\n");
    } else {
        printf("You entered: %s\n", input);
        free(input);
    }

    return 0;
}
```

In this example, the `readline` function is called to read a line of input from the console. The user is prompted to enter a string with the message "Enter a string: ".

If the user enters a string, it is printed to the console. The memory allocated by `readline` for the input string is freed using the `free` function.

If the user enters no input and presses enter, `readline` returns `NULL` and the message "No input provided" is printed to the console.

---
## Often used with

- [[add_history]] - to add the input line to the history buffer.
- [[rl_bind_key]] - to bind a custom function to a key sequence.
- [[rl_completion]] - to provide tab-completion for input.

---
## Similar functions

- [[fgets]] - reads a line of input from a file stream.
- [[gets]] - reads a line of input from the console. This function is unsafe and should be avoided.