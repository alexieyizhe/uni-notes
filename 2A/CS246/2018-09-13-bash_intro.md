**CS 246 |** Sept 13, 2018


# Intro to the Shell
The shell is the interface to the OS and your method of allowing the OS to perform tasks like running programs, managing files, etc. You can interact with a shell through:
 - A graphical interface (click, touch)
    - having a UI is easier to reason with
 - Command line interface (typing commands at a prompt)
    - More versatile, powerful, but a bit more clunky

This course uses bash (Bourne Again SHell).

### The Basics
- A **directory is just a special type of file**, so when we refer to ‘files’ in this course, we include directories in that definition as well.
- Every line of a valid text file must end with a newline char (`\n`), INCLUDING THE LAST LINE (Marmoset will check for this so include it so you don’t fail all your tests lol).

### Shell Commands
- `cat file.txt` passes the name of the file as an argument, and cat opens the file and displays it, but `cat < file.txt` has the file being opened by the shell, which passes the contents to cat as input
- <kbd>CTRL</kbd>+<kbd>D</kbd> sends an EOF signal to the program to indicate that there is no more input, <kbd>CTRL</kbd>+<kbd>C</kbd> kills the program immediately.
- A globbing pattern (*e.g.* `*`) is a shell capability that matches text based on patterns like the wildcard operator. These aren’t regex, just a functionality implemented by the shell.
- Using piping hands output to another __program__ or __utility__; output redirection passes output to another __file__ or __stream__.
- Use `$(CMD_NAME)` to embed commands inside others
 - `"double quotes"` group stuff together, `'single quotes'` completely supress any commands inside

### Process Streams
Every running process is attached to 3 streams which are (by default): `stdin`, `stdout`, `stderr`.

`stderr` is a separate output stream for error messages:
- Allows for intended output to be separated from unintended error messages
- Displays messages in stream instantly, is not buffered compared to other streams
- Use 2> to redirect error output just like regular output redirection
