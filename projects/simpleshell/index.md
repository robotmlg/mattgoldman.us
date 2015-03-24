---
layout: default
title: Simple Shell
---

# Simple Shell

![Simple Shell screenshot](/img/simple-shell-screenshot.png)

The code for this project can be found [here, at my bitbucket page](https://bitbucket.org/robotmlg/simple-shell).

This simple shell can run any external command with I/O piping between them.
It has cd and exit built in, and uses a table of function pointers to run them.
The input line is parsed into whitespace-separated and quote-wrapped tokens
with my lntok() function, which functions similarly to strtok().
The tokens from the string are placed into command_t structs, which assemble into
a linked list of commands.  When a pipe is detected in the input line, the prior
command is ended and a new command is added to the list.

Then, the commands are executed by iterating through the linked list and forking
a new child for each command.  Each command_t struct contains a pipe array
which is used for the input of the command (except for the first command in the 
list).  Each command is set to send its output to the pipe in the next command_t
struct in the list, and the command in that command_t struct will read from that
pipe.  The final command in the list has no next command, and so will send its 
output to stdout.  The parent process will also close both ends of the pipe,
to ensure that children will terminate.  Each child process is replaced by the
command in its command_t struct with execvp(), and the parent waits for each
to finish executing before displaying a new prompt.

Built-in commands are handled with a lookup table consising of structs matching
names to functions.  Before the commands are executed, the command name is
checked against the list of built-in functions.  If the function is a built-in,
normal exeuction is aborted, and the appropriate function is called from the 
table.
