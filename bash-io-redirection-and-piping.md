## IO Redirection and Piping

### Bash Pipelines

A *pipeline* is a sequence of one or more commands separated by the character **|** . The format for a pipeline is:

`[time [-p]] [!] command [| command2 …]`

The standard output (*stdout*) of *command* is connected via pipe to the standard input (*stdin*) of *command2*. This connection is performed before any redirections specified by the command (see **[redirection](#bash-redirection)**).

Each command in a pipeline is executed as a separate process(i.e., in a subshell).

The return status of a pipeline is the exit status of the last command, unless the **pipefail** option is enabled, in which case it’s return status is the value of the last (rightmost) command to exit with a non-zero status, or zero if all commands exit successfully.

If the reserved word **!** precedes a pipeline, it’s exit status is the logical negation of the exit status described above.

The shell waits for all commands in the pipeline to terminate before returning a value.

If the **time** reserved word precedes a pipeline, the elapsed as well as user and system time consumed by its execution are reported when the pipeline terminates. The **-p** option changes the output format to that specified by POSIX. The **TIMEFORMAT** variable may be set to a format string that specifies how the timing information should be displayed.

---

### Bash Redirection

<table>
  <tr>
    <td>`<`</td><td>redirects **stdin**</td><td>file descriptor 0</td>
  </tr>
  <tr>
    <td>`>`</td><td>redirects **stdout**</td><td>file descriptor 1</td>
  </tr>
  <tr>
    <td>`2>`</td><td>redirects **stderr**</td><td>file descriptor 2</td>
  </tr>
</table>

Redirections are processed in the order they appear, from left to right.

Note that the order of redirections is significant. For example, the command

`ls > dirlist 2>&1`

directs both stdout and stderr to the file *dirlist*, while the command

`ls 2> &1 > dirlist`

directs only the stdout to file *dirlist*, because the stderr was duplicated as stdout before stdout was redirected to *dirlist*.

#### Redirecting Input

Redirection of input causes the file whose name results from the expansion of *word* to be opened for reading on file descriptor *n*, or the stdin (file descriptor 0) if *n* is not specified.

`[n]< word`

#### Redirecting Output

Redirection of output causes the file whose name results from the expansion of *word* to be opened for writing on file descriptor *n*, or the stdout (file descriptor 1) if *n* is not specified. If the file doesn‘t exist, it is created; if it does exist, it is truncated to zero size.

`[n]> word`

Enable the **noclobber** option to the **set** builtin in order to disallow existing regular files to be overwritten by redirection of output:

`set -o noclobber` or `set -C`

Use **>|** to force overwriting an existing regular file even with the **noclobber** option to the **set** builtin enabled:

`echo "Overwritten!" >| regular_existing_file`

#### Appending Redirected Output

Redirection of output in this fashion causes the file whose name results from the expansion of *word* to be opened for appending on file descriptor *n*, or the stdout (file descriptor 1) if *n* is not specified. If the file doesn’t exist, it is created.

`[n]>>word`

#### Redirecting Standard Output and Standard Error

**Bash** allows both stdout (file descriptor 1) and stderr (file descriptor 2) to be redirected to the file whose name is the expansion of *word*:

`&>word` (**preferred**) or `>&word`

This is semantically equivalent to

`>word2>&1`
