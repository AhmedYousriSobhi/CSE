# CPU Scheduling

# Mystic Map
- [CPU Scheduling](#cpu-scheduling)
- [Mystic Map](#mystic-map)
- [Dynamic Scheduling in CPU Pipelines](#dynamic-scheduling-in-cpu-pipelines)
  - [Key Concepts](#key-concepts)
  - [Understanding the Problem](#understanding-the-problem)
  - [Instructions' Path through the Pipeline](#instructions-path-through-the-pipeline)
  - [Part: Scheduling Instructions](#part-scheduling-instructions)
  - [Part: Multiple Addition Units](#part-multiple-addition-units)

# Dynamic Scheduling in CPU Pipelines
Our focus here is on how instructions are issued, executed, and completed in a processor. This involves concepts from computer architecture and pipelining, which are crucial for understanding how modern CPUs efficiently execute multiple instructions.

## Key Concepts
- Pipelining:
    - A technique used in CPUs to execute multiple instructions simultaneously by dividing the execution process into different stages.
    - Think of it as an assembly line in a factory, where each stage of the line performs a part of the task.

- Single-Issue Pipeline:
    - A pipeline that can issue only one instruction per clock cycle.

- Dynamic Scheduling:
    - A technique where the CPU decides the order of instruction execution at runtime, allowing instructions to be executed out of order if there are no dependencies blocking them.
    - This is done to improve the utilization of CPU resources and to avoid stalls (delays).

- Functional Units:
    - Different units in the CPU that perform specific operations like addition, multiplication, etc.
    - For example, an addition unit performs addition operations, and a multiplication unit performs multiplication operations.

- Reservation Stations:
    - Buffers that hold instructions waiting to be executed by a functional unit.
    - Each reservation station can store operands and track when an instruction can be executed.

- Common Data Bus (CDB):
    - A bus that carries the results of executed instructions back to the reservation stations and registers.


## Understanding the Problem
In the problem, you are given a set of instructions and asked to determine how they move through the pipeline. The instructions use functional units that take different cycles to complete their operations. Here’s the detailed breakdown:
Instructions
```
    mul $6, $0, $2: Multiply values in registers $0 and $2, and store the result in $6.
    add $8, $4, $6: Add values in registers $4 and $6, and store the result in $8.
    add $9, $0, $2: Add values in registers $0 and $2, and store the result in $9.
    add $7, $4, $9: Add values in registers $4 and $9, and store the result in $7.
```

## Instructions' Path through the Pipeline
The instructions pass through several stages:
1. Issue: The instruction is placed in a reservation station.
2. Dispatch: The instruction is sent to the functional unit for execution when operands are available.
3. Commit: The instruction's result is written back to the register file, and the instruction is considered complete.

## Part: Scheduling Instructions
You are asked to complete a table showing when each instruction is issued, dispatched, and committed.

## Part: Multiple Addition Units
The question then asks how the scheduling would change if there were two addition units instead of one, considering a single CDB (Common Data Bus) and then two CDBs.
- If the processor has two addition units, it can handle two additions in parallel.
- With a Single Common Data Bus (CDB): Even with two addition units, only one result can be written back per cycle.
- With Two CDBs: If there are two CDBs, results can be written back simultaneously.

Notes 
- Issue Cycle -> Focus on the availability of the room.
- Dispatch Cycle -> Focus on register availability and Functional unit availability.
- Commit Cycle -> Focus on CDB.
