ECE281_Lab4
===========

ALU and Datapath Sim

__*DEMOS*__


Both the ALU and Datapath Simulations were checked off by Dr. Neebel.


__*DESIGN*__


To modify the ALU shell, I observed the PRISM's schematic as shown below:


![](https://github.com/dustyweisner/ECE281_Lab4/blob/master/PRISM_ALU.GIF?raw=true)


The OpSel was given to the multiplexer to find the instruction (0-7) that would be used to carry out a specific function defined in the ALU. For instance when Opsel is 0, the AND function occurs by setting the resulting bits to "Accumulator AND Data." The NEG was simply the Twos Compliment (negation) of the Accumulator (according to the input connections to the NEG function shown in the schematic above). IN and LD were concluded to be the same, just the Data bus's information. The same was carried out for the other functions; according to the wires' connections to each specific instruction, the ALU was modified. The following waveform is of the ALU Testbench:


![](https://github.com/dustyweisner/ECE281_Lab4/blob/master/ALUSim.GIF?raw=true)


To test and debug the ALU Testbench, I looked at the specific bits that are required for the input of each instruction and the results that occured and compared them to what they should have been. For example, if OpSel is "000," then I performed the AND instruction, ANDing Data ("0001") and the Accumulator ("0000") resulting in "0000". if OpSel is "001," then I performed the NEG instruction, taking the Two's Compliment of the Accumulator ("0100") resulting in "1100". I went through the entire waveform, and concluded that all of my instructions worked perfectly using those techniques.


As for the Datapath shell,



![](https://github.com/dustyweisner/ECE281_Lab4/blob/master/DatapathSim.GIF?raw=true)


__*REVERSE ENGINEERING*__

