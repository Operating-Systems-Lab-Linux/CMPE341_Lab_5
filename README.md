# Linux Lab 5 --- Shells and Bash Scripting

## Course Information

**Course:** Operating Systems Lab (CMPE341-S01-2025)\
**Instructor:** Prof. Dr. Nima Jafari Navimipour\
**Teaching Assistants:** Maryam Zaker, Hossam Rafaie, Parviz Pourmahmoud

------------------------------------------------------------------------

## Learning Outcomes

By the end of this lab, students will be able to: - Explain what a shell
is and distinguish between terminal, shell, and operating system. -
Describe Bash and identify other common Unix shells. - Explain types of
variables in the shell. - Write minimal Bash scripts with appropriate
shebang lines. - Make scripts executable and run them. - Redirect output
and manage standard streams.

------------------------------------------------------------------------

## 1. Understanding the Shell

A **shell** is a program that serves as an interface between the user
and the kernel.\
It allows users to send commands to the kernel and receive responses.
This interaction makes the shell a powerful tool for controlling the
operating system and running programs.

### Major Unix Shells

  ------------------------------------------------------------------------
  Shell       Description         Key Features         Limitations
  ----------- ------------------- -------------------- -------------------
  **Bourne    Original UNIX shell Compact and fast;    No command history;
  Shell       by Steve Bourne     foundation for       limited features
  (sh)**                          modern shells        

  **C Shell   Created by Bill Joy C-like syntax;       Syntax differs from
  (csh)**                         command history,     sh; less portable
                                  aliases              

  **Korn      By David Korn, AT&T Superset of sh; adds Not always
  Shell       Bell Labs           arithmetic, arrays,  installed by
  (ksh)**                         functions            default

  **Z Shell   Modern, powerful    Completion, plugins, Configuration can
  (zsh)**     shell               themes               be complex
  ------------------------------------------------------------------------

------------------------------------------------------------------------

## 2. Bash (Bourne Again Shell)

**Bash** is the GNU replacement for the original Bourne Shell. It is the
default shell in most Linux systems and supports both interactive and
scripting use.

**Why Bash?** - Compatible with Bourne syntax. - Provides features such
as command history, line editing, tab completion, functions, and
arrays. - Commonly used in online tutorials and Linux distributions.

------------------------------------------------------------------------

## 3. Basic Bash Scripting

A **Bash script** is a file containing a series of shell commands
executed line-by-line.

Example minimal script:

``` bash
#!/usr/bin/env bash
echo "Hello, world!"
```

### The Shebang Line

-   Indicates the interpreter to use: `#!/bin/bash`
-   Portable alternative: `#!/usr/bin/env bash` (searches Bash in PATH)

To run a script:

``` bash
chmod +x script.sh
./script.sh
```

------------------------------------------------------------------------

## 4. Shell Variables

Shell variables can be categorized by their **export status** and
**scope**.

  --------------------------------------------------------------------------------------
  Type             Description                      Example
  ---------------- -------------------------------- ------------------------------------
  Shell Variable   Available only in current shell  `name="student"`

  Environment      Exported to child processes      `export PATH=$PATH:/usr/local/bin`
  Variable                                          

  Global Variable  Visible throughout the script    Defined outside functions

  Local Variable   Visible only within functions    Declared using `local` keyword
  --------------------------------------------------------------------------------------

To manage variables: \| Action \| Command \| Notes \|
\|--------\|----------\|-------\| \| Create \| `VAR=value` \| Temporary
variable \| \| Export \| `export VAR=value` \| Makes variable available
to subshells \| \| Show environment \| `printenv` \| Lists exported
variables \| \| Unset \| `unset VAR` \| Deletes variable \| \| Persist
\| Add to `~/.bashrc` \| Loads with every new session \|

------------------------------------------------------------------------

## 5. Quoting and Command Substitution

### Quoting

-   **Double quotes (" ")**: Expand variables and commands.\
-   **Single quotes (' ')**: Treat contents literally.

Example:

``` bash
echo "User: $USER"
echo 'User: $USER'
```

### Command Substitution

Use command output within another command:

``` bash
today=$(date +%Y-%m-%d)
echo "Today is $today"
```

------------------------------------------------------------------------

## 6. Conditional Statements

### If Statements

``` bash
mynum=200
if [ $mynum -eq 200 ]; then
    echo "The condition is true."
fi
```

### If--Else and Case Statements

Used for branching logic and pattern-based decisions.

------------------------------------------------------------------------

## 7. Practical Challenges

### Challenge 1 --- Exploring Shells

1.  Display your current shell.\
2.  List all available login shells from `/etc/shells`.\
3.  Determine which shell each system user uses.

### Challenge 2 --- Script Verification

Write a script (`myscript.sh`) that: 1. Stores the full path of `htop`
in a variable.\
2. Checks if it exists using `-f`.\
3. Installs it if missing.

### Challenge 3 --- Package Installer

Write a script (`pkginstaller.sh`) that: 1. Accepts package names as
command-line arguments.\
2. Installs each package in a loop.\
3. Displays messages based on success or failure.

Brief example snippet:

``` bash
for pkg in "$@"; do
    sudo apt install -y "$pkg"
    if [ $? -eq 0 ]; then
        echo "$pkg installed successfully."
    else
        echo "Installation failed for $pkg."
    fi
done
```

------------------------------------------------------------------------

## 8. Input/Output Redirection and Pipes

  Concept                     Description             Example
  --------------------------- ----------------------- --------------------------
  **stdin (0)**               Input stream            `< input.txt`
  **stdout (1)**              Standard output         `> output.txt`
  **stderr (2)**              Error stream            `2> errors.log`
  Append output               Adds output to a file   `>> log.txt`
  Combine output and errors   Redirect both           `command > all.log 2>&1`
  Pipe                        Connects commands       `cat file | grep text`

Other related commands: `less`, `head`, `tail`, `wc`, `grep`, `sort`,
`uniq`.

------------------------------------------------------------------------

## 9. Summary of Key Concepts

-   The shell serves as the intermediary between user and kernel.\
-   Bash provides both interactive and scripting capabilities.\
-   Scripts automate command sequences and can use variables,
    conditions, and loops.\
-   Proper use of quoting and redirection improves script reliability.\
-   Understanding stdin, stdout, stderr, and pipes is crucial for
    automation.

------------------------------------------------------------------------

## Recommended Practice

Students should reproduce all challenges and modify the scripts to: -
Log operations to a file. - Handle user input and exit codes. - Use
comments and proper indentation for clarity.
