# 4. Operating System and Information Systems

## 4.1 Basic knowledge of Operating System

### Q.1 Define OS, functions and its types. [LQ]

→ It is system software that manages computer hardware and acts as an intermediary between the user (or application programs) and the hardware.

**Two Views:**
1. **Resource manager:** allocates CPU, memory and devices among competing programs.
2. **Extended machine:** hides hardware complexity behind simple services.

### Structure of OS

```
        +--------------------------------------------------+
        |                      Users                       |
        +--------------------------------------------------+
User    | Application programs: banking software, browser, |
mode    | office tools                                     |
        +--------------------------------------------------+
        | Shell & system utilities (command line or        |  <-- system calls
        | graphical interface)                             |
        +--------------------------------------------------+
Kernel  | KERNEL: process, memory, file & device           |
mode    | management; protection                           |
        +--------------------------------------------------+
        | Hardware: processor, memory, disks, I/O devices  |
        +--------------------------------------------------+
```
*Fig: Position of OS in a Computer system*

### Major functions

1. **Process Management**
   → create, schedule, synchronise, terminate processes; deadlock handling
2. **Memory Management**
   → allocate and free main memory; virtual memory by paging and swapping.
3. **File Management**
   → create, name, organise and protect files and directories.
4. **Device (I/O) Management**
   → drivers, buffering, caching, spooling
5. **Secondary Storage management**
   → free-space management, allocation, disk scheduling
6. **Protection and security**
   → authentication and access control
7. **User Interface**
   → Command-line (shell) or GUI.
8. **Others**
   → networking, error detection, accounting.

### Types of OS

- On the basis of processing
- On the basis of UI

### 1. On the basis of processing

#### a. Single user OS
→ 2 types
- (i) Single user → single task
- (ii) Single user → multiple task at a time (t1, t2)

#### b. Multi-user OS
→ sharing of data and information among different user.

**Disadvantage:** expensive hardware for mainframe computer.

**Example:** UNIX, Window 2000

#### c. Multiprogramming OS
→ execute multiple jobs by using a single CPU at the same time. User can't directly interact with the system. Ex: UNIX, Window 95 etc.

```
 [Word]      [Web Browser]      [Email]
    \             |              /
   process     process       process
      \           |           /
               [  OS  ]
                  |
               [ CPU ]
```

#### d. Multi Processing OS
→ Shared work. Ex: core banking database server, UNIX based OS, server Based OS, Linux etc.

```
 [CPU 1] <-----> [Main Memory] <-----> [CPU 2]
    ^                 ^  ^                ^
    |                 |  |                |
    v                 |  |                v
[I/O processor] <-----+  +-----> [I/O processor]
    ^                                     ^
    |                                     |
    v                                     v
[I/O Units]                         [I/O Units]
```

#### e. Batch OS
→ similar jobs collected and run with no user interaction

Ex: Day-end interest posting, bank-statement generation

```
User 1 --> [Job 1] --\
User 2 --> [Job 2] ---> (Computer Operator) --> [Batch 1] --\
User 3 --> [Job 3] --/                      --> [Batch 2] ---> [OS]
```

#### f. Time sharing OS (multi-tasking)
→ CPU time divided into small slices among many users.

Ex: Windows, UNIX/Linux server used by many tellers.

```
              User 3      User 4
        User 2      [CPU] --> User 5 (Active state)
              User 1      User 6 (Ready state)
```
*(Users waiting in the circle are in "Used state"; the CPU serves one user at a time.)*

#### g. Real time OS
→ Response within fixed deadline. Ex:- ATM transaction control, airbag controller, Traffic Light, Air Traffic Control system, Hotel Reservation System.

#### h. Distributed OS
→ Many computers appear as one system. Ex:- Clustered services

#### i. Network OS
→ share information over a network. Ex:- Microsoft Windows Server 2003, Microsoft Windows Server 2008, UNIX, Linux, MacOS X, Novell NetWare, BSD.

