# Execution Model

## Runtime Components

### General Computing Model

```
host machine
  process (global resources)
    thread (runs machine code)
```

Each process represents a program running on the host. Think of each process
itself as the data part of its program. Think of the process threads as the
execution part of the program.  
The process, as the data part, is the execution context in which the program
runs. It mostly consists of the set of resources assigned to the program by the
host, including memory, signals, file handles, sockets and environment
variables.  
Processes are isolated and independent from one another. The host manages the
process access to its assigned resources, in addition to coordinating between
processes.  

Each thread represents the actual execution of the program's machine code,
running relative to the resources assigned to the program's process. It is
strictly upto the host how and when the execution takes place.  

**A Python Program akways starts with exactly 1 thread** The program may grow
to run in multiple simultaneous threads.  
Unlike processes, threads in a process are not isolated and independent from
one another.  
All threads in a process share all the process's resources.  

### Pythons Runtime Model

```
host machine
  process
    python global runtime
      python interpreter
        thread
          python thread state
```

The runtime may grow to include multiple interpreters and each interpreter may
grow to include multiple thread states.  

Python runtime consists of:
* global runtime state
* interpreters
* thread states

Runtime ensures all that state stays consistent over its lifetime, particularly
when used with multiple host threads.  

The global runtime, at the conceptual level, is just a set of interpreters. 
While those interpreters are isolated and independent from one another, they
may share some data or other resources  
The runtime is responsible for managing these resources safely.  
The external utility of the global runtime is limited to managing interpreters.

When machine code executing in a host thread interacts with the python runtime,
it calls into Python in the context of a specific interpreter.  
Each interpreter completely encapsulates all of the non-process-global, non
thread specific state needed for the Python runtime to work.  
The runtime ensure multiple threads using the same interpreter will safely
share it between them.  

For thread specific runtime state, each interpreter has a set of thread states,
which it manages, in the same way the global runtime contains a set of
interpreters.  
It can have thread states for as many host threads as it needs.  

Once a program is running, a new Python threads can be created using the
threading module. Additional processes can be created using the os, subprocess
and the multiprocessing modules.  
Interpreters can be created and used with the interpreters module.  
Coroutines can be run using asyncio in each interpreter, typically only in a
single thread.  

