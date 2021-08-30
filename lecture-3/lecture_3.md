# ECE 552 Lecture 3: Objectives and Pipelining

## Do We Really Need a Faster Computer?

* For some purposes, no
  * PowerPoint, Instagram, anything your parents do...
* For other purposes?
  * Simulating long-running biological processes at molecular level
  * Gaming and simulations
  * Running DukeHub...
  * Applications we haven't even thought of yet
    * Build it, and they will come!

## That's Cute, How Do We Measure Speed?

* Two definitions
  * Latency (execution time): Time to finish one fixed task
  * Throughput (bandwidth): Number of tasks finished in a fixed time
  * *VERY* different: Throughput can exploit parallelism, latency cannot
    * It's basically a Subway sandwich assembly line
    * Low throughput can result in higher latency
  * These are often contradictory goals
  * Choose the definition that matches goals; most often this is throughput
    * Bus has a higher throughput than a car, even if a car is faster
    * Graphics processors are *throughput* engines, but have high latency
      * The name of the game in GPU dev is VOLUME
* SPEC (Standard Performance Evaluation Corporation) Benchmarks
  * [Linked here](http://www.spec.org)
  * Many specialized suites for specific tasks
  * SPEC Core 2017 is the going standard for most tasks...it's also $1000.00
* Mean Performance Numbers
  * Arithmetic mean
    * This is the one we all know from when we were kids
    * For units that proportional to time (e.g. latency)
    * ***THIS DOES NOT APPLY TO RATES OR RATIOS!!!!***
  * Harmonic Mean
    * For rates (e.g. throughput)
  * Geometric Mean
    * For unit-less quantities like ratios (e.g. speedups)
* CPU Performance Equation
  * `runtime = instructions/program * cycles/instruction * seconds/cycle`
  * cycles/instruction (uarch, compiler, program) are the focus of this class
* Metric Called MIPS (NOT THE ISA!!!!)
  * This is a bad metric
  * I can do a bajillion waiting instructions/second...doesn't mean I'm "waiting" better
  * Gigahertz falls victim to the same marketing bullshit
* Cycles per Instruction (CPI)
  * CPI: cycle/instruction for average instruction
    * IPC: (1/CPI) more intuitive, but harder to compute with
  * CPI example
    * A program that executes equal integer, FP, and memory operations
* Measuring CPI
  * We use SIMULATORS (SimpleScalar for HWs for us)
    * Measure exactly what you want, and the impact of potential fixes!
    * Method of choice for many micro-architects (and you!)

## Performance: Technology Basis and Trends

* Technology basis of performance
  * Performance proportional to (clock frequency * IPC)
    * Clock frequency: transistor delay, wire delay, pipelining

* Issue 1: How Many Pipeline Stages?
  * Trend had been to increase the number of pipeline stages
    * Chop data into finer pieces
    * Often causes CPI to increase...to a point
      * At some point, this actually causes a performance hit
    * "Optimal" pipeline depth is program and technology specific

  * PentiumIII: 12 stage pipeline, 800 MHz (faster than Pentium4)
  * Pentium4: 22 stage pipeline, 1 GHz
  * Intel Core: 14 stage pipeline (Intel learned its lesson...)
* Issue 2: CPI and Clock Frequency
  * System components are "clocked" independently
    * Increasing the processor "clock" doesn't accelerate memory, etc.
  * See slides for example
* ***AMDAHL'S LAW***
  * Overall speedup of optimization = 1 / ((1 - F) + (F/S)), where F is fraction optimized and S is the speedup on the optimized part
  * Overall speedup is limited by non-accelerated piece
  * Another way of thinking about this is ***MAKE THE COMMON CASE FAST***
    * Focus your energies on things that matter
  * ***NEVER FORGET AMDAHL'S LAW***
