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


As for the Datapath shell, I made a Component out of the ALU shell and instantiated it. From there I used the rest of the PRISM schematic, as shown below:


![](https://github.com/dustyweisner/ECE281_Lab4/blob/master/PRISM_Schematic.GIF?raw=true)


I started by looking at all of the Registers and their connections. I then used each Input, Load, Clear, and Clk to define the Output of each register. For example, if IRLd is '1', the IR is Data, and still taking into account the Reset, making IR "0000" when Reset_L is '0'. Also, if MARLo was on then MARHi was off, because together they make an 8-bit for the Program Counter Register. The other registers were created similarly, except the Data, which is set to 
Accumulator when EnAccBuffer is on, else set it to high impedence. Also implementing datpath signals was different. 


To test and debug the Datapath, I initially used the waveform given to match the produced waveform given below, which matched perfecly again.


![](https://github.com/dustyweisner/ECE281_Lab4/blob/master/DatapathSim.GIF?raw=true)


But then to test and debug more in depth, I reverse engineered it, which will be discussed under the "REVERSE ENGINEERING" section.


The Operation of the Testbench works in the place of the Controller. It gives the loads values and loads in specific instructions, so that the hardware can be tested for each specific intruction.


__*REVERSE ENGINEERING*__


To reverse engineer, I first analyzed how the waveform was produced, using the waveform below (split into two parts):


![](https://github.com/dustyweisner/ECE281_Lab4/blob/master/SIMpart1.GIF?raw=true)

![](https://github.com/dustyweisner/ECE281_Lab4/blob/master/SIMpart2.GIF?raw=true)


Since the first 50 ns was analyzed for me, I began around 50 ns, and ended at around 100 ns. At 55 ns, the instruction was ROR because the IR was '3', and also because at the end of the prior instruction (LDAI), at 45 ns the DATA said '3' prompting the next instruction. The DATA ('4') then marks the next instruction. Notice the impedence part of the ROR instruction. The DATA ('4') then marks the next instruction again, which is OUT. The DATA next says '3' which stores the accumulator value into Output port 3, at around 105 ns. The rest of the program was analyzed and chunked into PRISM instructions as shown below:


![](https://github.com/dustyweisner/ECE281_Lab4/blob/master/PRISM_Reverse.GIF?raw=true)


The program continues to jump using the JN instruction until the accumulator is not negative. When the jumps end, it continues through an infinite loop as to not crash using the JMP instruction. 

