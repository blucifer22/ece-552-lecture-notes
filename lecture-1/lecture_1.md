# ECE 552 Lecture 1: Syllabus

* We will discuss topics that are legitimately controversial in the field at this time, and as such, discussion is expected!
  * There are no solutions, only tradeoffs

## So What's the Objective of This Course?

* Making things faster with *instruction-level parallelism*
  * Pipelined cores
  * Superscalar (wide pipeline) cores
  * Static (compiler) core scheduling
  * Other fun things!

## Without Further Ado, All of ECE 250 in ***ONE*** Slide Deck

* What do ISAs have in common?
  * Sequential (von Neumann) execution model
  * Basic datatypes and operations
  * Virtual address size

* Features that differentiate ISAs?
  * Operand model
  * Number of registers
  * Addressing modes
  * Fun stuff!
    * Special instructions, etc.

* RISC vs. CISC
  * Key metric is *runtime*
    * `runtime = insn/program * cycles/insn * clock period`
  * RISC is near-invariably faster than CISC, so why does anyone use CISC?
    * Legacy applications, where writing in assembly was essentially a pre-requisite
      * "Powerful" instructions are more appealing than "good" instructions
    * The *golden handcuffs* of x86
    * People didn't *build* CISC, CISC was *converged* upon

* Caches
  * What we politely refer to in the industry as "muy *fucking* importante"
  * No cache? No computer
  * Temporal locality
    * If I used it recently, I probably will use it again soon
  * Spatial locality
    * Insns near what I just executed are highly likely to be executed shortly
    