```
 [Agent]    [Agent]     [Agent]
      \        |        /
   +--------------------------+
   |  Server software         |------ [Administrator Panel]
   |  Video Data Store        |
   +--------------------------+
      /        |        \
 [Agent]    [Agent]    [Agent]
```

#### j. Embedded OS (mobile)
→ Small built for one device. Used in smartphones, TVs, Automobiles (Car ECUs), IoT Devices, Medical Equipment and so on. Ex:- ATM, Android/iOS mobile banking.

### 2. On the basis of UI

| Basis | Graphical User Interface (GUI) | Command Line Interface (CLI) |
|---|---|---|
| Input | Mouse, Icons, menus, touch | Typed commands |
| Resource use | Higher memory and CPU | Very low |
| Interface | multiuser multitasking | single-user single tasking |
| User Friendly | More | Less |
| Performance | Slow | Fast |
| Example | Windows, Android | DOS, UNIX shell |

**Conclusion:** A bank uses batch for day-end work, time sharing and multiprocessing for online transactions and embedded systems in ATMs.

---

## 4.2 Process Management and Scheduling

### Q.1 Scheduling Algorithms

**Pre-emptive**
- Shortest Remaining time first (SRTF)
- Longest Remaining time first (LRTF)
- Round Robin
- Priority based (It can be the part of non-pre-emptive)

**Non Pre-Emptive**
- First Come First Serve (FCFS)
- Shortest Job First (SJF)
- Longest Job First (LJF)
- Highest Response Ratio Next (HRRN)
- Multi Level Queue

### Numerical

**Example 1:** Four processes arrive at time 0 in the order P1 to P4, where RR quantum = 4.

| Process | P1 | P2 | P3 | P4 |
|---|---|---|---|---|
| Burst time (ms) | 8 | 4 | 2 | 6 |
| Priority (1 = highest) | 3 | 1 | 4 | 2 |

```
FCFS        | P1        | P2     | P3  | P4        |
            0           8        12    14          20

SJF         | P3  | P2     | P4        | P1              |
            0     2        6           12                20

Priority    | P2     | P4        | P1              | P3  |
            0        4           10                18    20

Round Robin | P1     | P2     | P3  | P4     | P1     | P4  |
(q=4)       0        4        8     10       14       18    20
```
*Fig: Gantt charts of four algorithms for the same set of process*

**Formula,**
- Waiting time (WT) = Turnaround time (TAT) − burst time (i.e. 'b')
- Turnaround time (TAT) = completion time − arrival time
- Average (WT) = ΣWT / Total no. of Process
- Average TA = average WT + average burst

Suppose for FCFS for P1:
- TAT = 8 − 0 = 8
- WT = 8 − 8 = 0

similar for others...

| Algorithm | Order of execution | Waiting time of P1,P2,P3,P4 | Average waiting | Average TAT |
|---|---|---|---|---|
| FCFS | P1, P2, P3, P4 | 0, 8, 12, 14 | 8.5 ms | 13.5 ms |
| SJF | P3, P2, P4, P1 | 12, 2, 0, 6 | 5 ms | 10 ms |
| Priority | P2, P4, P1, P3 | 10, 0, 18, 4 | 8 ms | 13 ms |
| RR (q=4) | P1, P2, P3, P4, P1, P4 | 10, 4, 8, 14 | 9 ms | 14 ms |

**Example 2 (with arrival times)**

P1 to P4 arrives at 0, 1, 2, 3 ms with bursts 6, 3, 8, 2 ms. RR (q) = 2 ms

| Process | P1 | P2 | P3 | P4 |
|---|---|---|---|---|
| Arrival time | 0 | 1 | 2 | 3 |
| Burst time | 6 | 3 | 8 | 2 |

avg. burst = (6+3+8+2)/4 = 4.75

Now,

