# RISC-V-1C

This Project in 2 words is a project to build a [RISC-V](https://en.wikipedia.org/wiki/RISC-V) processor, a modern and up-to-date processor. Run the simulation on [digital simulation](https://en.wikipedia.org/wiki/Logic_simulation) software. Run several instruction tests and small programs on the simulator. Then transplant it to hardware using a reconfigurable [FPGA](https://en.wikipedia.org/wiki/Field-programmable_gate_array) board.

The simulator in question is called [Digital](https://github.com/hneemann/Digital). It allowed us to do the implementation, to test all the instructions implemented, even to test small programs. But most importantly, it enabled us to generate [Verilog](https://en.wikipedia.org/wiki/Verilog) code, which will then be the medium for transplanting to the FPGA. Normally, hardware implementation is done directly using the Verilog language. But for my part, I preferred visual programming, which makes debugging and testing easier for me. The image below is a snapshot of the entire processor (most of which is the [DataPath](https://en.wikipedia.org/wiki/Datapath)), created using Digital simulator.


