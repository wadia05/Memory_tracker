
# Memory Tracker

This project implements a simple memory tracking system in C to help manage dynamic memory allocation. It provides functions to allocate and free memory, keeping track of all allocated memory blocks and releasing them in bulk to prevent memory leaks.

## Files
- `memory_tracker.h`: Header file that contains the `tracker_t` structure definition and function declarations.

## Code Overview

### Header (`memory_tracker.h`)

The `memory_tracker.h` file includes the `tracker_t` struct and function prototypes:

```c
#ifndef MEMORY_TRACKER
#define MEMORY_TRACKER

#include <stdlib.h>

typedef struct tracker_s
{
    void *address;
    struct tracker_s *next_addr;
} tracker_t;

void *tracker_malloc(size_t size);
void free_all_allocate();

#endif
```

### `tracker_malloc`
The `tracker_malloc` function is a custom memory allocator that allocates memory and keeps track of allocated blocks using a linked list.

```c
void *tracker_malloc(size_t size);
```

- **Parameters**: 
  - `size`: Size of memory to allocate.
- **Returns**: 
  - A pointer to the allocated memory block if successful, or `NULL` if allocation fails.

### `free_all_allocate`
The `free_all_allocate` function deallocates all memory blocks allocated by `tracker_malloc` in a single operation, clearing the memory tracking list.

```c
void free_all_allocate(void);
```

- **Description**: Frees all allocated memory blocks by iterating through the linked list and releasing each block, then resets the tracker list head pointer to `NULL`.

### Example Usage
Here's an example of how to use `tracker_malloc` and `free_all_allocate` in your code:

```c
#include "memory_tracker.h"

int main()
{
    char *str = tracker_malloc(sizeof(char));
    if (str != NULL) {
        str[0] = 's';
    }

    int *num = tracker_malloc(sizeof(int) * 2);
    if (num != NULL) {
        num[0] = 2;
    }

    // Free all allocated memory blocks
    free_all_allocate();


    return 0;
}
```

## Requirements
- C compiler

## Compilation
To compile this code, use the following command:
```sh
gcc -o memory_tracker main.c
```

Replace `main.c` with your actual source file name.

## License
This project is licensed under the MIT License.
