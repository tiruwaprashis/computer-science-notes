# 2. Computer Architecture

## 2.1 Basic Computer Architecture, Registers, Memory Management

### ① Memory Hierarchy

**Def** → It is the arrangement of memory types in levels so the fastest, smallest, costliest memory is nearest the CPU and the slowest, largest, cheapest is farthest. It gives the illusion of a large, fast memory.

**Diagram** →

```text
 ▲ Faster / Costlier / Smallest
 │
 │        ┌──────────────────────────┐
 │        │        Registers         │ ┐ Internal
 │        ├──────────────────────────┤ ┘ Storage
 │        │     Cache (L1/L2/L3)     │
 │        ├──────────────────────────┤ ┐ Primary
 │        │    Main Memory (RAM)     │ ┘ Storage
 │        ├──────────────────────────┤
 │        │ Secondary Storage (SSD/HDD)│
 │        ├──────────────────────────┤
 │        │ Tertiary / Offline       │
 │        │ (Tape, Optical, Cloud)   │
 ▼        └──────────────────────────┘
 Slower / Cheaper / Largest
```

**Levels Table**

| Level | Technology | Speed | Size | Managed by |
| :--- | :--- | :--- | :--- | :--- |
| Registers | Flip-flops in CPU | <1 ns | Bytes–KB | Compiler / Programmer |
| Cache (L1, L2, L3) | SRAM | 1–20 ns | KB–MB | Hardware |
| Main Memory | DRAM | 50–100 ns | GB | OS |
| Secondary | HDD / SSD | 0.1–10 ms | 100s GB–TB | OS |
| Tertiary | Tape, Optical, Cloud | Seconds+ | TB–PB | OS / Operator |

### Types of Memory Device

```text
                          Memory
              ┌─────────────┴──────────────┐
        Primary Memory               Secondary Memory
     ┌────────┼─────────┐             ┌──────┴───────┐
    RAM      ROM     Cache         Optical Disc   Magnetic Disk
     │        │      Memory           │               │
   ├ SRAM   ├ PROM                  ├ CD           ├ Hard Disk Drive (HDD)
   └ DRAM   ├ EPROM                 └ DVD          ├ Solid State Drive (SSD)
            └ EEPROM                               └ USB Drive
```

### Locality of Reference (why the hierarchy works)

→ Programs access a small set of addresses repeatedly.

- **Temporal:** recently accessed location likely accessed again soon. [Ex:- loop counter, loop body; variable `sum` in a loop]
- **Spatial:** nearby locations likely accessed next. [Ex:- array `a[0]`, `a[1]`, `a[2]` → so a whole block is loaded into cache.]
- **Sequential:** instructions execute in order (PC increments).

**OR for memory management version**

→ OS + MMU function that tracks memory, allocates / reclaims it.

**Tasks:** allocation / deallocation, protection, relocation (logical + physical address via MMU), sharing, virtual memory.

### Conclusion

→ Hierarchy balances speed, size and cost; locality lets a small cache satisfy most CPU requests.

---

### ② Von Neumann Architecture / Stored Program Concept

**Def** → Proposed by John von Neumann (1945, EDVAC report). Central idea is both instructions and data are stored in the same read-write memory in binary, and the CPU fetches and executes instructions one by one.

**Diagram** →

```text
             ┌───────────────────────────┐
 ┌───────┐   │            CPU            │   ┌────────┐
 │ Input │ → │  (Control Unit + ALU +    │ → │ Output │
 └───────┘   │  Registers (PC, IR, MAR,  │   │  Unit  │
             │        MDR, ACC))         │   └────────┘
             └─────────────┬─────────────┘
                  ↕ ↕ ↕ (data bus, address bus, control bus)
     ┌───────────────────────────────────────────────┐
     │ Main Memory (instructions + data share the    │
     │ same memory)                                  │
     └───────────────────────────────────────────────┘
```

**Note:** Single bus

| Unit | Function |
| :--- | :--- |
| Input Unit | Accepts data/programs, converts to binary |
| Memory Unit | Stores instructions and data in addressable locations |
| Control Unit | Fetches, decodes, generates control signals |
| ALU | Arithmetic (+ − × ÷) and logic (AND, OR, NOT, compare) |
| Registers | Fast temporary storage inside CPU |
| Output Unit | Presents results (monitor, printer) |

**Von Neumann vs Harvard**

| Basis | Von Neumann | Harvard |
| :--- | :--- | :--- |
| Memory | Single for instructions + data | Separate |
| Buses | One set | Separate |
| Access | Cannot fetch both at once | Simultaneous |
| Cost / Used in | Cheaper; PCs | Costlier, faster; DSP, microcontrollers |

**Harvard Architecture**

```text
                          Unified Memory
         ← Data Bus ──────┐ ┌──────────────────────┐
  ┌─────← Address Bus ────┼─┤   Program Memory     │
  │ CPU ← Control Bus ────┘ │   (Instructions)     │
  │                         └──────────────────────┘
  │     ← Data Bus ───────┐ ┌──────────────────────┐
  │     ← Address Bus ────┼─┤     Data Memory      │
  └─────← Control Bus ────┘ └──────────────────────┘
```

