## Treasure Hunt System

This project simulates a Treasure Hunt management system, developed as part of the Operating Systems course. It is structured in three phases, gradually introducing more advanced OS concepts such as processes, signals, pipes, and inter-process communication (IPC).

The application is written in C using POSIX system calls, focusing on low-level file operations and multi-process coordination.

---

## Phase 1 – treasure_manager.c

This phase implements a command-line interface (CLI) for managing hunts and treasures.

Each hunt is stored as a directory containing binary-encoded treasure data (coordinates, clues, values), using low-level file operations (read, write).

### Features:
- Add treasures to a hunt  
- List all treasures  
- View a specific treasure by ID  
- Remove a treasure  
- Remove an entire hunt  

### How to run:

    gcc -Wall -o exe treasure_manager.c
    ./exe add Hunt001
    ./exe list Hunt001
    ./exe view Hunt001 1
    ./exe remove_treasure Hunt001 1
    ./exe remove_hunt Hunt001

---

## Phase 2 – treasure_hub.c

This phase introduces a multi-process interactive system.

A monitor process (child) is created using fork() and communicates with the parent using signals and pipes.

### Features:
- Interactive command prompt  
- Monitor process controlled via signals (SIGUSR1, SIGUSR2)  
- Communication between processes using pipes  
- Real-time listing and viewing of hunts and treasures  

### How to run:

    gcc -Wall -o exe treasure_hub.c
    ./exe

### Example commands:

    prompt > startMonitor
    prompt > listHunts
    prompt > listTreasures Hunt001
    prompt > viewTreasure Hunt001 1
    prompt > stopMonitor
    prompt > exit

---

## Phase 3 – score_calculator.c + treasure_hub.c

This phase extends the system with parallel score computation.

For each hunt, a separate process is created (fork + exec) to calculate user scores, demonstrating multi-process scaling and workload distribution.

### Features:
- Parallel score computation (one process per hunt)  
- Aggregation of results via pipes  
- Improved inter-process coordination  

### How to run:

    gcc -Wall -o exe treasure_hub.c
    ./exe

### Example commands:

    prompt > startMonitor
    prompt > listHunts
    prompt > listTreasures Hunt001
    prompt > viewTreasure Hunt001 1
    prompt > calculateScore
    prompt > stopMonitor
    prompt > exit

---

## Key Concepts Demonstrated

- Process management: fork(), exec()  
- Inter-process communication (IPC): pipe()  
- Signal handling: SIGUSR1, SIGUSR2  
- Low-level file I/O: read(), write()  
- Multi-process architecture:  
  - Parent process (hub)  
  - Child process (monitor)  
  - Grandchild processes (score calculators)  

---

## Why this project matters

This project demonstrates a solid understanding of Operating Systems fundamentals by combining low-level programming with a structured, multi-process architecture. It highlights the ability to build systems that rely on process coordination, IPC mechanisms, and efficient resource management, without relying on high-level abstractions.
