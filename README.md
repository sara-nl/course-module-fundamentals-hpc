# Hands-on fundamentals of high-performance computing

This hands-on session introduces basic usage of the Snellius supercomputer at SURF. You will learn how to:
* connect to Snellius,
* understand the Linux environment,
* navigate the file system,
* compile a simple parallel program,
* submit and monitor jobs using the SLURM workload manager.

## 1. Accessing Snellius and exploring the Linux environment

> **Objective:** Connect to Snellius and retrieve basic system and user information. Verify your access and become familiar with the Linux environment. Log this information in your home directory, in a file called `<username>.dat`.
> 
>| #  | Question                                      | Command                               | Environment variable |
>|----|-----------------------------------------------|---------------------------------------|----------------------|
>| 1  | What is your username?                        | `whoami`                              | `echo $USER`         |
>| 2  | What is your current working directory?       | `pwd`                                 | `echo $PWD`          |
>| 3  | What is your home directory?                  | _none_                                | `echo $HOME`         |
>| 4  | Which login node are you on?                  | `hostname`                            | `echo $HOSTNAME`     |
>| 5  | When did you last log in to Snellius?         | `last -n 1 $USER`                     | _none_               |
>| 6  | How much storage quota do you have?           | `myquota`                             | _none_               |
>| 7  | What is your compute budget and usage?        | `accinfo`                             | _none_               |

### Connecting to Snellius

To access Snellius, connect via SSH ([troubleshooting guide](https://servicedesk.surf.nl/wiki/spaces/WIKI/pages/30660265/Snellius+FAQ#SnelliusFAQ-TroublewithconnectingtoSnellius)):
```
ssh <username>@snellius.surf.nl
```

### Creating your first file

After connecting to Snellius, your Shell will be located at your home directory: `/home/<username>`. This is a common setup in Linux environments. If you are using an `scur` login, your home directory should be empty. Let's create your first file, called <username>.dat. There, we will log some of the environment values during the following steps.
```
[<username>@int6 ~]$ touch <username>.dat
[<username>@int6 ~]$ ls
<username>.dat
```

> 🖥️ **Editing files in the Shell**
>
> There are multiple ways to edit files in a Shell. Two common options are:
> * Shell editors like [`vim`](https://www.vim.org) or [`nano`](https://www.nano-editor.org), for manual editing.
> * Output [redirection](https://www.gnu.org/software/bash/manual/html_node/Redirections.html) using `>` for overwriting or `>>` for appending.

### Exploring the Linux environment

When you log in to Snellius (or any Linux-based system), you interact with the system through a shell. The shell is a command-line interpreter that reads and executes commands. It also gives access to environment variables—named values used to configure your session or store user-specific details.

For example, you can check your username using the environment variable $USER. This will return your SURF username, which is set automatically at login. 
```
[<username>@int6 ~]$ echo $USER
<username>
```

You will encounter environment variables often in this course, for tasks such as selecting compilers, accessing file paths, or configuring MPI jobs.

> 📦 **Why do environment variables exist?**
> 
> You’re working on a shared system (Snellius), with thousands of users and hundreds of programs. Every time you run a program, it needs to know who you are, where your files are, what software you use, what language or region settings you prefer.
> 
> Typing these details every single time would be painful and error-prone. That’s where environment variables come in: they act as a set of predefined, user-specific values that make the shell context-aware and help programs behave correctly without manual input every time.
> 
> Let’s say John Doe wants to create a folder for logs and save a file there. John could hardcode:
> ```
> mkdir /home/johnd/logs
> echo "My log entry" > /home/johnd/logs/run.log
> ```
> 
> But this will fail for everyone else, because `/home/johnd/` only works for John. Instead, John could use the environment variable `$HOME`, which automatically expands to the correct home directory for any user:
> ```
> mkdir -p $HOME/logs
> echo "My log entry" > $HOME/logs/run.log
> ```
> 
> ✅ Now the script works for everyone, not just John. This is essential in shared environments, job scripts, and automation.