---

### ③ CPU Registers (PC, IR, MAR, MDR/MBR, ACC, GPR)

**Def** → Small, extremely fast storage locations inside the CPU holding instructions, addresses, data and results during execution; top of the memory hierarchy (1 clock cycle access).

| Register | Function |
| :--- | :--- |
| PC (Program Counter) | address of next instruction |
| IR (Instruction Register) | holds current instruction |
| MAR (Memory Address Register) | address of memory location to read/write; connected to address bus |
| MDR/MBR (Memory Data/Buffer Register) | data being read/written to memory; connected to data bus |
| ACC (Accumulator) | holds one operand and ALU result |
| GPR (General Purpose Registers) | R0–Rn, AX, BX, CX, DX; programmer-usable for data, address, counters |

**Other registers:** SP (Stack Pointer), Status/Flag register.

| Basis | General Purpose Register (GPR) | Special (SPR) |
| :--- | :--- | :--- |
| Purpose | Multiple uses (data, address, counter) | Fixed dedicated function |
| Access | Directly usable by programmer | Often restricted |
| Controlled by | Programmer / compiler | CPU hardware / Control Unit / OS |
| Examples | R0–R15, AX, BX ... | PC, IR, MAR ... |

---

## 2.2 Organization of Hard Disk

### ① Physical and Logical Organization of Hard Disk and Disk Access Time

**Def** → HDD is a non-volatile secondary storage device storing data magnetically on rotating circular platters, giving large capacity at low cost with random (direct access).

**Diagram**

```text
(a) One surface, top view               (b) Platter stack, side view

        ╭───────────╮                      ┌──────── Platter ────────┐
      ╱ ╲  sector  ╱ ╲                     ═════════╪═════════
     │   ╲  ▓▓▓  ╱   │ ← Track             ═════════╪═════════  ← Spindle
     │ ●──────────────│ ← Spindle           ═════════╪═════════
      ╲  ╱       ╲  ╱                      Cylinder: the same track on
        ╰───────────╯                                 every surface
   Actuator arm → read/write head
```

**Disk capacity** = surfaces × tracks/surface × sectors/track × bytes/sector

**Example:** 4 platters (8 surfaces), 10,000 tracks, 500 sectors, 512 bytes then

Disk capacity = 8 × 10000 × 500 × 512 = 20,480,000,000 B ≈ 20.48 GB

**Disk access time** = Seek time + Rotational latency + Transfer time

| Component | Meaning | Formula / value |
| :--- | :--- | :--- |
| Seek time | Move head to required track/cylinder | 3–10 ms average |
| Rotational latency | Wait for sector to rotate under head | Average = ½ rotation = 60/(2 × RPM); 4.17 ms at 7200 RPM |
| Transfer time | Read/write the data | Data size / transfer rate |

**Numerical**

→ Suppose, Seek = 9 ms, 7200 RPM, rate = 100 MB/s, read = 4 KB

- then, Rotation = 60/7200 = 8.33 ms
- avg latency = 4.17 ms
- Now, Transfer = 4 KB / 100 MB/s = 0.04 ms

**Formula:** Access time = 9 + 4.17 + 0.04 ≈ 13.2 ms

**Conclusion**

→ Access time is dominated by mechanical seek and rotational delays, so performance depends on RPM, seek time and scheduling.

---

## 2.3 CPU Architecture

### ① Instruction Cycle (Fetch-Decode-Execute) with RTL (Register Transfer Language)

**Def** → It is the sequence of steps the CPU repeats for every instruction until HALT (means stops).

**Diagram** →

```text
 [Start] → ┌─────────────────┐   ┌────────┐   ┌─────────┐
           │ FETCH           │ → │ DECODE │ → │ EXECUTE │
           │ Instruction from│   └────────┘   └────┬────┘
           │ memory into IR  │                     ↓
           └────────▲────────┘          ┌──────────────────┐
                    │                   │ Interrupt check  │
                    │                   │ if pending       │
                    │                   └───┬──────────┬───┘
                    │                    no │          │ yes
                    └───────────────────────┘          ↓
                    loop back until HALT       ┌──────────────────┐
                    ◄──────────────────────────│ Service it:      │
                                               │ save PC, run ISR │
                                               └──────────────────┘
```

| Phase | Action | RTL |
| :--- | :--- | :--- |
| Fetch | PC → MAR; memory read; instruction into IR; PC incremented | T0: MAR ← PC <br> T1: MDR ← M[MAR], PC ← PC+1 <br> T2: IR ← MDR |
| Decode | Control Unit decodes opcode, finds operand address | T3: Decode IR (opcode) <br> T4: MAR ← IR (address) <br> T5: MDR ← M[MAR] |
| Execute | ALU performs operation | T6: ACC ← ACC + MDR (ADD) <br> or PC ← IR (address) (JUMP) |
| Store | Result to register/memory, flags updated | T7: M[MAR] ← MDR (STORE) <br> or Rd ← result |
| Interrupt check | If pending, save PC, run ISR | — |

