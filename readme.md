# Interactive Shell Program in C

## Overview

This project is an interactive shell program implemented in C. It supports a range of functionalities including background and foreground processes, signal handling, input/output redirection, and command pipelines. This shell program also includes additional features like user-defined commands and signal handling. Built as part of the course project for Operating Systems Class.

## Run and Build

To start the shell:
1. Run `make` to build the shell.
2. Execute `./main` to start the shell.

To exit the shell, use the command `exit_s`.

The `caler` function is used to call functions provided as arguments.

## Functionality

### Commands

1. **`ls [<dir>,-la]`**: Lists directories and files.
   - `<dir>`: Specifies the directory to list (optional).
   - `-la`: Lists all files including hidden ones (optional).

2. **`cd [<dir>]`**: Changes the current directory.
   - **`cd -`**: Switches to the previous working directory and prints its path.

3. **`echo str`**: Outputs the string `str` to stdout.

4. **`pinfo <pid>`**: Prints information about the process with ID `<pid>`.

5. **`command &`**: Executes the `command` in the background.

6. **`history <num>`**: Prints the last `num` commands executed in the shell.

7. **`pwd`**: Prints the current working directory.

8. **`setenv var [value]`**: Sets or updates the environment variable `var` to `value`. If `value` is omitted, `var` is set to an empty string.

9. **`unsetenv var`**: Deletes the environment variable `var` if it exists.

10. **`jobs`**: Lists all background processes with their job numbers, process IDs, and states.

11. **`kjob <job number> <signal number>`**: Sends the specified `signal number` to the background job with the given `job number`.

12. **`fg <job number>`**: Brings the background job with the given `job number` to the foreground.

13. **`bg <job number>`**: Changes the state of the stopped background job with the given `job number` to running.

14. **`overkill`**: Kills all background processes.

15. **`quit`**: Exits the shell. Pressing `CTRL+D` also exits the shell.

### Specifications

#### Specification 1: Input/Output Redirection

Supports input and output redirection using `<`, `>`, and `>>`.

- **Input Redirection**: Use `<` to take input from a file.
  - Example: `sort < lines.txt`

- **Output Redirection**: Use `>` to redirect output to a file (overwrite) and `>>` to append output to a file.
  - Example: `diff file1.txt file2.txt > output.txt`
  - Example: `sort < lines.txt > sortedlines.txt`

#### Specification 2: Command Pipelines

Supports command pipelines using the pipe symbol `|`. Can handle any number of pipes.

- **Example (two commands)**: `more file.txt | wc`
- **Example (three commands)**: `grep "new" temp.txt | cat somefile.txt | wc`

#### Specification 3: I/O Redirection within Command Pipelines

Handles I/O redirection within command pipelines.

- **Example**: `cat < in.txt | grep "pattern" > out.txt`

#### Specification 4: User-defined Commands

1. **`setenv var [value]`**: Sets or updates the environment variable `var`.

2. **`unsetenv var`**: Deletes the environment variable `var`.

3. **`jobs`**: Lists all background processes with job numbers, process IDs, and states.

4. **`kjob <job number> <signal number>`**: Sends a signal to the background job with the given job number.

5. **`fg <job number>`**: Brings the background job with the given job number to the foreground.

6. **`bg <job number>`**: Resumes the stopped background job with the given job number.

7. **`overkill`**: Kills all background processes.

8. **`quit`**: Exits the shell. Pressing `CTRL+D` also exits the shell.

#### Specification 5: Signal Handling

1. **`CTRL-Z`**: Pushes the currently running foreground job to the background and changes its state to stopped.

2. **`CTRL-C`**: Interrupts the currently running foreground job by sending the SIGINT signal.

#### Bonus Specifications

1. **Last Working Directory**: Use `cd -` to switch to the previous working directory and print its path.

2. **Exit Codes**: Displays exit codes of commands alongside the prompt:
   - `:')` for successful exit
   - `:'(` for unsuccessful exit

3. **Command Chaining with Logical AND and OR**: Supports logical `@` (AND) and `$` (OR) operators for chaining commands.
   - **Example**: `ls $ echo penguins` (Runs `echo penguins` only if `ls` fails)

### Assumptions

1. If the same command is typed consecutively in different sessions, both instances will be stored in history.

2. The symbols `<`, `>`, `>>`, `&`, `|`, `;`, `@`, `$`, `-` always correspond to their special meanings and will not appear otherwise, such as in inputs to `echo`.

3. Input and output redirection are handled for internal commands as well.

4. Background functionality is not implemented for internal commands like `cd`, `ls`, etc.

5. Redirection operators like `2>&1`, `&>`, `>&`, or `2>` are not implemented.

6. Commands may include spaces and tabs.

7. The shell should handle executing another instance of the shell program and show an appropriate error message if the command cannot be executed.

### Useful Information

1. Use of `popen`, `pclose`, and `system()` calls is not permitted.
2. Helpful routines and system calls: `getenv`, `signal`, `dup`, `dup2`, `wait`, `waitpid`, `getpid`, `kill`, `execvp`, `malloc`, `strtok`, `fork`, `setpgid`, `setenv`, and `getchar`.
3. Use `exec` family of commands to execute system commands and handle errors appropriately.
4. Use `fork()` to create child processes and `wait()` to reap them.
5. Implement signal handlers to manage background processes.


