## Limited Direct Execution

CPU achieves virtualization by time sharing the CPU. Implemented through LDE, allowing for security and a method to stop the process from running and switch to another one.


LDE: limit what a process can do without OS assistance. Need to set up:

Modes
- Process created in user-mode. Restricted (ie. can't issue I/O request), and doing prohibited things will cause process to be killed.
- Kernel mode: I/O requests, execute restricted instructions
- To allow privileged instructions, perform a system call (access file syste, create/destroy processes, communicate with other processes, allocate memory)

Executing a system call (trap instruction)
1. Jumps into kernel and raises privilege to kernel mode
2. When finish, OS calls return-from-trap instruction to return to user program and reduce privilege level
3. Push PC, flags, and other registers into kernel stack => return from trap will pop these values from stack and resume execution
4. Trap table contains locations of trap handlers, so we know where to jump when syscalls are made.

Phases of LDE
1. Initialize trap table with a privileged instruction
2. Kernel sets up things to start executing to process, then switches CPU to user mode. When process wishes to issue system call, it traps into OS, then returns back. 

How can OS regain control of CPU?
1. Cooperative approach: OS regains control of CPU by waiting for system call or illegal operation to take place
2. Noncooperative approach: Timer interrupt every few miliseconds. At this point, interrupt handler in OS runs and OS regains control of CPU


Saving and Restoring Context
- Once OS has control, needs to decide whether to continue running process or switch to a different one (determined by a scheduler)
- If change, execute a context switch (save register values onto its kernel stack, restore for the new process)
- User registered saved onto process kernel stack. During context switch, KERNEL REGISTERS are saved by OS into memory of the process structure of the process