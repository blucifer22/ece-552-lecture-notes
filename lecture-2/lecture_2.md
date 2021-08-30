# ECE 552 Lecture 2: High-Speed Review of Undergrad Architecture

## Why is Hierarchy a Good Thing in Memory?

* *Temporal Locality:* Recently executed instructions are likely to be executed again soon
  * Loops!
  * Likewise for data
    * Data in loops
    * "Hot" global data
* *Spatial Locality:* Instructions near recently executed instructions are likely to be executed soon
  * Sequential execution
  * Data near recently referenced data likely needs to be referenced soon
    * Elements in an array, fields in a struct, variables in a stack frame
* ***LOCALITY IS ONE OF THE MOST IMPORTANT CONCEPTS IN COMPUTER ARCHITECTURE!!!***

## Memory System Performance Equations

* For some memory component `M`
  * Access: read or write to `M`
  * Hit: desired data found in `M`
  * Miss: desired data not found in `M`
    * Must get the data from another, slower, component
  * Fill: the act of placing data in `M`
  * %miss: #misses / #accesses
  * thit: time to read data from (or write data to) `M`
  * tmiss: time to read data into `M` from lower level
  * tavg: average access time
    * tavg = thit + (%miss * tmiss)

## Virtual Memory: How we make 4 == 8 == 64 == 2^64

* We essentially treat "real" memory as a big cache
  * Paginate, and then allow the hardware and OS to determine the map between virtual addresses and physical addresses.
* Address translation!
  * Virtual address gets split between a virtual page number (VPN) and a page offset (POFS)
  * Translate the VPN into a physical page number (PPN)
  * POFS is *NOT* translated however
* Above example?
  * 64 KB pages ==> 16-bit POFS
  * 32-bit machine ==> 32-bit VA ==> 16-bit VPN
  * Maximum 256 MB physical memory ==> 28-bit PA ==> 12-bit PPN

## I/O: The Very Scary Bit

* Just about everything has to go through I/O in some capacity
* Modern processors communicate with I/O using memory-mapped I/O
  * Some physical addressed "map" to I/O devices
    * Ex. address 8G + 12 could map to control register for disk
  * Communication with the device happens through a series of load/store operations
* Direct Memory Access (DMA)
  * Bulk I/O transfers (ex. page faults) save time
  * This is not without risk though, DMA allows *very* intimate understanding of the hardware and data so tread with care!

## So What's the Actual Objective of This Course?

***MAKE THE PROCESSOR GO BRRT!!!!***

**Readings:** H+P Chapter 1 (EZ reading)
**Paper:** Instruction Sets and Beyond: Computers, Complexity, and Controversy (Notification on Sakai when it's actually due!)

* Jokes aside, here are the actual objectives
  * Goals for new uarchs
  * More performance
  * Less power/energy
  * Lower cost (not really our problem)

* What does a CompArch do?
  * We design ISAs
    * Except not as much these days...
    * RISC-V is pretty much the most recent "big deal"
  * We design uarchs
    * This is where the money is in 2021

* Why do we need a new uArch?
  * Improvements in hardware technology!
    * Moore's Law! ==> transistor machine go brrt!
      * Except not as much anymore...
    * New technologies for switches and/or storage
      * Flash, phase change memory, memristors, etc.
      * Wafer-scale processors
      * Quantum ==> Not gonna go there
  * Improvements in compiler technology
    * Can co-design hardware and compiler to optimize performance
    * Ex.) Use new compiler techniques to create software that goes fast even on relatively simple uarch.

* Processors are built out of transistors
  * Moore's Law
    * Continued (until very recently) due to transistor miniaturization
    * Absolute improvements in density, speed, power, and cost
    * Processor density (~35% annual), speed ~15%
    * Memory density ~60%, speed ~4%
    * Big improvements in disk density and network bandwidth too
  * Moore's Curve
    * Moore's Law: Memory density improvement (2x / 18 months)
    * Moore's Curve: system performance improvement (2x / 18 months)
      * Self-fulfilling prophecy
    * "Technology nodes" are basically marketing material at this point
      * Franklin is crying a little bit rn
  
## Dennard Scaling

* As transistors kept getting smaller in each generation, they kept using less and less power
  * Moore: More transistors per chip
  * Dennard: Less power per transistor
  * Moore + Dennard = constant power per chip

* Annnnnnnnnnd then Dennard scaling ended
  * Option 1: Exploiting Moore's Law (can't do that anymore lol)
  * Option 2: Lower on-chip activity factor (only use what you need when you need it)
  * Option 3: Create more power-efficient uarchs (This is bleeding edge rn)

***THE TRUE RATE LIMITING FACTOR OF COMPUTER ARCHITECTURE IS POWER BUDGET!!!***
