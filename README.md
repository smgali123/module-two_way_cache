# 2-Way Set-Associative Cache with LRU Policy

## Overview
This repository contains the RTL (Register-Transfer Level) design and testbench verification of a parameterized 2-way set-associative cache memory written in Verilog HDL. The core objective of this project is to implement an efficient Least Recently Used (LRU) replacement algorithm for dynamic data allocation and to evaluate the cache hit/miss decision logic during memory access operations.

## Features
* **Parameterized Architecture:** The number of sets can be easily adjusted using the `SETS` parameter (Default is 4).
* **LRU Replacement Policy:** Implements a hardware-based Least Recently Used algorithm to efficiently manage data replacement when cache sets are full.
* **Synchronous Operations:** Fully synchronous read and write operations controlled by clock and reset signals.
* **Hit/Miss Evaluation Logic:** Accurately determines cache hits and misses based on index and tag comparisons.
* **Functional Verification:** Includes a comprehensive testbench (`tb_cache`) to simulate and validate various read, write, and invalid address memory access scenarios.

## RTL Architecture Details
The cache module receives a 32-bit address, which is internally split into:
* **Index:** `[3:2]` (Used to select the set)
* **Tag:** `[31:4]` (Used to check for a hit within the set)

It maintains two distinct blocks (Way 0 and Way 1) per set, keeping track of data, tags, valid bits, and a dedicated LRU bit for replacement decisions.

## How to Simulate
1. Clone this repository to your local machine.
2. Open your preferred HDL simulation tool (e.g., ModelSim, Vivado, EDA Playground, or Icarus Verilog).
3. Compile both the design file (`two_way_cache.v`) and the testbench file (`tb_cache.v`).
4. Run the simulation. The testbench will output the Read/Write operations, Hit/Miss status, and retrieved data in the console.

## Testbench Output Example
The testbench validates the logic by executing the following sequence:
1. Write data `0xAAAAAAAA` to address `0x10`.
2. Read from address `0x10` (Expected: Hit = 1, Data = `0xAAAAAAAA`).
3. Write data `0xBBBBBBBB` to address `0x20`.
4. Read from address `0x20` (Expected: Hit = 1, Data = `0xBBBBBBBB`).
5. Read from an uninitialized address `0x40` (Expected: Hit = 0).
