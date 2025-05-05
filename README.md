# RISC-V-1C

This Project in 2 words is a project to build a [RISC-V](https://en.wikipedia.org/wiki/RISC-V) processor, a modern and up-to-date processor. Run the simulation on [digital simulation](https://en.wikipedia.org/wiki/Logic_simulation) software. Run several instruction tests and small programs on the simulator. Then transplant it to hardware using a reconfigurable [FPGA](https://en.wikipedia.org/wiki/Field-programmable_gate_array) board.

The simulator in question is called [Digital](https://github.com/hneemann/Digital). It allowed us to do the implementation, to test all the instructions implemented, even to test small programs. But most importantly, it enabled us to generate [Verilog](https://en.wikipedia.org/wiki/Verilog) code, which will then be the medium for transplanting to the FPGA. Normally, hardware implementation is done directly using the Verilog language. But for my part, I preferred visual programming, which makes debugging and testing easier for me. The image below is a snapshot of the entire processor (most of which is the [DataPath](https://en.wikipedia.org/wiki/Datapath)), created using Digital simulator.

![image](rv32i.png)

## Implementation

Looking at the image at above of the processor, it's easy to see that 90% of the figure represents the processor's DataPath, the rest is the [Control Unit](https://en.wikipedia.org/wiki/Control_unit). The color coding of the processor components is fairly self-explanatory. Light blue is for mass storage, such as [RAM](https://en.wikipedia.org/wiki/Random-access_memory) and [ROM](https://en.wikipedia.org/wiki/Read-only_memory). Dark blue is for the Control Unit. Yellow is for the register, or small memory. Red is for combinatorial circuits, such as the [Arithmetic-Logic Unit](https://en.wikipedia.org/wiki/Arithmetic_logic_unit) or Adders. White is for Multiplexers. Small triangles represent connections that are not drawn, used to avoid cluttering the schematic. The following is a list of processor components:

1.  Control Unit (CU): This is the unit responsible for decoding the instruction, and triggering control signals to control the other DataPath components.
2.  Program Counter (PC): The register containing the address of the instruction currently being executed.
3.  ROM: A read-only memory containing the list of instructions to be executed (the program).
4.  Regiter File (RF): A register bank containing all the programmable registers (32 x 32-bit registers) of the processor.
5.  RAM: The main memory where program data is stored. Accessed by the 2 instructions Store and Load.
6.  Arithmetic and Logic Unit (ALU): This is the unit responsible for all possible arithmetic and logic operations of the processor.
7.  Adders (+): Combinatorial circuits that perform addition, used by the DataPath for address calculation.
8.  Sign expanders (in trapezoid form): Combinatorial circuits for converting integers signed on a reduced number of bits (12 bits, for example) to 32-bit representations.
9.  Shifter (in parallelogram form): Combinatorial circuit for shifting bits.
10.  Multiplexers (in the form of an isosceles trapezoid): Via control signals from the Control Unit, they control the flow of data trough the DataPath.


