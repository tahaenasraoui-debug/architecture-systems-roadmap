# Computer Architecture & Systems Roadmap

 ![License](https://img.shields.io/badge/license-MIT-green.svg) ![language](https://img.shields.io/badge/language-C%20%2B%20assembly-blue.svg) ![focus](https://img.shields.io/badge/focus-hardware%20to%20OS-informational.svg)

Build a computer from logic gates up: CPU, memory, operating system, compiler, and distributed systems. The goal is to remove the magic from everything below your code.

## Table of Contents

1. [Workflow Overview](#workflow-overview)
2. [Prerequisites](#prerequisites)
3. [Phase 1: Gates to CPU](#phase-1-gates-to-cpu)
4. [Phase 2: The Programmer's View](#phase-2-the-programmers-view)
5. [Phase 3: Operating Systems](#phase-3-operating-systems)
6. [Phase 4: Languages & Compilers](#phase-4-languages--compilers)
7. [Phase 5: Distributed Systems](#phase-5-distributed-systems)
8. [Capstone Projects](#capstone-projects)
9. [Repository Layout](#repository-layout)
10. [Engineering Rules](#engineering-rules)
11. [Exit Criteria](#exit-criteria)

---

## Workflow Overview

```
 Logic gates --> CPU design --> Assembly + C --> Memory + caches
                                                      |
 Distributed <-- Compilers <-- Operating systems <---+
 systems         (interpreters)  (processes, virtual memory, FS)
```

## Prerequisites

- [ ] Basic programming in any language, C preferred
- [ ] Comfortable in Linux and the terminal
- [ ] Binary, hexadecimal, and boolean algebra

## Phase 1: Gates to CPU

Goal: Build a working computer from NAND gates and understand how it executes instructions.

| Resource | Type | Why |
|----------|------|-----|
| [Nand2Tetris](https://www.nand2tetris.org/) | Project course | Build a computer, assembler, VM, and compiler |
| [Ben Eater: Build an 8-bit Computer](https://eater.net/8bit) | Videos and kits | See a CPU on a breadboard |
| [Digital Design and Computer Architecture: RISC-V Edition](https://pages.hmc.edu/harris/ddca/ddcarv.html) | Textbook site | Formal CPU design, pipelining |
| [Logisim Evolution](https://github.com/logisim-evolution/logisim-evolution) | Tool | Digital logic simulator |

- [ ] Nand2Tetris projects 1 to 6 (gates through assembler)
- [ ] Design a single-cycle RISC-V CPU in Logisim
- [ ] Add pipelining and identify hazards

**Deliverables**
- [ ] `hardware/` with HDL or Logisim files for ALU and CPU
- [ ] `docs/cpu_design.md` explaining datapath and control

## Phase 2: The Programmer's View

Goal: Know what the machine does with your C code.

| Resource | Type | Why |
|----------|------|-----|
| [Computer Systems: A Programmer's Perspective](http://csapp.cs.cmu.edu/) | Textbook site | Machine code, memory, linking, concurrency |
| [Beej's Guide to C](https://beej.us/guide/bgc/) | Free book | Practical C |
| [Compiler Explorer](https://godbolt.org/) | Tool | See assembly for any snippet |
| [What Every Programmer Should Know About Memory](https://akkadia.org/drepper/cpumemory.pdf) | Paper | Caches, TLBs, NUMA |

- [ ] CS:APP: data representation, machine-level programs, memory hierarchy
- [ ] Read assembly output for loops, function calls, and structs
- [ ] Measure cache effects with a matrix-multiply benchmark

**Deliverables**
- [ ] `src/c/` with data lab, bomb-style reverse-engineering notes, and cache benchmark
- [ ] `docs/cache_report.md` with measured numbers

## Phase 3: Operating Systems

Goal: Understand processes, virtual memory, scheduling, and file systems by building them.

| Resource | Type | Why |
|----------|------|-----|
| [Operating Systems: Three Easy Pieces](https://pages.cs.wisc.edu/~remzi/OSTEP/) | Free book | Virtualization, concurrency, persistence |
| [xv6-riscv](https://github.com/mit-pdos/xv6-riscv) | Teaching OS | Small, readable Unix-like kernel |
| [MIT 6.1810 Operating System Engineering](https://pdos.csail.mit.edu/6.828/) | Course page | Use the xv6 labs only, skip the lectures |
| [OSDev Wiki](https://wiki.osdev.org/) | Wiki | Reference for bare-metal work |

- [ ] OSTEP: virtualization (CPU and memory) then concurrency then persistence
- [ ] Read xv6 source: boot, syscalls, scheduler, file system
- [ ] Complete xv6 labs on system calls, page tables, and traps

**Deliverables**
- [ ] `src/os/xv6-labs/` branches per lab
- [ ] A shell in C with pipes and redirection in `src/c/shell/`
- [ ] A `malloc` implementation with tests

## Phase 4: Languages & Compilers

Goal: Understand how code becomes execution.

| Resource | Type | Why |
|----------|------|-----|
| [Crafting Interpreters](https://craftinginterpreters.com/) | Free book | Build a tree-walk interpreter and a bytecode VM |

- [ ] Part I: tree-walk interpreter in a high-level language
- [ ] Part II: bytecode VM in C
- [ ] Add one language feature of your own

**Deliverables**
- [ ] `src/lang/` with interpreter and VM
- [ ] Test suite of scripts with expected output

## Phase 5: Distributed Systems

Goal: Reason about consensus, replication, and failure.

| Resource | Type | Why |
|----------|------|-----|
| [MIT 6.824 Distributed Systems](https://pdos.csail.mit.edu/6.824/) | Course page | Use the labs, they are the value |
| [The Raft Consensus Algorithm](https://raft.github.io/) | Site and paper | Readable consensus algorithm |
| [Designing Data-Intensive Applications](https://dataintensive.net/) | Book | Replication, partitioning, consistency |

- [ ] Read the Raft paper twice
- [ ] Implement Raft leader election and log replication
- [ ] Build a replicated key-value store on top

**Deliverables**
- [ ] `src/dist/raft/` with tests that inject network partitions
- [ ] `docs/consistency.md` stating the guarantees your store gives

## Capstone Projects

- [ ] Hardware: a working CPU running a program you assembled yourself
- [ ] Software stack: your assembler, VM, and compiler running a game or program on your CPU (Nand2Tetris full stack)
- [ ] OS: add a feature to xv6 (for example, a new syscall or copy-on-write fork)
- [ ] Distributed: a fault-tolerant key-value store on Raft

## Repository Layout

```
architecture-systems/
├── README.md
├── hardware/                 # Logisim / HDL designs
├── src/
│   ├── c/
│   │   ├── shell/
│   │   └── malloc/
│   ├── os/
│   │   └── xv6-labs/
│   ├── lang/                 # interpreter and VM
│   └── dist/
│       └── raft/
├── tests/
├── bench/
└── docs/
    ├── cpu_design.md
    ├── cache_report.md
    └── consistency.md
```

## Engineering Rules

These are strict. A phase is not complete until its deliverables follow all of them.

### 1. Daily 1:3 Theory-to-Building Ratio

- [ ] For every 1 hour of reading or watching, spend 3 hours building, solving, or running labs
- [ ] Log hours in `docs/log.md` at the end of each session
- [ ] No new chapter until the previous one has working code or a written lab report

### 2. Git Branch Hygiene

- [ ] `main` is always green and never receives direct commits
- [ ] One branch per deliverable: `phase-N/short-description`
- [ ] Small commits with imperative messages; squash-merge via PR after checks pass
- [ ] Delete branches after merge

### 3. Quality Gates

- [ ] C builds clean with `gcc -Wall -Wextra -Werror` and sanitizers (`-fsanitize=address,undefined`)
- [ ] [valgrind](https://valgrind.org/) reports no leaks on tests
- [ ] [clang-tidy](https://clang.llvm.org/extra/clang-tidy/) passes; tests use [Unity](https://github.com/ThrowTheSwitch/Unity) or a simple custom harness
- [ ] Debug with `gdb`; commit the failing test before the fix

### 4. Branch-Specific Rules

- [ ] Read the source of one real system per phase (xv6, a small interpreter, Raft)
- [ ] Benchmarks include methodology and raw numbers, not just conclusions
- [ ] Concurrency code ships with a stress test and a thread sanitizer run
- [ ] No copy-pasting lab solutions from the internet

## Exit Criteria

- [ ] Trace a C function call through the stack, registers, and cache
- [ ] Explain what happens on a page fault from trap to return
- [ ] Build a language interpreter without a tutorial open
- [ ] Explain why Raft is safe under partitions and where it sacrifices availability