```
FCFS | P1        | P2     | P3                | P4  |
     0           6        9                   17    19

SJF  | P1        | P4  | P2     | P3                |
     0           6     8        11                  19

RR   | P1 | P2 | P3 | P4 | P1 | P2 | P3 | P1 | P3 | P3 |
(q=2)0    2    4    6    8    10   11   13   15   17   19
```

| Algorithm | Order of execution | WT of P1,P2,P3,P4 | Avg. WT | Avg. TAT |
|---|---|---|---|---|
| FCFS | P1, P2, P3, P4 | 0, 5, 7, 14 | 6.5 ms (26/4) | (6.5 + 4.75) = 11.25 ms |
| SJF | P1, P4, P2, P3 | 0, 7, 9, 3 | 4.75 ms | 9.5 ms |
| RR | P1, P2, P3, P4, P1, P2, P3, P1, P3, P3 | 9, 7, 9, 3 | 7.5 ms | 12.25 ms |

**Conclusion**
→ No single algorithm is best for everything. Batch work favors SJF, interactive systems favor RR and real systems combine them in multilevel queues.

---

### Q.2 Deadlocks, RAG and Banker's Algorithm

→ Deadlock is a state where 2 or more process wait indefinitely, can arise only if all four of the following hold at the same time:

1. **Mutual exclusion:** at least one resource can be used by only one process at a time.
2. **Hold and wait:** a process holds one resource while waiting for another.
3. **No preemption:** a resource cannot be forcibly taken, it is released voluntarily.
4. **Circular wait:** a closed chain of processes exists where each waits for a resource held by the next.

**Example with diagram**

```
(a) Cycle: deadlock                    (b) No cycle: no deadlock

   assigned  [R1]  requesting             as.   [R1]
 (P1) <-------      -------> (P2)       (P1) <----
   |                          ^                       
   | requesting      assigned |        (P1) -- req. --> [R2] -- as. --> (P2)
   +-------> [R2] ------------+
```

**Methods of handling deadlocks**

