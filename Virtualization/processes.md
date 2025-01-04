## Processes

Process: a running program
Time-sharing the CPU allos users to run as many concurrent processes as they like => **VIRTUALIZATION**

We can switch from one program to another with a **context-switch**

Process structure
- Address space
- Program counter (which instruction program will execute next)
- Stack/frame pointer

Steps to running a program
1. Load code and static data (initialized variables) into address space
    - Programs reside on disk in an executable format
2. Allocate a runtime stack (local variables, function parameters, return addresses)
3. Allocate heap
4. Initialize three file descriptors: stdin, stdout, stderr
5. Start program at main() => from here, OS transfer control of program to CPU

Process can be: running, ready, or blocked (not ready to run unless some other event takes place)