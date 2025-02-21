# Microshell - 42_Exam_Rank_04

## Description
This project is a simple shell implementation for the **Exam Rank 04** at **42 School**. It is designed to execute commands, handle pipes (`|`) and semicolons (`;`), and includes a basic implementation of the `cd` command. The program follows strict rules and limitations set by the exam.

## Features
- Executes system commands using `execve`.
- Supports command chaining using `;` (semicolon).
- Handles piping (`|`) between commands.
- Implements a custom version of the `cd` command.
- Manages process creation using `fork()` and interprocess communication using `pipe()`.

## Compilation
To compile the program, use:
```sh
cc -Wall -Wextra -Werror microshell.c -o microshell
```

## Usage
The program executes commands similarly to a UNIX shell but with limited functionality. It reads input from `argv` and processes commands accordingly.

### Example:
```sh
$ ./microshell /bin/echo hello ; /bin/ls | /bin/cat -e
hello
file1$
file2$
```

### Built-in Commands
- `cd <path>`: Changes the current working directory.
  - If `cd` is executed without exactly **one** argument, an error message is displayed.
  - If `chdir()` fails, an error message is printed.

## Error Handling
- If `cd` is called with incorrect arguments:
  ```sh
  error: cd: bad arguments
  ```
- If `cd` fails to change the directory:
  ```sh
  error: cd: cannot change directory to <directory>
  ```
- If `execve` fails to execute a command:
  ```sh
  error: cannot execute <command>
  ```
- If a fatal error occurs:
  ```sh
  error: fatal
  ```

## Code Structure
- `err()`: Prints error messages to `stderr`.
- `cd()`: Implements the `cd` command with error handling.
- `set_pipe()`: Configures pipes for interprocess communication.
- `exec()`: Handles command execution, forking, and piping.
- `main()`: Parses input arguments and executes commands sequentially.

## Notes
- The shell does **not** support input redirection (`<`) or output redirection (`>`).
- Commands must be specified with their full path (`/bin/ls`, `/usr/bin/env`, etc.).
- `execve` is used directly, without support for `$PATH` resolution.

## License
This project is free to use for educational purposes. Please do not submit this as your own work in 42 School exams.

