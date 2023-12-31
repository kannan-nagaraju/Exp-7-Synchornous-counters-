## NAME: PRASHANTH.K
## REGISTER NUMBER:212223230152

# Exp-6-Synchornous-counters - up counter and down counter 
### AIM: 
## To implement 4 bit up and down counters and validate  functionality.
### HARDWARE REQUIRED: 
##  PC, Cyclone II , USB flasher
### SOFTWARE REQUIRED:   
## Quartus prime

### THEORY 

## UP COUNTER 
The counter is a digital sequential circuit and here it is a 4 bit counter, which simply means it can count from 0 to 15 and vice versa based upon the direction of counting (up/down). 

The counter (“count“) value will be evaluated at every positive (rising) edge of the clock (“clk“) cycle.
The Counter will be set to Zero when “reset” input is at logic high.
The counter will be loaded with “data” input when the “load” signal is at logic high. Otherwise, it will count up or down.
The counter will count up when the “up_down” signal is logic high, otherwise count down

Since we know that binary count sequences follow a pattern of octave (factor of 2) frequency division, and that J-K flip-flop multivibrators set up for the “toggle” mode are capable of performing this type of frequency division, we can envision a circuit made up of several J-K flip-flops, cascaded to produce four bits of output.
The main problem facing us is to determine how to connect these flip-flops together so that they toggle at the right times to produce the proper binary sequence.
Examine the following binary count sequence, paying attention to patterns preceding the “toggling” of a bit between 0 and 1:
Binary count sequence, paying attention to patterns preceding the “toggling” of a bit between 0 and 1.

Note that each bit in this four-bit sequence toggles when the bit before it (the bit having a lesser significance, or place-weight), toggles in a particular direction: from 1 to 0.



 
 

Starting with four J-K flip-flops connected in such a way to always be in the “toggle” mode, we need to determine how to connect the clock inputs in such a way so that each succeeding bit toggles when the bit before it transitions from 1 to 0.

The Q outputs of each flip-flop will serve as the respective binary bits of the final, four-bit count:

 
 

Four-bit “Up” Counter
![image](https://user-images.githubusercontent.com/36288975/169644758-b2f4339d-9532-40c5-af40-8f4f8c942e2c.png)



## DOWN COUNTER 

As well as counting “up” from zero and increasing or incrementing to some preset value, it is sometimes necessary to count “down” from a predetermined value to zero allowing us to produce an output that activates when the zero count or some other pre-set value is reached.

This type of counter is normally referred to as a Down Counter, (CTD). In a binary or BCD down counter, the count decreases by one for each external clock pulse from some preset value. Special dual purpose IC’s such as the TTL 74LS193 or CMOS CD4510 are 4-bit binary Up or Down counters which have an additional input pin to select either the up or down count mode.
![image](https://user-images.githubusercontent.com/36288975/169644844-1a14e123-7228-4ed8-81a9-eb937dff4ac8.png)


4-bit Count Down Counter
### Procedure
1.Create a New Project: Open Quartus and create a new project by selecting "File" > "New Project Wizard." Follow the wizard's instructions to set up your project, including specifying the project name, location, and target device (FPGA).
2.Create a New Design File:

Once the project is created, right-click on the project name in the Project Navigator and select "Add New File." Choose "Verilog HDL File" or "VHDL File," depending on your chosen hardware description language. ⦁ Write the Combinational Logic Code:

Open the newly created Verilog or VHDL file and write the code for your combinational logic. 3.Compile the Project: To compile the project, click on "Processing" > "Start Compilation" in the menu. Quartus will analyze your code, synthesize it into a netlist, and perform optimizations based on your target FPGA device. 4.Analyze and Fix Errors:

If there are any errors or warnings during the compilation process, Quartus will display them in the Messages window. Review and fix any issues in your code if necessary. View the RTL diagram. 5.Verification: Click on "File" > "New" > "Verification/Debugging Files" > "University Program VWF". Once Waveform is created Right Click on the Input/Output Panel > " Insert Node or Bus" > Click on Node Finder > Click On "List" > Select All.

Give the Input Combinations according to the Truth Table and then simulate the Output Waveform.



### PROGRAM 
## UP COUNTER
```
module sc(clk,A);
input clk;
output reg[0:3]A;
always@(posedge clk)
begin
A[0]=((((A[1])&(A[2]))&A[3])^A[0]);
A[1]=(((A[2])&(A[3]))^A[1]);
A[2]=((A[3])^A[2]);
A[3]=1^A[3];
end
endmodule
```
## DOWN COUNTER
```
module downcounter(
  input wire clk,   
  input wire rst,   
  output reg [3:0] count   
);

  always @(posedge clk or posedge rst) begin
    if (rst) begin
      
      count <= 4'b1111;
    end else begin
     
      count <= count - 1;
    end
  end

endmodule
```

### RTL LOGIC UP COUNTER AND DOWN COUNTER  
## UP COUNTER
![image](https://github.com/kannan-nagaraju/Exp-7-Synchornous-counters-/assets/145742755/ad926dd9-b304-4d01-b74c-a37f6b33a321)

## DOWN COUNTER
![image](https://github.com/kannan-nagaraju/Exp-7-Synchornous-counters-/assets/145742755/d0e385e2-2914-439c-9357-bb4ba3518f49)


### TIMING DIGRAMS FOR COUNTER  
## UP COUNTER
![image](https://github.com/kannan-nagaraju/Exp-7-Synchornous-counters-/assets/145742755/bea5c413-ebec-4690-98a6-5500142b83c2)

## DOWN COUNTER
![image](https://github.com/kannan-nagaraju/Exp-7-Synchornous-counters-/assets/145742755/1a5fecbe-5e09-4a1f-941a-c448354111c6)

### TRUTH TABLE 
## UP COUNTER
![image](https://github.com/kannan-nagaraju/Exp-7-Synchornous-counters-/assets/145742755/98c69352-3431-4652-9634-290c73d0e0da)

## DOWN COUNTER
![image](https://github.com/kannan-nagaraju/Exp-7-Synchornous-counters-/assets/145742755/9c3103fa-28c0-4832-a8fc-3d4c601d2ece)

### RESULTS
By this we have verified the truth table of 4-bit up-counter and down counter using verilog.
