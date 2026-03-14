# Mini Shell 🐚

## 📌 Project Overview

By definition, the Operating System (OS) acts as an interface between the user and the hardware. Before GUI-based interfaces, systems were mainly operated using CLI (Command Line Interface). In Linux, the BASH shell reads commands and executes them using Linux Kernel System calls.

The goal of this project is to implement a **Mini Shell (msh)** that mimics the BASH shell using Linux Kernel System calls and IPC mechanisms like signals. It handles a set of commands, special keyboard actions like Ctrl+C, and can be extended for advanced functionalities like command history.

## 🔧 Features

### ⚙️ Command Execution
- Executes external commands entered by the user
- Creates a child process using `fork()` and executes using `exec()`
- Parent waits for child to complete using `wait()`
- Displays `msh>` prompt only after child completes
- Re-displays prompt if user enters empty command

### 📦 Special Variables
- `echo $?` — Prints exit status of last executed command
- `echo $$` — Prints PID of the msh shell
- `echo $SHELL` — Prints msh executable path

### 🚦 Signal Handling
- **Ctrl+C (SIGINT)** — Sends SIGINT to foreground program; re-displays prompt if no program running
- **Ctrl+Z (SIGTSTP)** — Stops foreground program and displays its PID

### 🛠️ Built-in Commands
- `exit` — Terminates the msh shell
- `cd` — Changes current working directory
- `pwd` — Displays current working directory

## 🧠 Pre-requisites

- Linux System Calls (`fork`, `exec`, `wait`, `getpid`)
- Signal handling (`signal`, `sigaction`, `SIGINT`, `SIGTSTP`)
- Process management concepts
- IPC mechanisms
- File descriptors and I/O redirection

## 🧰 File Structure

- `main.c` — Entry point, prompt display and command reading loop
- `execute.c` — Fork, exec and wait logic for external commands
- `builtin.c` — Built-in command implementations (cd, pwd, exit)
- `signal.c` — Signal handling for Ctrl+C and Ctrl+Z
- `parse.c` — Command parsing and tokenization
- `shell.h` — Header file with function prototypes and macros

## ⚙️ How to Compile & Run
```bash
# Compile
gcc main.c execute.c builtin.c signal.c parse.c -o msh

# Run
./msh

# Example usage
msh> ls -l
msh> pwd
msh> cd /home
msh> echo $?
msh> echo $$
msh> exit
```

## 🔁 How It Works

1. Shell displays `msh>` prompt and waits for user input
2. User enters a command
3. Shell parses the command and checks if it's built-in
4. If built-in → executes directly
5. If external → `fork()` creates child → `exec()` runs command → parent `wait()`s
6. After completion → prompt is displayed again
7. Ctrl+C sends SIGINT to running foreground process
8. Ctrl+Z stops running foreground process

## What I Learned

- Linux system calls — `fork()`, `exec()`, `wait()`, `getpid()`
- Signal handling using `signal()` and `sigaction()`
- Process creation and management in Linux
- Built-in command implementation in C
- Command parsing and tokenization
- How BASH shell works internally

## Author

**Miryala Vamshi**  
Embedded Systems Engineer  
📧 vamshimiryala2@gmail.com  
🔗 [LinkedIn](https://linkedin.com/in/vamshi-miryala-a7b71a347)
