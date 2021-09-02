# ECE 552 Lecture 5: It's the End of the World as we Know it and I Feel Fine

## All Roads Lead to Multi-Core

* We prefer our chips in the unmelted state, therefore we need to do things to reduce power consumption
* What breaks chips?
  * Transient errors
    * Cosmic-ray/alpha-particle strikes and flips bit(s)
    * Breaks the currently running program, but eventually fixes itself
  * Wearout-induced permanent faults
    * Temperature and electrical effects cause things to break over time
    * This historically hasn't been much of an issue because hard drives were spinning disks
      * Becoming a bit more relevant buuuuuuuuuuuuut we can circumvent this with redundant transistors

## On Pipelining and Instruction Level Parallelism

* Simplified MIPS with a twist
  * ***OUTPUT WILL ALWAYS BE ON THE RIGHT!!!***
* All processors are architecturally von Neumann, *BUT* this is an abstraction
  * Under the hood, it doesn't need to be this and in fact, SHOUlD NOT for purposes of performance enhancement
* Typical programs do the following while maintaining the VN illusion
  * Pipelining
  * Out of order execution
* Instruction Level Parallelism (ILP)
  * *ILP IS UNRELATED TO HARDWARE, IT IS A PROPERTY OF THE PROGRAM!!!*
  * Whether or not we *achieve* this potential is a function of the hardware
    * See slides for a really compelling example!

## On Actual Pipelining

* The H&P 5-Stage Pipeline
  * The pedagogical pipeline, but by no means the only pipelining scheme
* Pipelining dramatically improves the throughput of any system
* Note that loads will ALWAYS use the integer add stage, even when you have an FPU because fractional memory addresses are bad for business