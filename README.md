# Get Next Line (GNL)

This project is part of the 42 curriculum. The goal is to create a function that returns a line ending with a newline, read from a file descriptor.

## Function Prototype

```c
char *get_next_line(int fd);
```

## Description

The `get_next_line` function reads from a file descriptor and returns the next line, including the newline character (`\n`). It uses a static variable to save the remaining buffer between calls, allowing it to read the file line by line until EOF.

If an error occurs or the end of file is reached, it returns `NULL`.

## Files

- `get_next_line.h`   – Header file with function prototype and helper function declarations.
- `get_next_line.c`   – Main implementation.
- `get_next_line_utils.c` – Utility functions (e.g., `ft_strlen`, `ft_strjoin`, `ft_strchr`, `ft_calloc`, `ft_bzero`).
- `get_next_line_bonus.h` – Bonus version header (supports multiple file descriptors).
- `get_next_line_bonus.c` – Bonus implementation.
- `get_next_line_utils_bonus.c` – Bonus utilities.

## Compilation

### Mandatory part

```bash
gcc -Wall -Wextra -Werror -D BUFFER_SIZE=42 get_next_line.c get_next_line_utils.c -o test_gnl
```

### Bonus part

```bash
gcc -Wall -Wextra -Werror -D BUFFER_SIZE=42 get_next_line_bonus.c get_next_line_utils_bonus.c -o test_gnl_bonus
```

You can adjust `BUFFER_SIZE` as needed (default is 50 if not defined).

## Usage Example

```c
#include "get_next_line.h"
#include <fcntl.h>
#include <stdio.h>

int main(void)
{
    int fd = open("test.txt", O_RDONLY);
    char *line;

    while ((line = get_next_line(fd)) != NULL)
    {
        printf("%s", line);
        free(line);
    }
    close(fd);
    return (0);
}
```

## Notes

- The function handles file descriptors correctly, including reading from multiple file descriptors in the bonus version.
- Memory leaks must be avoided; always free the returned line after use.
- The static variable ensures that the function remembers where it left off for the next call.

## Author

cgorin (cgorin@student.42.fr)