| Method | Idea |
|---|---|
| Prevention | Break one of the four conditions |
| Avoidance | stay in a safe state (Banker's algo) |
| Detection and recovery | detect (wait-for graph), then terminate process or preempt resources |
| Ignore (ostrich approach) | Used by most general-purpose OSs |

**Prevention of each condition**
- **Mutual exclusion:** make resources shareable (read-only files).
- **Hold and wait:** request all resources at once before starting.
- **No preemption:** allow OS to take resources from a lower-priority process.
- **Circular wait:** number resources and require requests in increasing order.

**Banker's algorithm (Dijkstra)** / (Deadlock Avoidance / Deadlock Detection)

**Example:** A system has 8 instances of resource A and 6 of resource B. Using the Banker's algorithm, find whether the given state is safe, and whether a request of (1,1) by P4 can be granted.

- Allocation: P1 (2,1), P2 (2,1), P3 (1,1), P4 (1,2)
- Maximum: P1 (4,3), P2 (3,2), P3 (5,2), P4 (2,4)

→ Given,
- Total resources = (8,6)
- Need = Max − Allocation

| Process | Allocation (A,B) | Max (A,B) | Need (A,B) |
|---|---|---|---|
| P1 | (2,1) | (4,3) | (2,2) |
| P2 | (2,1) | (3,2) | (1,1) |
| P3 | (1,1) | (5,2) | (4,1) |
| P4 | (1,2) | (2,4) | (1,2) |
| Sum | (6,5) | | |

Now,
Available = Total resources − sum of Allocation
= (8,6) − (6,5)
= (2,1)

| Process | Allocation (A,B) | Maximum Need | Available | Remaining Need |
|---|---|---|---|---|
| P1 | (2,1) | (4,3) | (2,1) | (2,2) |
| P2 | (2,1) | (3,2) | (4,2) | (1,1) |
| P3 | (1,1) | (5,2) | (5,3) | (4,1) |
| P4 | (1,2) | (2,4) | (6,5) | (1,2) |
| | (6,5) | | | |

Available = current available + allocation

Available ≥ Remaining Need

∴ P2 → P3 → P4 → P1 (Safe Sequence)

Available (6,5) of P4 ≥ Req remaining need (1,1) by P4,
∴ safe so granted.

---

### Q.3 Program vs process vs thread

| Basis | Program | Process | Thread |
|---|---|---|---|
| Nature | Passive; a file on disk | Active; program in execution | Active; part of process |
| Creation and switching | Not applicable | Slow and costly | Fast; less state to save |
| Communication | Not applicable | Through inter-process communication | Directly through shared memory |
| Effect of a fault | None | other processes are protected | May bring down the whole process |

```
(a) A process in memory          (b) A process with three threads

+-------------+                  +--------------------------------------------+
| Stack       | ↓ grows down     | Shared: code, data, heap, open files       |
|-------------|                  |  +----------+ +--------------+ +----------+ |
| free space  |                  |  | Thread 1 | | Thread 2     | | Thread 3 | |
|-------------|                  |  | registers| | reg, program | | reg, PC  | |
| Heap        | ↑ grows up       |  | PC       | | counter      | |          | |
| Data        |                  |  | own stack| | own stack    | | own stack| |
| Text        |                  |  +----------+ +--------------+ +----------+ |
+-------------+                  +--------------------------------------------+
```

**Process states**

```
                 admitted             dispatch                exit
     (New) ------------------> (Ready) ------------> (Running) ------------> (Terminated)
                                  ^  ^   <-------------   |
                                  |  |      interrupt     |
                  I/O or event    |  +-----(Waiting)<-----+  I/O or event wait
                  completed       |
                                  +--------(Waiting)
```
*Fig: 5-state process model*

| Transition | Cause | Done by |
|---|---|---|
| New → Ready | Process admitted to memory | Long-term scheduler |
| Ready → Running | Process selected (dispatch) | Short-term scheduler and dispatcher |
| Running → Ready | Time slice expired / higher priority arrived | Timer Interrupt |
| Running → Waiting | I/O request or event wait | The process itself |
| Waiting → Ready | I/O or event completed | Interrupt handler |
| Running → Terminated | Normal exit or abort | Process or OS |

**Schedulers**

| Scheduler | Controls | Frequency |
|---|---|---|
| Long-term / Job Scheduler | which jobs enter memory (degree of multiprogramming); mix of (I/O-bound and CPU-bound jobs) | Rare (New → Ready) |
| Short-term / CPU Scheduler | which ready process runs next | Very frequent (milliseconds) |
| Medium-term / Swapper | swaps processes out and in to reduce memory load (Ready/Waiting ↔ Suspended) | Occasional |

→ The dispatcher gives CPU control to the selected process.

```
                         time slice expired
                   +-----------------------------+
                   v                             |
[Job pool   ] long-term  [Ready queue ] short-term  [ CPU ] ------> [Exit]
[(on disk)  ]--scheduler->[(in memory)]--scheduler->[     ]
                              ^   ^                    |
        medium-term           |   | I/O complete       | I/O request
        scheduler (swapping)  |   |                    v
                              |   +------------ [I/O waiting queue]
                              v
                    [Swapped-out processes]
```
*Fig: scheduling queues and the three schedulers*

---

## 4.3 DOS, UNIX and Windows Operating Systems

### LQ.1 Compare DOS, UNIX and Windows

| Basis | DOS | UNIX | Windows |
|---|---|---|---|
| Developer/Origin | Microsoft, for IBM PC (1981) | Bell Laboratories, 1969, rewritten in C (1973) | Microsoft; Windows 1.0 (1985) |
| Interface | command line | command line (shell) + optional GUI | GUI |
| Users | Single-user | multi-user | Multi-user |
| Tasking | Single-tasking | Preemptive multi-tasking | Preemptive multitasking |
| Memory | 640 KB conventional limit, no virtual memory | virtual memory | Virtual memory |
| Security | No logins, no permissions | Owner/group/other permissions | Accounts, access control lists |
| Banking use | None in production | core banking servers | Branch PCs, many ATMs |

### (1) DOS
- **Internal commands:** DIR, CD, MD, COPY, DEL, TYPE, CLS, DATE, TIME, EXIT
- **External commands** (separate files on disk, loaded when called): FORMAT, DISKCOPY, XCOPY, ATTRIB, TREE

### (2) UNIX

```
        Applications and Utilities: commands, compilers, user programs
          ( Shell: command interpreter between the user and kernel
             ( Kernel: manages processes, memory, files and devices
                ( Hardware )))
```
*Fig: Layered structure of UNIX*

| Commands of DOS | Same/Alternative commands in UNIX |
|---|---|
| DIR | ls |
| CD | cd / pwd |
| MD / RD | mkdir / rmdir |
| COPY | cp |
| DEL | rm |
| TYPE | cat |
| CLS | clear |
| FIND | grep |
| ATTRIB | chmod |
| FORMAT | mkfs |

**Similarity:** all 3 provide a shell/command interface, file system, process control and device management.

**Conclusion:** DOS is one user on an unprotected machine, UNIX/Linux and Windows NT dominate today.

---

## 4.4 Identifying and Managing Security Threats in OS

### LQ.1 OS security threats, vulnerabilities and hardening strategy for a bank.

→ The OS controls every file, process and device, so whoever controls the OS, controls all applications and data above it. Securing a bank therefore begins with securing the OS of its servers, branch PCs and ATMs.

**Def**
→ A threat is a possible cause of harm. A vulnerability is a weakness that a threat can use. Hardening is reducing the vulnerabilities of a system.

| Threat | How it harms OS | Example / Common vulnerabilities |
|---|---|---|
| Malware | Malicious code (virus, worm, Trojan, ransomware, spyware, rootkit) runs with the user's rights | Ransomware encrypting a file server |
| Exploit of a software flaw | A bug such as a buffer overflow lets an attacker run code or crash the system | WannaCry (2017) used an SMBv1 flaw that had been patched two months earlier |
| Privilege escalation | An ordinary account gains administrator/root rights | Teller account becoming local administrator |
| Unauthorized access | Guessed, stolen or default passwords | Default administrator password left unchanged |
| Denial of service (DOS) | Processor, memory, disk or network exhausted | Flooding a server until users cannot login |
| Insider misuse | An authorised user abuses or exceeds given rights | Administrator altering logs |
| Backdoor (trap door) | Hidden entry point bypassing normal authentication | Undocumented maintenance account |

### OS hardening strategy

```
1. Install only   -->  2. Patch and   -->  3. Remove unused   -->  4. Strong authentication,
   what is needed        update OS           services; ports,        least privilege
                                             accounts                       |
                                                                            v
8. Backup, test,  <--  7. Logging and  <--  6. Anti-malware,    <--  5. Resource controls;
   audit, review         monitoring           host firewall,          permissions, encryption
        |                                     integrity checks
        +---------------------- repeat as a cycle ----------------------> (back to 1)
```

→ NRB IT guidelines require that a bank should provide highest level of security settings for OS and firewalls by;
- changes default passwords immediately after installation.
- applies patches as recommended by vendors.
- gives access on a need-to-know basis with least privilege.

### Types of Malware
1. **Virus** → Infected / Infects file
2. **Worm** → Self-contained, self-propagating (spreads over the network without user action)
3. **Trojan horse** → Disguised as useful software
4. **Ransomware** → Encrypts data for payment
5. **Rootkit** → Hides itself with system privileges
6. **Spyware** → Steals information secretly

**Conclusion**
→ Threat: What attacks
Vulnerability: the weakness used
