# Week 1 - OS as a resource manager
--- 
## --- OS manages access to resources such as CPU, memory and disk.

Sharing the CPU
--- 
- Program alternates between
  - input
  - computation
  - output
- CPU is idle during I/O phases
- Multiprogramming
  - keep several programs active in memory and switches execution amoung them to optimise resources
  ![multigraph.PNG](attachments/74553981-653f-49b1-97d9-97d8f10e57d6/14ba0784.PNG)

CPU Virtualization
---
- Timesharing (multitasking)
  - extension of multiprogramming
  - CPU switches amoung all active computations to guarantee acceptable performance
  ![timeshare.PNG](attachments/74553981-653f-49b1-97d9-97d8f10e57d6/080633a6.PNG)
- Creating the illusion many CPUs exist
  - Virtual CPU = process
  - Timesharing
    - switch virtual onto physical CPU
    - stop virtual CPU
    - switch another virtual CPU onto physical CPU

KEY ABRACTION FOR CPU VIRTUALIZATION
- a process is the set of program instructions and execution state
- What state information is important?
  - Registers
    - program counter/instruction pointer
    - stack pointer and frame pointer
  - Memory (address space)
    - isolated

Process Control Block
---
- OS maintains a data structure for each process that stores state info
  - everything needed to stop running process, store and retrieve it
  ![pcb.PNG](attachments/74553981-653f-49b1-97d9-97d8f10e57d6/e1f31058.PNG)
  
Process creation
---
1. Load a program into memory into the address space of the process
    - program initially reside on disk in .exe format
    - OS performs lazy loading
      - loads code as needed
2. the programs run-time stack is allocated

3. the programs heap is created
4. the OS does some other initialization tasks
    - I/O setup

5. start the program running at entry point (main())
    - OS transfers control of the CPU to new process
