# RISC-V-1C

This Project in 2 words is a project to build a [RISC-V](https://en.wikipedia.org/wiki/RISC-V) processor, a modern and up-to-date processor. Run the simulation on [digital simulation](https://en.wikipedia.org/wiki/Logic_simulation) software. Run several instruction tests and small programs on the simulator. Then transplant it to hardware using a reconfigurable [FPGA](https://en.wikipedia.org/wiki/Field-programmable_gate_array) board.

The simulator in question is called [Digital](https://github.com/hneemann/Digital). It allowed us to do the implementation, to test all the instructions implemented, even to test small programs. But most importantly, it enabled us to generate [Verilog](https://en.wikipedia.org/wiki/Verilog) code, which will then be the medium for transplanting to the FPGA. Normally, hardware implementation is done directly using the Verilog language. But for my part, I preferred visual programming, which makes debugging and testing easier for me. The image below is a snapshot of the entire processor (most of which is the [DataPath](https://en.wikipedia.org/wiki/Datapath)), created using Digital simulator.

![image](images/rv32i.png)

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

## Instruction Set Architecture

The [Instruction Set](https://en.wikipedia.org/wiki/Instruction_set_architecture) chosen to be implemented on this processor is the RV32I, with the exception of the 3 instructions ecall, ebreak, and fence, which are not so essential for normal program execution. You can see all the instructions in the diagram below, these are the green instructions, excluding the 3 already mentioned. RISC-V is designed to be flexible enough to include several instruction sets. In our case, we've chosen to implement only the basics. That is, the basic instructions for 32-bit format.

![image](images/RV32IMAC-ISA.jpg)

## Verilog generated code

Digital has the ability to automatically generate Verilog or [VHDL](https://en.wikipedia.org/wiki/VHDL) code; in our case, we generated the Verilog code. However, to make the code compatible with the FPGA, some modifications had to be made. The most important of these was a change in the implementation of RAM memory to force the use of the built-in memory blocks, since by default the code didn't use the FPGA's built-in memory blocks called [BRAMs](https://nandland.com/lesson-15-what-is-a-block-ram-bram/); instead RAM was implemented using elementary logic cells. This led to the use of a very high number of logic cells, making the FPGA insufficient to hold the processor. All the Verilog code is contained in [cpu.v](cpu.v).

## FPGA Cyclone IV implementation

An Intel Altera Cyclone IV FPGA was used to implement the processor on hardware. The exact reference of the FPGA is [EP4CE1](https://www.waveshare.com/coreep4ce10.htm), with a frequency of 50 MHz, 164 pins, 10k logic elements, and 50 KB of dedicated memory. To get a glimpse of processor execution on the very fast FPGA, the code has been modified to change the clock frequency from 50 MHz to 1 Hertz. And the first 4 bits of the ALU output are displayed on the 4 LEDs directly integrated into the FPGA. The demonstration video below shows the execution.

[![image](images/fpga-video.jpg)](https://youtu.be/b0H4Q8MfbC4)

The Verilog code was compiled on [Intel Quartus](https://en.wikipedia.org/wiki/Quartus_Prime) Prime Lite edition [EDA](https://en.wikipedia.org/wiki/Electronic_design_automation), and the summary of the compilation result is shown in the following image:

![image](images/Quartus_risc-v_summary.jpg)

Being inexperienced with FPGAs, I'd like to point out that Google's AI [Gemini 2.5](https://aistudio.google.com), helped me a lot in the FPGA implementation process. I even uploaded the verilog code of the processor design to it, and it managed to find a bug that I didn't detect with the few unit tests I ran.








