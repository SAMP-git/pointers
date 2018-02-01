# pointers
Slice's formatex because it doesn't have a GitHub repo.

Original thread: [pointers.inc - Pointers for PAWN!](http://forum.sa-mp.com/showthread.php?t=311757)

All credits to [Slice/oscar-broman](https://github.com/oscar-broman/)

The original library wasn't shipped with an explicit license but I'm sure, in the spirit of Open Source, Slice is happy to have this redistributed via GitHub - if not, let me know!  


[![sampctl](https://shields.southcla.ws/badge/sampctl-pointers-2f2f2f.svg?style=for-the-badge)](https://github.com/SAMP-git/pointers)

Here's a neat implementation of pointers for PAWN! This include makes it a lot easier to deal with variadic functions (functions that can take a varying number of arguments), but also allows you to, for example, have pointers from large enum structures into other arrays, parts of strings, etc.

## Installation

Simply install to your project:

```bash
sampctl package install SAMP-git/pointers
```

Include in your code and begin using the library:

```pawn
#include <pointers>
```

## Usage
A quick example:
```pawn
new
    g_Test[] = {123, 456, 789}
;

public OnGameModeInit() {
    new address = GetVariableAddress(g_Test);
    
    // Change the 2nd value
    @ptr[address][1] = 444;
    
    // Print out the values
    printf("%d, %d, %d", @ptr[address][0], @ptr[address][1], @ptr[address][2]);
}
```

Here's an example of a function that appends all string arguments to a given string.

```pawn

public OnGameModeInit() {
    new buf[128] = "Lorem";
    
    concat(buf, sizeof(buf), "ipsum", "dolor", "sit", "amet,", "consectetur", "adipiscing.");
    
    // Prints out: Lorem ipsum dolor sit amet, consectetur adipiscing.
    print(buf);
}

// Append all strings to szOutput
stock concat(output[], maxsize = sizeof(output), ...) {
    new
        arg_count = numargs()
    ;
    
    for (new i = 2; i < arg_count; i++) {
        // First add a space
        strcat(output, " ", maxsize);
        
        // Then add the string
        strcat(output, @arg[i], maxsize);
    }
}
```

Syntax:

```pawn
@ptr[address] // This is now a pointer to "address"
@arg[2] // This is now a pointer to the 3rd argument (0 is the first)
```