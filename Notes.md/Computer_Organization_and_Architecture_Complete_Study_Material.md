# GATE CSE — Computer Organization and Architecture

> **Syllabus:** Instruction set and addressing modes; ALU design; hardwired and microprogrammed control; memory interfacing and hierarchy (performance and cache mapping); I/O interface (interrupt and DMA); instruction pipelining and pipeline hazards.
>
> **Level:** Fundamentals to GATE CSE problem-solving. Architecture-specific details are identified where conventions vary.

## Table of Contents
1. [Foundations](#1-foundations)
2. [Instruction set architecture](#2-instruction-set-architecture)
3. [Addressing modes](#3-addressing-modes)
4. [ALU design](#4-alu-design)
5. [Control unit design](#5-control-unit-design)
6. [Memory interfacing and hierarchy](#6-memory-interfacing-and-hierarchy)
7. [Cache memory and mapping](#7-cache-memory-and-mapping)
8. [I/O interface, interrupts and DMA](#8-io-interface-interrupts-and-dma)
9. [Instruction pipelining](#9-instruction-pipelining)
10. [Pipeline hazards](#10-pipeline-hazards)
11. [GATE revision sheet](#11-gate-revision-sheet)
12. [Practice questions](#12-practice-questions)
13. [Detailed answer key](#13-detailed-answer-key)

---

# 1. Foundations

## 1.1 Computer architecture and computer organization

**Computer architecture** describes features visible to a programmer, such as the instruction set, programmer-visible registers, data types, instruction formats and addressing modes.

**Computer organization** describes how those features are implemented, such as the ALU, control signals, datapath, buses, cache and memory technology.

| Architecture | Organization |
|---|---|
| What the machine provides | How the machine is built |
| ISA, registers, addressing modes | ALU, control unit, datapath, buses |
| Affects program compatibility | Affects implementation and performance |

## 1.2 Main components

- **CPU:** executes instructions.
- **ALU:** performs arithmetic and logical operations.
- **Control unit:** generates signals that coordinate CPU operations.
- **Registers:** small, fast storage locations inside the CPU.
- **Main memory:** stores active programs and data.
- **I/O devices:** communicate with the external world.
- **System interconnect/bus:** carries address, data and control signals.

Important CPU registers:

| Register | Purpose |
|---|---|
| PC (Program Counter) | Address of the next instruction |
| IR (Instruction Register) | Holds the current instruction |
| MAR (Memory Address Register) | Holds the address for a memory access |
| MDR/MBR (Memory Data Register) | Holds data being read/written |
| SP (Stack Pointer) | Points to the stack top, as defined by the ISA |
| Status/flag register | Stores zero, carry, overflow and other flags |
| General-purpose registers | Hold operands and results |

## 1.3 Instruction execution cycle

A simplified instruction cycle:

1. **Fetch:** read instruction using PC.
2. **Decode:** identify opcode and operands.
3. **Operand fetch:** obtain operands from registers or memory.
4. **Execute:** perform ALU or other operation.
5. **Memory access:** read/write data memory if needed.
6. **Write-back:** store result.
7. **PC update:** select next instruction address.

Typical fetch micro-operations:
\[
MAR\leftarrow PC,\quad MDR\leftarrow M[MAR]
\]
\[
IR\leftarrow MDR,\quad PC\leftarrow PC+\text{instruction length}
\]

A branch or jump may replace the normal sequential PC update.

## 1.4 Buses and basic performance terms

- **Address bus:** identifies a memory or I/O location.
- **Data bus:** carries data.
- **Control bus:** carries read, write, interrupt and timing signals.

An address bus with `n` independent bits can identify `2^n` locations. If the system is byte-addressable, those locations represent `2^n` bytes.

Clock period and frequency:
\[
T=\frac{1}{f}
\]

CPU execution time:
\[
CPU\ Time=Instruction\ Count\times CPI\times Clock\ Cycle\ Time
\]
or
\[
CPU\ Time=\frac{IC\times CPI}{Clock\ Rate}
\]

For multiple instruction classes:
\[
CPI_{avg}=\sum_i\left(\frac{IC_i}{IC}\right)CPI_i
\]

---

# 2. Instruction set architecture

## 2.1 Instruction set and instruction format

An **instruction set** is the collection of machine-level operations a processor can execute. Examples include `ADD`, `SUB`, `LOAD`, `STORE`, `AND`, `JUMP` and `BRANCH`.

A typical conceptual instruction format:

```text
+----------+-------------+-------------+-------------+
| Opcode   | Destination | Source 1    | Source 2    |
+----------+-------------+-------------+-------------+
```

- **Opcode:** operation to perform.
- **Operand fields:** identify registers, constants or addresses.
- **Addressing-mode field:** may specify how to locate an operand.
- **Immediate/displacement field:** may contain a constant or address offset.

Formats vary. An instruction need not contain every field. If an opcode field has `k` bits, it can encode at most:
\[
2^k
\]
distinct opcode patterns.

## 2.2 Instruction classes

| Class | Purpose | Examples |
|---|---|---|
| Data transfer | Move data | LOAD, STORE, MOV |
| Arithmetic | Numeric operation | ADD, SUB, MUL |
| Logical | Bitwise operation | AND, OR, XOR, NOT |
| Shift/rotate | Move or rotate bits | SHL, SHR |
| Control transfer | Change instruction flow | JMP, BRANCH, CALL, RETURN |
| I/O | Communicate with device | IN, OUT in some ISAs |

## 2.3 Zero-, one-, two- and three-address instructions

The number of explicit address/operand fields gives rise to different instruction formats.

**Three-address**
```text
ADD R1, R2, R3
```
\[
R1\leftarrow R2+R3
\]
Two source operands and a separate destination.

**Two-address**
```text
ADD R1, R2
```
A common meaning is:
\[
R1\leftarrow R1+R2
\]
One operand is also the destination.

**One-address** — often uses an implied accumulator (AC):
```text
LOAD A
ADD B
STORE C
```
\[
AC\leftarrow M[A],\quad AC\leftarrow AC+M[B],\quad M[C]\leftarrow AC
\]

**Zero-address** — common in stack machines:
```text
PUSH A
PUSH B
ADD
```
`ADD` pops two operands, adds them and pushes the result.

| Format | Common implied resource |
|---|---|
| Three-address | None |
| Two-address | Destination is also a source |
| One-address | Accumulator |
| Zero-address | Stack |

Always use the instruction semantics stated in a question; conventions are not universal.

## 2.4 RISC and CISC

**RISC (Reduced Instruction Set Computer)** commonly uses relatively simple instructions, often fixed-length formats, many registers and a load/store organization in which arithmetic operates mainly on registers.

**CISC (Complex Instruction Set Computer)** commonly provides a richer instruction set, more addressing modes, possibly variable-length instructions and instructions that perform multiple lower-level operations.

| RISC tendency | CISC tendency |
|---|---|
| Simpler instruction operations | More complex instruction operations |
| Often fixed-length format | May use variable-length format |
| Commonly load/store | May allow memory operands in more operations |
| Often simpler decoding | Potentially more complex decoding |

These are broad tendencies, not strict rules. Modern processors combine ideas from both.

---

# 3. Addressing modes

## 3.1 Effective address

An **addressing mode** specifies how an instruction locates an operand. The **effective address (EA)** is the actual memory address used for the operand.

Do not confuse the effective address with the data stored at that address.

## 3.2 Common addressing modes

### Immediate
The operand value is part of the instruction.
```text
MOV R1, #25
```
\[
R1\leftarrow25
\]
No separate data-memory read is needed for the operand. The constant is limited by the immediate field width.

### Direct (absolute)
The instruction contains the memory address:
```text
LOAD R1, [1000]
```
\[
EA=1000,\quad R1\leftarrow M[1000]
\]

### Memory-indirect
The instruction's address field points to a memory location that contains the effective address:
\[
EA=M[A],\quad Operand=M[EA]
\]
This requires an extra memory access to obtain the effective address.

### Register
The operand is in a named register. For example, `ADD R1,R2` reads `R2` as a register operand.

### Register-indirect
A register contains the memory address:
\[
EA=R2,\quad Operand=M[R2]
\]
If `R2=500`, the operand is read from memory location 500.

### Indexed
A common form:
\[
EA=A+IX
\]
Useful for arrays. For elements larger than one byte, a scaled form may be used:
\[
EA=Base+Index\times ElementSize
\]

### Base/displacement
\[
EA=BaseRegister+Displacement
\]
Useful for fields within structures and locations relative to a base address.

### PC-relative
\[
EA=PC+Displacement
\]
Often used by branches. Architectures differ on whether PC refers to the current instruction or the next instruction.

### Auto-increment and auto-decrement
- Auto-increment: use the address in the register, then increment it.
- Auto-decrement: decrement the register, then use the updated address in a common convention.
The update order and amount depend on the ISA and operand size.

### Implied and stack
- **Implied:** operand is specified by the opcode, such as an accumulator or flag.
- **Stack:** operand is at the stack top and accessed through the stack pointer.

## 3.3 Comparison table

| Mode | Effective address / operand rule |
|---|---|
| Immediate | Operand is encoded in instruction |
| Direct | `EA=A` |
| Memory-indirect | `EA=M[A]` |
| Register | Operand is in named register |
| Register-indirect | `EA=R` |
| Indexed | `EA=A+IX` |
| Base/displacement | `EA=Base+Disp` |
| PC-relative | `EA=PC+Disp` |
| Auto-increment | Use `[R]`, then update R |
| Auto-decrement | Update R, then use `[R]` |
| Implied | Operand determined by opcode |
| Stack | Operand at stack top |

## 3.4 Solved effective-address example

Given:
- Address field `A=200`.
- `R1=500`.
- `M[200]=700`.
- `M[700]=42`.

Then:
- Direct: `EA=200`; operand = `M[200]=700`.
- Memory-indirect: `EA=M[200]=700`; operand = `M[700]=42`.
- Register-indirect through R1: `EA=500`; operand = `M[500]` (not specified).
- Immediate: use the constant encoded in the instruction; do not read `M[200]`.

---

# 4. ALU design

## 4.1 What is an ALU?

The Arithmetic Logic Unit performs arithmetic, logical and often shift operations.

Common operations:
- Addition, subtraction, increment and decrement.
- AND, OR, XOR and NOT.
- Comparisons.
- Logical and arithmetic shifts; rotates.

A simplified ALU contains operand inputs, arithmetic and logic circuits, operation-selection logic, a result output and status flags.

```text
 Operand A ----+----> Arithmetic unit ---+
               |                         |
 Operand B ----+----> Logic unit --------+--> Result MUX --> Result
                         ^                    ^
                         |                    |
                    ALU control --------------+
```

## 4.2 Adder equations

For bit `i` of a full-adder chain:
\[
S_i=A_i\oplus B_i\oplus C_i
\]
\[
C_{i+1}=A_iB_i+A_iC_i+B_iC_i
\]

A ripple-carry adder connects each stage's carry output to the next stage's carry input.

## 4.3 Subtraction using two's complement

\[
A-B=A+\overline B+1
\]

A common adder/subtractor uses a control bit `SUB`:
\[
B_i'=B_i\oplus SUB
\]
\[
Result=A+B'+SUB
\]

- `SUB=0`: B passes unchanged and carry-in is 0; perform addition.
- `SUB=1`: B is complemented and carry-in is 1; perform subtraction.

Example: 7 − 3 in 4 bits:
```text
 A       = 0111
 B       = 0011
 ~B + 1  = 1101
 ----------------
 0111 + 1101 = 1 0100
```
Discard the carry beyond 4 bits: `0100` = 4.

## 4.4 Logic operations

A bitwise logic unit may produce:
```text
A = 1010
B = 1100
A AND B = 1000
A OR  B = 1110
A XOR B = 0110
NOT A   = 0101   (4-bit width)
```

The width must be known for NOT/complement.

## 4.5 Shift operations

- **Logical left shift:** shift left; fill vacated low bits with 0.
- **Logical right shift:** shift right; fill vacated high bits with 0.
- **Arithmetic right shift:** shift right while replicating the sign bit in two's-complement representation.
- **Rotate:** shifted-out bits re-enter at the opposite end.

For unsigned values, a left shift by one often corresponds to multiplication by 2 if no significant bit is lost. A logical right shift often corresponds to integer division by 2. Signed arithmetic and overflow need care.

## 4.6 Status flags

| Flag | Meaning |
|---|---|
| Z (Zero) | Result is zero |
| N/S (Negative/Sign) | MSB of result is 1 in signed two's-complement interpretation |
| C (Carry) | Carry-out or borrow-related condition, as defined by ISA |
| V/OV (Overflow) | Signed arithmetic overflow |

For n-bit addition:
- Unsigned overflow is indicated by carry-out.
- Signed overflow occurs when same-sign operands produce a result with the opposite sign.

A common two's-complement addition formula:
\[
V=C_n\oplus C_{n-1}
\]
where `C_n` is carry out of the MSB and `C_(n-1)` is carry into the MSB.

Carry and overflow are different. Flag conventions for subtraction/borrow vary by architecture.

## 4.7 ALU control and design steps

A hypothetical ALU control table might be:

| Control | Operation |
|---|---|
| 000 | AND |
| 001 | OR |
| 010 | ADD |
| 110 | SUB |
| 111 | Compare |

Actual encodings are architecture-specific.

Design procedure:
1. List required operations.
2. Determine operand width.
3. Select/design arithmetic building blocks.
4. Design logic and shift functions.
5. Add result-selection multiplexers.
6. Define control encodings.
7. Define status flag behavior.
8. Test normal and boundary cases, including overflow.

---

# 5. Control unit design

## 5.1 Purpose and micro-operations

The control unit coordinates CPU operations. It determines which registers supply operands, which register receives a result, which ALU operation occurs, whether memory is read/written and how the PC changes.

A **micro-operation** is a small register-level operation, often performed in one clock step:
\[
MAR\leftarrow PC
\]
\[
MDR\leftarrow M[MAR]
\]
\[
IR\leftarrow MDR
\]
\[
R1\leftarrow R2+R3
\]

Control signals enable the relevant data transfers and functional units.

## 5.2 Hardwired control unit

A hardwired control unit generates control signals using fixed logic circuits such as decoders, gates, state registers and finite-state control logic.

```text
Instruction Register --> Decoder ----+
                                      |
Clock / timing state ----------------+--> Control logic --> Control signals
                                      |
Status / condition flags -------------+
```

**Advantages**
- Often fast because signals are generated directly by logic.
- Useful where high-speed control is important.

**Disadvantages**
- Changing instruction behavior may require hardware redesign.
- Rich instruction sets can make the logic complicated.
- Design and verification can be difficult.

## 5.3 Microprogrammed control unit

A microprogrammed control unit stores control information in **control memory**. A machine instruction is implemented as a sequence of **microinstructions**.

Main components:
- Control memory.
- Control Address Register (CAR) or microprogram counter.
- Microinstruction register.
- Microprogram sequencer.
- Next-address selection logic.

```text
Control Address Register
          |
          v
    Control Memory
          |
          v
 Microinstruction Register
          |
          v
    Control signals
          |
          v
       Datapath

Sequencer chooses the next microinstruction address.
```

A microinstruction may contain:
- Control field: selects micro-operations.
- Condition field: selects a condition to test.
- Next-address field: specifies or helps determine the next microinstruction.

The sequencer may select the sequential next address, a branch address, an opcode-mapped entry or a conditional path based on flags.

## 5.4 Horizontal and vertical microprogramming

**Horizontal**
- Wide microinstruction.
- Many control signals can be specified directly and in parallel.
- Less decoding may be needed.
- Control memory can be large.

**Vertical**
- Encoded, narrower microinstruction fields.
- Requires decoding to generate individual control signals.
- Often uses less control memory but adds decoding.

| Horizontal | Vertical |
|---|---|
| Wide control word | Narrower encoded word |
| More direct control | More decoding |
| More parallel control possibilities | More compact representation |
| Often larger control store | Often smaller control store |

## 5.5 Hardwired versus microprogrammed

| Feature | Hardwired | Microprogrammed |
|---|---|---|
| Signal generation | Fixed logic | Microinstructions in control memory |
| Speed | Often faster | May require microinstruction fetch/decode |
| Flexibility | Less flexible | Easier to modify microcode |
| Complexity | Logic can grow complex | Complex behavior represented as sequences |
| Control storage | No control store required | Requires control memory |

These are tendencies, not absolute rules. Modern designs may be hybrid.

---

# 6. Memory interfacing and hierarchy

## 6.1 Why hierarchy?

Fast memory is generally expensive per bit and limited in capacity. Large storage is cheaper per bit but slower. A hierarchy balances speed, capacity and cost.

```text
        Registers
           |
         L1 Cache
           |
         L2 Cache
           |
         L3 Cache
           |
      Main Memory (DRAM)
           |
     Secondary Storage
        (SSD / HDD)
```

Moving downward, capacity generally increases, cost per bit decreases and access latency increases.

## 6.2 Locality of reference

- **Temporal locality:** recently accessed data/instructions are likely to be accessed again soon (for example, a loop counter).
- **Spatial locality:** locations near a recently accessed location are likely to be accessed soon (for example, sequential array traversal).

Caches exploit these patterns.

## 6.3 Memory technologies

| Memory | Typical property | Common use |
|---|---|---|
| SRAM | Fast, no periodic refresh while powered, costly per bit | Cache |
| DRAM | Dense, requires periodic refresh | Main memory |
| ROM/nonvolatile memory | Retains contents without power | Firmware |
| Flash | Electrically erasable nonvolatile memory | SSD, USB storage |
| HDD | Magnetic, mechanical storage | Secondary storage |

SRAM and DRAM are volatile: they lose contents when power is removed.

## 6.4 Performance terms

- **Access time:** time from starting an access until data is available.
- **Memory cycle time:** minimum time between starting successive operations.
- **Bandwidth/transfer rate:** data transferred per unit time.
- **Latency:** delay before the first data becomes available.
- **Hit:** requested block is found in cache.
- **Miss:** requested block is not found in cache.

Bandwidth and latency are different.

## 6.5 Memory capacity and chip organization

A memory chip organized as `N × W` has N addressable words, each W bits wide:
\[
Capacity=N\times W\ bits
\]
If N is a power of 2:
\[
AddressLines=\log_2N
\]

Example: `4K × 8`:
- Words = 4096 = `2^12`.
- Width = 8 bits.
- Address lines = 12.
- Capacity = 32768 bits = 4096 bytes = 4 KiB.

## 6.6 Building larger memories

**Increase word width:** To build `4K × 16` from `4K × 8` chips, use two chips in parallel. Both receive the same address; each supplies 8 data bits.

**Increase number of words:** To build `16K × 8` from `4K × 8` chips, use four chips. The lower 12 address bits select a word within a chip; higher address bits and a decoder select the chip.

## 6.7 Memory interfacing and address decoding

Memory interfaces commonly use:
- Address lines.
- Data lines.
- Read enable.
- Write enable.
- Chip select.
- Output enable.

**Address decoding** determines which chip responds to an address range.

- **Full decoding:** all relevant high-order address bits are used to select a device, avoiding unintended aliases.
- **Partial decoding:** only some bits are decoded; multiple addresses may select the same physical device (address aliasing/mirroring).

The exact address map depends on the system design.

---

# 7. Cache memory and mapping

## 7.1 Cache basics

A cache stores copies of recently/frequently used memory blocks. The CPU checks the cache for a requested address:
- **Hit:** block is present.
- **Miss:** block is absent and must be fetched from a lower memory level.

A cache line stores a data block, tag, valid bit and possibly dirty/status bits.

## 7.2 Address fields

A common byte-addressed cache address is divided into:

```text
+----------------+-------------+--------------+
|      Tag       |    Index    | Block offset |
+----------------+-------------+--------------+
```

- **Offset:** selects a byte within a block.
- **Index:** selects a cache line or set.
- **Tag:** identifies which memory block is stored there.

For address width `m`, block size `B` bytes and number of sets `S` (powers of 2):
\[
OffsetBits=\log_2B
\]
\[
IndexBits=\log_2S
\]
\[
TagBits=m-IndexBits-OffsetBits
\]

## 7.3 Direct-mapped cache

Each memory block can go to exactly one cache line:
\[
CacheLine=BlockNumber\bmod L
\]
where L is the number of cache lines.

Address fields: tag, index and block offset.

Advantages: simple and fast lookup. Disadvantage: conflict misses when active blocks map to the same line.

## 7.4 Fully associative cache

A block can be placed in any cache line. There is no index field; the requested tag is compared against tags in all valid lines.

Advantages: flexible placement and fewer mapping conflicts. Disadvantages: more comparison hardware and a replacement policy is needed when full.

## 7.5 Set-associative cache

A cache with k ways per set:
\[
Sets=\frac{TotalLines}{k}
\]
A memory block maps to one set and can occupy any of its k ways:
\[
SetIndex=BlockNumber\bmod Sets
\]

Address fields: tag, set index and block offset.

| Feature | Direct mapped | Fully associative | k-way set associative |
|---|---|---|---|
| Possible location | One line | Any line | Any way in one set |
| Index | Yes | No | Set index |
| Tag comparison | One selected line | All lines | Ways in selected set |
| Hardware complexity | Low | High | Medium |

## 7.6 Solved address-field examples

**Example 1:** 32-bit byte addresses, 16 KiB direct-mapped cache, 64-byte blocks.

Lines:
\[
L=\frac{16\times1024}{64}=256=2^8
\]
Offset bits = `log2(64)=6`.
Index bits = `log2(256)=8`.
Tag bits = `32−8−6=18`.

**Example 2:** 32 KiB cache, 64-byte blocks, 4-way set associative, 32-bit addresses.

Lines:
\[
L=\frac{32768}{64}=512
\]
Sets:
\[
S=\frac{512}{4}=128=2^7
\]
Offset = 6 bits; index = 7 bits; tag = `32−7−6=19` bits.

## 7.7 Hit ratio and AMAT

\[
HitRatio=\frac{Hits}{TotalAccesses}
\]
\[
MissRate=1-HitRatio
\]

For one cache level:
\[
AMAT=HitTime+MissRate\times MissPenalty
\]

Example: hit time 2 ns, miss rate 0.05, miss penalty 50 ns:
\[
AMAT=2+0.05(50)=4.5\ ns
\]

For L1 and L2, where L2 miss rate is **local** (conditional on an L1 miss):
\[
AMAT=L1HitTime+L1MissRate(L2HitTime+L2MissRate\times L2MissPenalty)
\]

- **Local miss rate:** misses divided by accesses to that cache.
- **Global miss rate:** misses at that level divided by total CPU memory accesses.

Check the problem's definition of miss penalty; do not count lower-level access twice.

## 7.8 Write and replacement policies

**Write-through:** update cache and lower-level memory on every write. Simpler lower-level consistency, but more traffic.

**Write-back:** update cache only and mark line dirty; write to lower level when evicted. Less traffic, but requires dirty-bit tracking.

**Write-allocate:** on a write miss, bring the block into cache, then write.

**No-write-allocate/write-around:** on a write miss, write to lower level without allocating the block.

Write policy and allocation policy are separate decisions.

Replacement policies when a set is full:
- **LRU:** least recently used.
- **FIFO:** earliest inserted.
- **Random:** randomly selected.
- **Pseudo-LRU:** lower-cost approximation of LRU.

A direct-mapped cache has no replacement choice.

## 7.9 Cache miss categories

1. **Compulsory:** first access to a block.
2. **Capacity:** cache cannot hold the working set.
3. **Conflict:** blocks compete for the same set/line due to mapping restrictions.

---

# 8. I/O interface, interrupts and DMA

## 8.1 I/O interface

CPU and peripheral devices differ in speed, data format, transfer size and timing. An I/O interface/controller bridges this difference.

Common registers:
- **Data register:** holds transferred data.
- **Status register:** ready, busy, error or completion status.
- **Control register:** receives commands/configuration.

## 8.2 Memory-mapped and isolated I/O

**Memory-mapped I/O:** device registers occupy addresses in the memory address space; normal load/store instructions may access them.

**Isolated/port-mapped I/O:** I/O has a separate address space and often uses special I/O instructions.

| Memory-mapped | Isolated |
|---|---|
| Shares memory address space | Separate I/O address space |
| Often uses normal load/store | Often uses special I/O instructions |
| Uses part of memory address space | Separate port space |

## 8.3 Programmed I/O (polling)

1. CPU issues a device command.
2. CPU repeatedly reads status.
3. If device is not ready, CPU checks again.
4. When ready, CPU transfers data.
5. Repeat as required.

Simple, but CPU time is wasted while waiting and transferring.

## 8.4 Interrupt-driven I/O

The CPU starts I/O and continues other work. The device interrupts when it needs service or completes an operation.

Typical sequence:
1. CPU initiates I/O.
2. CPU executes other instructions.
3. Device raises interrupt request.
4. CPU recognizes it at an allowed instruction boundary.
5. Required context is saved.
6. Control transfers to the Interrupt Service Routine (ISR).
7. ISR services/acknowledges the device.
8. Context is restored and execution resumes.

Exact context saving and priority behavior depend on the architecture.

Important terms:
- **IRQ:** interrupt request.
- **ISR:** interrupt service routine.
- **Interrupt vector:** identifies/locates the ISR.
- **Maskable interrupt:** can be disabled/masked.
- **NMI:** non-maskable interrupt.
- **Priority:** determines service order.
- **Interrupt latency:** time from request to start of service.

Interrupt identification may use polling, vectored interrupts or daisy chaining.

## 8.5 DMA (Direct Memory Access)

DMA allows a controller to transfer a block directly between an I/O device and main memory with limited CPU involvement.

CPU typically:
1. Programs DMA address, transfer count and direction.
2. Starts the transfer.
3. Continues executing other instructions.
4. Handles completion/error notification.

DMA controller:
- Requests bus access.
- Transfers data.
- Updates address and count.
- Signals completion.

### DMA modes

- **Burst/block mode:** obtains the bus and transfers a block continuously; CPU may be unable to use the bus during the burst.
- **Cycle stealing:** takes individual bus cycles that could otherwise be used by CPU.
- **Transparent mode:** transfers when CPU is not using the bus, if supported.

## 8.6 Comparison of I/O methods

| Feature | Programmed I/O | Interrupt-driven I/O | DMA |
|---|---|---|---|
| Device checking | Repeated polling | Device notifies CPU | Controller manages transfer |
| Data movement | CPU | CPU/ISR | DMA controller |
| CPU overhead | High | Interrupt/service overhead | Setup/completion overhead |
| Suitable for | Simple/low-volume I/O | Event-driven/small transfers | Large block transfers |

**Important:** An interrupt is a notification mechanism; DMA is a transfer mechanism. DMA commonly uses an interrupt to notify the CPU when a transfer completes.

---

# 9. Instruction pipelining

## 9.1 Concept

Pipelining overlaps stages of multiple instructions. Like an assembly line, while one instruction is in a later stage, another can be in an earlier stage.

It improves **throughput** (instructions completed per unit time), not necessarily the latency of an individual instruction.

## 9.2 Classic five-stage pipeline

| Stage | Name | Operation |
|---|---|---|
| IF | Instruction Fetch | Fetch instruction |
| ID | Instruction Decode/Register Read | Decode and read registers |
| EX | Execute | ALU operation/address calculation |
| MEM | Memory Access | Read/write data memory |
| WB | Write Back | Write result to register |

Not every instruction uses every stage in the same way.

## 9.3 Pipeline cycles and speedup

For k stages and n instructions, with one instruction entering each cycle and no stalls:
\[
PipelineCycles=k+(n-1)
\]
Without pipelining, if each instruction takes k cycles:
\[
NonPipelineCycles=nk
\]
Ideal speedup:
\[
Speedup=\frac{nk}{k+n-1}
\]

Example: 5-stage pipeline, 5 instructions:
\[
Cycles=5+5-1=9
\]
Non-pipelined cycles = `5×5=25`.
Speedup = `25/9≈2.78`.

For a large instruction stream, ideal speedup approaches k, assuming balanced stages and no overhead/hazards.

## 9.4 Latency, throughput and stage time

- **Latency:** time for one instruction to pass through the pipeline.
- **Throughput:** rate at which completed instructions emerge.
- In an ideal k-stage pipeline, latency is about k cycles and steady-state throughput approaches one instruction per cycle.

If stage delays are `t1,...,tk` and pipeline-register overhead is `t_reg`:
\[
T_{clk}\ge\max(t_1,t_2,\ldots,t_k)+t_{reg}
\]
The slowest stage limits the clock period. Unequal stages reduce efficiency.

---

# 10. Pipeline hazards

## 10.1 Definition and types

A **pipeline hazard** prevents an instruction from executing in its intended cycle.

Three main types:
1. Structural hazard.
2. Data hazard.
3. Control hazard.

## 10.2 Structural hazard

Occurs when simultaneous stages need the same hardware resource and it cannot serve both.

Example: one unified single-ported memory is used for instruction fetch and data access. An IF access and a MEM access conflict.

Solutions:
- Separate instruction and data memories/caches.
- Multi-ported resources.
- Duplicate hardware.
- Stall one instruction.

## 10.3 Data hazards

A data hazard occurs when an instruction depends on a value that is not yet safely available.

**RAW (Read After Write):** later instruction reads a location before an earlier instruction writes its new value.
```text
I1: ADD R1, R2, R3
I2: SUB R4, R1, R5
```
`I2` needs the result produced by `I1`. This is a true data dependency.

**WAR (Write After Read):** a later instruction writes a location before an earlier instruction has read its old value. This is an anti-dependency and is mainly relevant when reads/writes may occur out of order.

**WAW (Write After Write):** a later instruction writes a location before an earlier instruction writes its result. This is an output dependency and can occur when writes complete out of order.

| Hazard | Meaning |
|---|---|
| RAW | Read after write — true dependency |
| WAR | Write after read — anti-dependency |
| WAW | Write after write — output dependency |

In a simple in-order five-stage pipeline with reads in ID and writes in WB in order, RAW is the common register data hazard; WAR and WAW are generally avoided by stage ordering.

## 10.4 Forwarding (bypassing)

Forwarding sends a result directly from a later pipeline stage to an earlier stage that needs it, rather than waiting for register write-back.

For the ADD/SUB sequence above, the ADD result can be forwarded to the SUB ALU input. Forwarding reduces many RAW stalls but does not solve every dependency.

## 10.5 Load-use hazard

```text
I1: LOAD R1, 0(R2)
I2: ADD  R3, R1, R4
```
In a classic five-stage pipeline, load data becomes available after MEM. The immediately following ADD may need to stall even with forwarding. With standard forwarding in the classic model, one bubble is commonly required; exact stalls depend on timing and bypass paths.

## 10.6 Stalling and bubbles

A **stall** delays an instruction until a resource or value becomes available. A **bubble** is an empty pipeline slot, often represented by a NOP.

Stalls reduce throughput.

## 10.7 Control hazards and branch prediction

A control hazard occurs when the next instruction address is unknown due to a branch or jump.

Solutions:
- Stall until branch resolution.
- Resolve branches earlier.
- Predict branch direction/target.
- Use delayed branching where defined by the ISA.
- Flush incorrectly fetched instructions after a misprediction.

**Static prediction** uses a fixed rule (for example, always taken). **Dynamic prediction** uses observed branch history.

A misprediction causes a penalty because incorrect speculative instructions must be discarded. They must not commit incorrect architectural results.

## 10.8 Hazard summary

| Hazard | Cause | Typical solution |
|---|---|---|
| Structural | Resource conflict | Duplicate/partition resource, multi-port, stall |
| RAW | Consumer needs unavailable result | Forwarding, stall |
| WAR | Later write overtakes earlier read | Preserve order, register renaming |
| WAW | Later write overtakes earlier write | Preserve order, register renaming |
| Control | Next PC depends on unresolved branch | Prediction, early resolution, stall, flush |

## 10.9 Pipeline examples

**Example 1:** 5-stage pipeline, 10 instructions, no stalls:
\[
Cycles=5+10-1=14
\]
Non-pipelined cycles = `5×10=50`; speedup = `50/14≈3.57`.

**Example 2:** 5-stage pipeline, 8 instructions, 3 extra stall cycles:
\[
IdealCycles=5+8-1=12
\]
\[
TotalCycles=12+3=15
\]

For a pipeline:
\[
CPI=\frac{TotalCycles}{InstructionCount}
\]
For a long ideal single-issue stream, ideal CPI approaches 1. A useful model is:
\[
CPI=CPI_{ideal}+AverageStallCyclesPerInstruction
\]

---

# 11. GATE revision sheet

## 11.1 High-value question patterns

1. Calculate CPU execution time from instruction count, CPI and clock rate.
2. Calculate effective addresses for different addressing modes.
3. Determine opcode capacity and instruction-field widths.
4. Trace ALU addition/subtraction and status flags.
5. Compare hardwired and microprogrammed control.
6. Calculate memory capacity and address lines.
7. Combine memory chips to obtain a required organization.
8. Calculate cache tag, index and offset widths.
9. Determine cache line/set for a memory block.
10. Calculate hit ratio, miss rate and AMAT.
11. Compare write-through/write-back and allocation policies.
12. Trace interrupt handling or DMA.
13. Calculate ideal pipeline cycles and speedup.
14. Identify RAW, WAR, WAW, structural and control hazards.
15. Count stalls under a specified forwarding/branch model.

## 11.2 Formula sheet

**CPU performance**
\[
CPU\ Time=IC\times CPI\times T_{clock}
\]
\[
CPU\ Time=\frac{IC\times CPI}{ClockRate}
\]

**Memory**
\[
NumberOfAddresses=2^{AddressBits}
\]
\[
Capacity=Words\times BitsPerWord
\]
\[
AddressLines=\log_2(Words)
\]

**Cache**
\[
Lines=\frac{CacheSize}{BlockSize}
\]
\[
Sets=\frac{Lines}{Ways}
\]
\[
OffsetBits=\log_2(BlockSize)
\]
\[
IndexBits=\log_2(Sets)
\]
\[
TagBits=AddressBits-IndexBits-OffsetBits
\]
\[
AMAT=HitTime+MissRate\times MissPenalty
\]

**Pipeline**
\[
PipelineCycles=k+n-1
\]
\[
NonPipelineCycles=nk
\]
\[
Speedup=\frac{nk}{k+n-1}
\]
\[
CPI=\frac{TotalCycles}{InstructionCount}
\]

## 11.3 Common GATE traps

- Effective address is not the operand stored at that address.
- Immediate addressing uses a value in the instruction, not a memory address.
- Memory-indirect addressing reads a pointer from memory.
- Address-bit count depends on the number of addressable units.
- Cache index bits use the number of sets, not the number of ways.
- Fully associative caches have no set-index field.
- A k-way cache has `total lines / k` sets.
- Check whether miss penalty includes lower-level access time.
- Local and global miss rates are different.
- Write policy and write-allocation policy are separate.
- DMA transfers data; an interrupt notifies the CPU.
- Pipelining improves throughput, not necessarily individual latency.
- `k+n−1` assumes ideal stages, no stalls and one instruction entering per cycle.
- RAW is a true dependency; WAR/WAW are name dependencies.
- Forwarding cannot eliminate every load-use stall.
- Branch penalty depends on branch-resolution stage and prediction policy.

## 11.4 Quick revision checklist

- [ ] Explain architecture versus organization.
- [ ] Trace fetch, decode, execute and write-back.
- [ ] Calculate effective addresses in listed addressing modes.
- [ ] Explain RISC and CISC.
- [ ] Derive ALU add/subtract behavior and flags.
- [ ] Compare hardwired and microprogrammed control.
- [ ] Calculate memory capacity and chip organization.
- [ ] Explain locality and memory hierarchy.
- [ ] Calculate cache fields and AMAT.
- [ ] Explain polling, interrupts and DMA.
- [ ] Calculate pipeline cycles, CPI and speedup.
- [ ] Identify hazards and decide whether forwarding/stalls are needed.

---

# 12. Practice questions

**Attempt these before checking the answer key.** Use the definitions and pipeline assumptions stated in each question.

## A. Conceptual questions

**Q1.** Distinguish computer architecture from computer organization.

**Q2.** What is the difference between an effective address and an operand?

**Q3.** Explain immediate, direct and memory-indirect addressing.

**Q4.** Why can one adder perform both addition and subtraction?

**Q5.** What is the main difference between hardwired and microprogrammed control?

**Q6.** Why does a computer use a memory hierarchy?

**Q7.** Explain temporal and spatial locality.

**Q8.** What is the difference between an interrupt and DMA?

**Q9.** Does pipelining reduce the latency of an individual instruction?

**Q10.** Distinguish RAW, WAR and WAW hazards.

## B. MCQs

**Q11.** An instruction with 6 opcode bits can represent at most:
A. 6  B. 12  C. 32  D. 64

**Q12.** In PC-relative addressing, the effective address is commonly:
A. `M[PC]`  B. `PC + displacement`  C. `PC × displacement`  D. `displacement − PC`

**Q13.** Which control unit stores control information as microinstructions?
A. Hardwired  B. Microprogrammed  C. Arithmetic  D. Cache-based

**Q14.** Which memory is commonly used for CPU caches?
A. DRAM  B. SRAM  C. HDD  D. Optical disk

**Q15.** A fully associative cache has:
A. One cache line  B. No tag  C. No index/set field  D. No block offset

**Q16.** Which technique transfers a block between an I/O device and main memory with limited CPU involvement?
A. Polling  B. DMA  C. Busy waiting  D. Decoding

**Q17.** An instruction needs a value that a previous instruction has not produced. Which hazard?
A. Structural  B. RAW  C. WAR  D. Control

**Q18.** An ideal 6-stage pipeline executes 20 instructions. Cycles required?
A. 20  B. 25  C. 26  D. 120

## C. MSQs

**Q19.** Select true addressing-mode statements:
A. Immediate operand is in the instruction.
B. Register-indirect uses a register as a memory pointer.
C. Direct addressing obtains EA by reading a pointer from memory.
D. PC-relative uses a displacement relative to PC.

**Q20.** Select true cache-mapping statements:
A. A direct-mapped block has one possible line.
B. A fully associative block can be placed in any line.
C. A 4-way cache has four sets.
D. A set-associative block maps to one set and can occupy any way in it.

**Q21.** Select true I/O statements:
A. Polling repeatedly checks device status.
B. Interrupts can allow CPU work while a device operates.
C. DMA requires CPU to transfer every data word.
D. DMA completion can be reported using an interrupt.

**Q22.** Select true pipelining statements:
A. Pipelining overlaps instruction stages.
B. Ideal single-issue throughput can approach one instruction per cycle.
C. Pipelining guarantees lower latency for every instruction.
D. Branches can cause control hazards.

## D. Numerical Answer Type

**Q23.** A CPU executes 2 million instructions, average CPI 2.5, clock rate 1 GHz. Find execution time in milliseconds.

**Q24.** A memory has 8K words, each 16 bits. Find capacity in bytes.

**Q25.** An 8 KiB direct-mapped cache has 32-byte blocks. Find its number of lines.

**Q26.** A byte-addressed system has 24-bit addresses. A direct-mapped cache has 4 KiB capacity and 16-byte blocks. Find tag bits.

**Q27.** Hit time = 1 ns, miss rate = 0.04, miss penalty = 40 ns. Find AMAT.

**Q28.** A 5-stage pipeline executes 12 instructions without stalls. Find cycles.

**Q29.** A modulo-64 counter requires how many flip-flops at minimum?

## E. Application problems

**Q30.** A register contains 1200. An instruction uses register-indirect addressing through it. If `M[1200]=75`, find EA and operand.

**Q31.** Use 8-bit two's-complement arithmetic to calculate `12−5`. Show the bit operations.

**Q32.** A 4-way set-associative cache has 256 total lines. Find number of sets.

**Q33.** A two-level cache has L1 hit time 1 ns, L1 miss rate 0.10, L2 hit time 5 ns, L2 local miss rate 0.20 and L2 miss penalty 50 ns. Find AMAT.

**Q34.** In a classic five-stage pipeline:
```text
I1: ADD R1, R2, R3
I2: SUB R4, R1, R5
```
Identify the dependency/hazard and a technique that can reduce stalls.

**Q35.** A 4-stage ideal pipeline executes 100 instructions. Compare pipelined and non-pipelined cycles and find ideal speedup.

**Q36.** A device must transfer a large block to main memory. Which is generally most suitable: programmed I/O, interrupt-driven I/O or DMA? Explain.

---

# 13. Detailed answer key

## A. Conceptual answers

**A1.** Architecture describes programmer-visible features such as ISA, registers and addressing modes. Organization describes implementation details such as datapath, ALU, control logic, buses and memory technology.

**A2.** Effective address is the memory location calculated by the addressing mode. Operand is the data stored there. In register addressing, the operand is directly in a register.

**A3.**
- Immediate: value is part of the instruction.
- Direct: instruction contains the memory address.
- Memory-indirect: instruction points to a memory location containing the effective address.

**A4.**
\[
A-B=A+\overline B+1
\]
The adder can perform subtraction by complementing B conditionally and setting carry-in to 1.

**A5.** Hardwired control generates signals using fixed logic. Microprogrammed control reads microinstructions from control memory.

**A6.** Fast memory is expensive and limited; large memory is slower and cheaper per bit. A hierarchy balances speed, capacity and cost.

**A7.** Temporal locality means recently used locations are likely to be reused. Spatial locality means nearby locations are likely to be accessed soon.

**A8.** An interrupt notifies the CPU that an event needs attention. DMA transfers data between device and memory without requiring the CPU to move every word.

**A9.** Not necessarily. Pipelining overlaps instructions and improves throughput. Individual latency may remain roughly the sum of stage delays.

**A10.**
- RAW: later read before earlier write.
- WAR: later write before earlier read.
- WAW: later write before earlier write.

## B. MCQ answers

**A11. D — 64.** `2^6=64`.

**A12. B — `PC + displacement`.** The exact PC reference point depends on the architecture.

**A13. B — Microprogrammed.** Control words are stored in control memory.

**A14. B — SRAM.** SRAM is commonly used for cache; DRAM for main memory.

**A15. C — No index/set field.** A fully associative cache can place a block in any line.

**A16. B — DMA.** The DMA controller handles block transfer.

**A17. B — RAW.** The consumer reads a value before the producer has made it available.

**A18. B — 25.**
\[
Cycles=k+n-1=6+20-1=25
\]

## C. MSQ answers

**A19. A, B and D.** Direct addressing uses the address in the instruction; it does not first fetch a pointer from memory.

**A20. A, B and D.** Four-way means four lines per set, not four sets.

**A21. A, B and D.** DMA moves data; CPU does not transfer every word. Completion can be reported by interrupt.

**A22. A, B and D.** Pipelining overlaps stages; ideal throughput approaches one instruction per cycle; branches can create control hazards. Lower individual latency is not guaranteed.

## D. NAT solutions

**A23.**
\[
Time=\frac{2\times10^6\times2.5}{10^9}=0.005s=\boxed{5ms}
\]

**A24.**
\[
8K=8192\ words
\]
\[
Capacity=8192\times16=131072\ bits
\]
\[
Bytes=131072/8=\boxed{16384\ bytes}=16KiB
\]

**A25.**
\[
Lines=\frac{8\times1024}{32}=\boxed{256}
\]

**A26.**
- Lines = `4096/16=256`.
- Offset bits = `log2(16)=4`.
- Index bits = `log2(256)=8`.
- Tag bits = `24−4−8=\boxed{12}`.

**A27.**
\[
AMAT=1+0.04(40)=\boxed{2.6ns}
\]

**A28.**
\[
Cycles=5+12-1=\boxed{16}
\]

**A29.**
\[
n=\log_2 64=\boxed{6}
\]

## E. Worked solutions

**A30.** Register-indirect uses the register contents as EA. Thus `EA=1200`; operand=`M[1200]=75`.

**A31.**
```text
  12       = 00001100
   5       = 00000101
  ~5       = 11111010
  -5       = 11111011
             00001100
           + 11111011
           ----------
           1 00000111
```
Discard the carry beyond 8 bits. `00000111=7`. Answer: **7**.

**A32.**
\[
Sets=\frac{256}{4}=\boxed{64}
\]

**A33.** L2 miss rate is local:
\[
AMAT=1+0.10(5+0.20\times50)
\]
\[
=1+0.10(15)=\boxed{2.5ns}
\]

**A34.** `I1` writes R1 and `I2` reads R1: a RAW hazard. Forwarding/bypassing can send the result directly to the consumer, reducing or eliminating the stall depending on when the result is available.

**A35.**
\[
PipelinedCycles=4+100-1=\boxed{103}
\]
\[
NonPipelinedCycles=100\times4=\boxed{400}
\]
\[
Speedup=400/103\approx\boxed{3.883}
\]

**A36.** DMA is generally best for a large block because the DMA controller transfers data directly between the device and main memory. The CPU configures the transfer and handles completion instead of moving every word. An interrupt may notify the CPU when DMA completes.

---

## Final self-assessment

You are ready for mixed GATE-level COA questions when you can:

1. Trace instruction execution and calculate effective addresses.
2. Solve ALU addition/subtraction and interpret flags.
3. Compare hardwired and microprogrammed control.
4. Solve memory-chip organization and address-decoding problems.
5. Calculate cache tag/index/offset fields and AMAT.
6. Explain programmed I/O, interrupts and DMA.
7. Calculate pipeline cycles, CPI and speedup.
8. Identify hazards and decide when forwarding or stalls are required.

**Suggested study order:** Instruction Set → Addressing Modes → ALU → Control Unit → Memory Hierarchy → Cache → I/O → Pipelining and Hazards. Practise numerical questions after each topic.
