# CS-3113-OS-Project-1c
Project 1C readme

CS 3113 - Operating Systems
Teacher: Cristian Grant

Code written by: Sean Burdett


Description

1) Summary of how to compile and use this shell

2) Description of each internal command line feature

3) Description of known bugs

4) a) What happens when Ctrl-C is pressed during
        I. Command execution?
        II. User entry of commands?
        III. Would SIGINT tapping control this better?
   b) Other polish questions

1. Summary

This shell was created as part of the CS 3113 Operating System course. It is meant to familiarize students with the functions of this Linux
command line. The shell has many features including:

        - reads in a line of keyboard input at a time, parsing it into tokens that are separated by white spaces
        - the prompt for each line is taken from the current working directory
        - supports I/O redirection. Any point where a command outputs to User it can instead be redirected to another file. At certain command arguments the User may designate to instead use a file as source of input rather than the keyboard.
        - accepts a bash file in initial shell call "./1c bashfile" and will run the bashfile as input
        - the shell can be started by the "make" command using the given makefile
        - "make all" and "make clean" can compile
        - fork and exec are used for the system call. Fork creates two processes where one process called the 'child' runs the exec command which creates another instance that runs the particualr system call. The parent process waits for the child to finish, unless the user desgnates a '&' at the end of the command line.

2. Commands

        cd - change the current directory and update the envvironment
        clr - clear the screen
        dir - list the current directory contente (ls -al)
        dir <directory> - list the given directory contents (ls -al <directory>)
        environ - list all the environment strings
        help - display help manual
        pause - stops the command line and continues when ENTER is pressed
        echo - repeats the line of input
        quit - quit from the program with a zero return value

        external commands -  all other command line inputs are executed via a fork and exec

input redirection - 

        when a command line includes '<' input redirection immediately begins after the first command.
                    '<' must be delimited by white space in the command line and then followed by desired input <fileName>
output redirection - 

        when a command line includes '>' output redirection is turned on in the child process where the exec command prints out the output to the designated file. '>' must be delimited by white space in the command line and then followed by desired output <fileName>. Output file is created if it doesnt exist and truncated if it does.
output redirection appending - 
                
       '>>'  must be delimited by white space in the command line and then followed by desired output <fileName>. Output file is created if it doesnt exist and appended too if it does.


3. Bugs

- "make clean" will compile however the makefile must be edited to remove a specific file


4. a) What happens when Ctrl-C is pressed during
        I. Command execution? 
        
        Executuion stops immeditely and the shell is exited.
II. User entry of commands?
        
        The shell is exited immediately.
III. Would SIGINT trapping control this better?

        While more code would be necessary to control the signal this would give more control and security to the user. If the shell was using
        any memory in the heap controlling interrupt signal would allow the shel to clean up any object before exiting. Also if the user
   b) Other polish questions

        All array arguments are checked for existence often using

        if (args[i])

        Input redirection existence and reading permission is checked.

        The makefile does compile for "make", "make all", "make clean"
