# Week 2 - Virtualizing the CPU
---
Process Abstraction
---
  - When you run a .exe file, the OS creates a process
  - multiple programs are running at a time
  - OS is timesharing CPU
    - How?
    - Policy: which process to run
    - Mechanizm: how to "context switch" between processes

What constitutes a process?
---
- A unique identifier (PID)
- Memory image
  - Code and data (static)
  - stack and heap (dynamic)
- CPU context: registers
- File descriptors
  - pointers to open files/ devices

How does OS create process?
---
- Allocates memory and creates memory image
  - load code and data from disk
  - create runtime stack and heap
- Open basic files
  - STDIN, OUT, ERR
- Initialize CPU registers

CPU state of a process
---
![PSW.PNG](attachments/b258798d.PNG)

#### Process Sceduling: A computer has one or more CPUs, which execute the instructions of programs. Modern OSs are preemptive mulitasking systems.
- Multitasking means that multiple processes can simultaneously reside in memory and each uses the CPU(s)
- Preemptive means that the rules governing whoch processes recieve use of the CPU and for how long are determined by the kernal process scheduler(rather than processes themselves)

---
![CPUprocessSceduler.PNG](attachments/0f1737a1.PNG)

![ee015273.png](attachments/ee015273.png)

OS data structures
---
- OS maintains a data structure of all active processes
- Information about each process is stored in a process control block
  - Process Identifier
  - Process state
  - Pointers to other related processes
  - CPU context of the process
  - Pointer to memory location
  - Pointer to open files

Library functions vs API
---
- Early OSs used libraries of function calls to replace commonlt used functions
  - e.g. low level I/O handling code
- Moving beyond libraries, the OS began to take on a more central role in managing the machine
  - code run on behalf of theOS was determined to be special

API = Application Programming Interface = functions available to write user programs.
- API provided by OS is a set of "system calls"
  - System call is a function call into the OS code that runs at a higher priviage level
  - Sensitive operations are allowed only at a higher privilage level
  - Some "blocking" system calls cause the process to be blocked and descheduled


POSIX API: a standard set of system calls that an OS must implement.
---
- programs written to the POSIX API can run on any POSIX compliant OS
- ensures program portability

Dual mode operation and protected control transfer
---
- **Kernal**: core of operating system that manages resourses and provides services to other parts of the OS
- **Kernal Mode**: execution with the full privilages of the hardware
  - READ AND WRITE TO ANYWHERE
- **User mode**: processes do not have full access to hardware resources.
  - Limited to privilages granted by kernal
    - limited memory access to prevent users from overwriting kernal code

- Want to allow the kernal to *carefully expose key functionality* to user process

Switching between processes
---
- *Cooperative approach*: Wait for system calls
  - **Trap** instruction
    - jump into kernal
    - raise privilidge level to kernal mode

  - **Return-from-trap** instruction
    - return into the calling user program
    - reduce priviledge level back to user mode
- *non-cooperative approach*: OS takes control with interupts