**Example**

Q. Add 500 at address 100 where ACC = 5, M[500] = 7

Given, MAR = 100, MDR = 7

- **Fetch:**
  - T0: MAR(100) ← PC
  - T1: M[100], 101 ← 100+1 [i.e. PC = 101]
  - T2: IR ← ADD 500
- **Decode:**
  - T4: MAR = 500 ← IR
- **Execute:**
  - T6: ACC ← ACC + MDR (ADD)
  - ACC ← 5 + 7
  - ACC = 12
- **Store:** flags update; next fetch at 101.

---

### ② Types of Computer Architecture

| Basis | 1. Complex Instruction Set Computer (CISC) | 2. Reduced Instruction Set Computer (RISC) |
| :--- | :--- | :--- |
| Instruction set | Large, complex | Small, simple |
| Instruction length | Variable | Fixed |
| Execution | Multiple cycles | Mostly one cycle |
| Control Unit | Microprogrammed | Hardwired |
| Registers | Few | Many |
| Memory access | Any instruction | Only LOAD/STORE |
| Pipelining | Difficult | Easy |
| Code size | Small | Large |
| Examples | x86, VAX | ARM, MIPS, SPARC, RISC-V |

**Diagram**

```text
        CISC Architecture                          RISC Architecture

           Main Memory                    Instruction Memory        Data Memory
               ↕                                  ↓                      ↕
  Microprogram Control Unit                Hardwired Control Unit   Large Register File
  (Control Memory / Microcode)                    ↓                      ↕
        ↓            ↕                    Simple Fixed-length    →  ALU (Pipelined)
  Complex Instruction ↔ ALU + Few                Decoder
        Decoder          Registers

  [Memory-to-memory operations allowed]     [Only LOAD/STORE access memory]
```

*Fig: Block Diagram of CISC & RISC*

**Example:** suppose (a = a × b)

| CISC | RISC |
| :--- | :--- |
| `MULT 2:3, 5:2` <br> (one instruction) | `LOAD A, 2:3` <br> `LOAD B, 5:2` <br> `PROD A, B` <br> `STORE 2:3, A` <br> (four instructions) |

**Conclusion:** CISC cuts program size, RISC gains speed through simplicity and pipelining; modern CPUs mix both.

---

## 2.4 I/O Management, I/O Interface, I/O Request Handling, I/O Devices

### ① Direct Memory Access (DMA)

→ A DMA controller (DMAC) transfers blocks of data directly between an I/O device and main memory without continuous CPU involvement; CPU only starts the transfer and is interrupted at the end.

**Block Diagram** →

```text
   ┌────────────────────── Address Bus ──────────────────────┐
   ├────────────────────── Data Bus ─────────────────────────┤
   │            │                                │           │
 ┌─┴───┐   ┌────┴──────────────────┐ read/write ┌┴─────────┐
 │     │ ← │ DMAC                  │ ─────────► │   Main   │
 │ CPU │   │ ┌───────────────────┐ │            │  Memory  │
 │     │   │ │ Address register  │ │            └──────────┘
 │     │   │ │ Word-count reg.   │ │
 │     │   │ │ Control register  │ │
 │     │   │ │ (Request/Grant)   │ │
 └─────┘   │ │ Status register   │ │
           │ └───────────────────┘ │
           └───▲───────────────┬───┘
      DMA request           DMA acknowledge
               │               ▼
           ┌───┴───────────────────┐
           │ I/O device (eg disk)  │
           └───────────────────────┘

 CPU ↔ DMAC:  Bus request (HOLD) · Bus grant (HLDA) · Interrupt at end
 Data moves, device ↔ memory over the data bus, not through the CPU
```

| Component | Function / Working |
| :--- | :--- |
| Address Register | Starting memory address; incremented after each word |
| Word count register | No. of words; decremented; zero = transfer complete |
| Control register | Mode and direction (read/write, burst/cycle-stealing) |
| Status register | Busy, done, error, request pending |
| Control logic | Sends bus request (HOLD), receives grant (HLDA), generates read/write signals, DREQ/DACK handshake |
| Interrupt line (INTR) | Tells CPU transfer is complete |

| Basis | Programmed I/O | Interrupt-driven I/O | DMA |
| :--- | :--- | :--- | :--- |
| CPU involvement | Full; busy-wait (polling) | Free until interrupt | Only start and end |
| Data path | Device → CPU reg → memory | Device → CPU reg → memory | Device → memory directly |
| Speed | Slowest | Moderate | Fastest |
| Hardware cost | Simple, cheap | Needs interrupt controller | Needs DMA controller |
| Data unit / use | One word; simple slow device | One word per interrupt; keyboard, mouse | Block; disk, network, graphics |
