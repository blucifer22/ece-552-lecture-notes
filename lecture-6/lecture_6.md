# ECE 552 Lecture 6: More Fun with Pipelining

## The Fine Art of Making ILP go BRRRRRT

* Remember that *programs* have dependencies and ILP, ***NOT*** the hardware
* *Hazards* are when we have a dependence and both instructions are in the pipeline together
  * Stalls are when we make younger instructions wait for older ones to complete.
  * Implementation? de-assert pipeline latch write-enable signals
  * This must be propagated down the pipeline, which creates bubbles (stages with no instructions in them)
  * Read-After-Write (RAW) dependencies are *true* dependencies, others can be removed with register renaming
    * Stall logic is outlined in the slides, *REVIEW THIS*
  * NOTE: Even with full bypassing, some stalls are unavoidable
    * Load-use
      * The load value isn't ready until the END of the M stage, and thus we cannot use the MX bypass
      * Thus, we have to use the WX bypass
      * With this bypass, we can stall in either D or X
  * Most multi-cycle functional units are also pipelined
    * Watch out for structural hazards (these can be somewhat circumvented with hardware replication, which is tenable because Si is cheap and plentiful)
  * Control hazards
    * We need to fetch past branch instructions before the outcome of a branch is known.
    * At a branch, we can't tell if it's a branch so we proceed sequentially
    * At execute, we may discover that younger instructions are wrong and we need to recover.
    * *Recovery* not bad, instructions F and D haven't written anything
      * *Flush* instructions in F and D (replace with nops)
* (Dynamic) branch prediction, affectionately known as "Let's guess and check!"
  * 