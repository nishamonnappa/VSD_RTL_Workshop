
A brief learning summary on 5-day workshop on Verilog coding guidelines, synthesis of RTL code to netlist, GLS, and simulation mismatches (RTL v/s Netlist) at VSD with SKY130 Technology, from 23-27 June 2021.

Open-Source Tools Used in the session: -
1. Verilog: Simulator. Used for RTL Simulation and Gate Level Simulations
2. Yosys: Opensource Logic Synthesis Tool
3. Skywater 130nm Standard Cell Libraries


An Overview:

	
An Overview:

	Session -1
	  Introduction to open-source simulator iverilog
	  Labs using iverilog and gtkwave
	  Introduction to Yosys and Logic synthesis
	  Labs using Yosys and Sky130 PDKs

	Session -2
	  Introduction to timing. libs
	  Hierarchical vs Flat Synthesis
	  Various Flop Coding Styles and optimization

	Session -3
	  Introduction to optimizations
	  Combinational logic optimizations
	  Sequential logic optimizations
	  Sequential optimizations for unused outputs

	Session -4
	  GLS, Synthesis-Simulation mismatch and Blocking/Non-blocking statements
	  Labs on GLS and Synthesis-Simulation Mismatch
	  Labs on synth-sim mismatch for blocking statement

	Session -5
	  If Case constructs
	  Labs on "Incomplete If Case"
	  Labs on "Incomplete overlapping Case"
	  for loop and for generate
	  Labs on "for loop" and "for generate"






Session -1

The session on first day was an introduction to the tool used and about the inputs and outputs of the RTL design flow.

	- Input to iverilog- RTL design and the stimulus generator, i.e., the testbench (TB)
	- Ouput of iverilog- VCD file (value change dump) format.
	- The stimulus observer used here in GTKWave, which was demonstrated 


Session -2
A Glimpse of “sky_fd_sc_hd_tt_025C_1v80.lib” file was given and technical specifications of the same. Below is a snippet of a sky130_fd_sc_hd_tt_025C_1v80.lib file used for the Lab activity in the session. It refers to all the standard cells to be used in the design and how they connect accordingly during synthesis and simulation. It contains all the slow and fast cells.
 
 ![image](https://user-images.githubusercontent.com/86371082/123688344-81779780-d86f-11eb-9bc7-6d6ef6a145e6.png)


![image](https://user-images.githubusercontent.com/86371082/123688604-d9160300-d86f-11eb-8c79-61dff3db202c.png)


![image](https://user-images.githubusercontent.com/86371082/123688675-efbc5a00-d86f-11eb-94c2-69b77db233b0.png)

 
 
Details: -  sky130_fd_sc_hd_tt_025C_1v80.lib

	Sky130- It’s a 130nm library
	tt- Typical Process
	025C- Temperature
	1v80- indicates the Temperature
	**Basically, the standard cell library is designed around all the minimum, typical and maximum corner of 
    PVT corner for manufacturing the IC.
	
Other Details: - The library file contains below:-

	1. Delay_model:”Look Up”
  2. Some of the units of the time, voltage, power, current, and resistance are mentioned as below: 
 
  ![image](https://user-images.githubusercontent.com/86371082/123688816-1f6b6200-d870-11eb-9f7b-86c1d84f805b.png)
  
  3. The standard cells are mentioned for different gates (AND, OR, INVERTER, etc) as below: 
 
  ![image](https://user-images.githubusercontent.com/86371082/123688888-3742e600-d870-11eb-9655-0b563970137f.png)

  4.The feature such as the leakage power of different cells are mentioned, for example for the cell “sky130_df_sc_hd_a210i_4” and its corresponding Verilog model which gives the logical operation for the cell is shown as below: -
  
  ![image](https://user-images.githubusercontent.com/86371082/123688969-53df1e00-d870-11eb-914c-672177047ad1.png)
 
  Note here: -
    A.a210i stands for 2 input A1 and A2 undergoes AND operation, the output of this operation will undergo OR operation with B1 and the output of this entire operation is         inverted as below: -
  
  ![image](https://user-images.githubusercontent.com/86371082/123689094-796c2780-d870-11eb-940e-cf5289564060.png)
  

  ![image](https://user-images.githubusercontent.com/86371082/123689191-943e9c00-d870-11eb-80fd-1d1a19c86d3b.png)

 
   B. If you could observe above cell “sky130_df_sc_hd_a210i_4” has 3 input and hence there could be 8 possible inputs, hence for all the 8 possible inputs the leakage power        is mentioned as below:-
   
  
  ![image](https://user-images.githubusercontent.com/86371082/123689248-a3bde500-d870-11eb-9779-7c0bcc0d46ee.png)
  
  ![image](https://user-images.githubusercontent.com/86371082/123689288-af111080-d870-11eb-8b7a-4ffd7c3cff7a.png)

 
	 5. Library contains all the specification such as power, delay, capacitance with respect to each pin, example 
      for pin A1 is shown below: -
  
  ![image](https://user-images.githubusercontent.com/86371082/123689325-bcc69600-d870-11eb-9511-494bf8e5c02b.png)
 

	6. Below is the comparison of the area of the standard cells a210_1, a210_1, and a210_4. We can note here that:

  	A. sky130_fd_sc_hd__a21o_2
    
    
   ![image](https://user-images.githubusercontent.com/86371082/123691174-e7b1e980-d872-11eb-8d80-2facd4c01380.png)
   
   ![image](https://user-images.githubusercontent.com/86371082/123691228-fac4b980-d872-11eb-8bb9-5e19b613bfb4.png)
     



	B. sky130_fd_sc_hd__a21o_1
  
  ![image](https://user-images.githubusercontent.com/86371082/123689522-f13a5200-d870-11eb-8fd2-928dac4f15e9.png)
  
  ![image](https://user-images.githubusercontent.com/86371082/123689551-f7c8c980-d870-11eb-85ee-09c5ea21970b.png)
   


	C. sky130_fd_sc_hd__a210_4
  
  ![image](https://user-images.githubusercontent.com/86371082/123689598-02835e80-d871-11eb-9b7b-3d8f4722e2f3.png)
  
  ![image](https://user-images.githubusercontent.com/86371082/123689634-0d3df380-d871-11eb-883b-fed006d5a105.png)


 
       
The above observation can be summarized in the table below:-


CELL	Area	Delay	Power	Cell
Width
sky130_fd_sc_hd__a21o_1	7.5072
	Maximum	Minimum	Minimum
sky130_fd_sc_hd__a21o_2	8.75854
	Intermediate	Intermediate	Intermediate
sky130_fd_sc_hd__a21o_4	15.0144
	Minimum	Maximum	Maximum

Hierarchical Synthesis v/s Flat Synthesis
To understand the command “synth -top <Design_Top_module>” used in the synthesis tool Yosys, the below example of a Verilog design was taken.
 
The expected output as per the code above is as following:-
 
Now Synthesize the above design using Yosys tool, some of the simple command used here are:
read_liberty -lib <library_path>
read_verilog <design_path >
synth -top <top_module_name>
abc -liberty <library_path>

Now to look at the synthesised design, the command used is “show <multiple_modules>”
The output given by the tool is as below:
 
This is hierarchical design, where we don’t see the gates 
Now we write the netlist write verilog -attr <>
module sub_module1(a, b, y);
  wire _0_;
  wire _1_;
  wire _2_;
  input a;
  input b;
  output y;
  sky130_fd_sc_hd__and2_0 _3_ (
    .A(_1_),
    .B(_0_),
    .X(_2_)
  );
  assign _1_ = b;
  assign _0_ = a;
  assign y = _2_;
endmodule

module sub_module2(a, b, y);
  wire _0_;
  wire _1_;
  wire _2_;
  input a;
  input b;
  output y;
sky130_fd_sc_hd__lpflow_inputiso1p_1 _3_ (
    .A(_1_),
    .SLEEP(_0_),
    .X(_2_)
  );
  assign _1_ = b;
  assign _0_ = a;
  assign y = _2_;
endmodule
Next, we use the command “flatten” and then write the Verilog module. The difference is the hierarchy of the design is preserved, however not preserved in flat model its one single netlist
Then use show command.
 
Synthesized at sub module level.

Then the various Flop coding styles and optimization associated were discussed.
 
	Both Async reset and sync reset --no race condition
	But both set and reset ---cause race condition

 

Session -3
Introduction to Logic Optimizations
                                              
Combinational Logic Optimization
Goal:
	Reduced Area
	Reduced Power
Method Used for Optimization:
	Constant propagation
	Direct Optimization
Example: -
 
The CMOS construction for the above example is as below: -

 (https://images.slideplayer.com/17/5347720/slides/slide_11.jpg)
Let’s assume A=0, then the OUT=D ̅, hence the entire Logic reduces to an inverter as below: -
 
 


	Boolean logic optimization
	K-Map
	Quine McKluskey


Sequential Logic Optimization
	Basic method is sequential constant propagation
	Advanced methods are: -
	State Optimization
	Retiming
	Sequential Logic Cloning (Floor Plan Aware Synthesis)
Lab Work: -
 
 
 
 
 

Before Opt_clean -purge

 
After Opt_clean -purge
 
Multimode_opt flatten nd then opt clean
First design will infer a flop but the second one will not
Check for potential race here---my inference
Modify above code
 
Synthesis: -
 

Session -4
GLS, Blocking vs Non-Blocking and Synthesis-Simulation Mismatch
Gate-Level-Simulation (GLS):
	Running the test bench with Netlist as Design Under Test (DUT)
	Netlist is logically same as RTL Code.
	Same Test Bench will align with the Design.
	GLS verifies the logical correctness of design after synthesis
	Ensuring the timing of the design is met.
	For this GLS needs to be run with delay annotation
 
Fig: GLS input and output
The Yosys tool maps the design in RTL to gate level netlist like in figure above using the gate level Verilog model during synthesis. The gate level Verilog model can be functional and/or timing aware.


 
Fig: Mapping Of RTL Code to Gat-Level-Netlist


First design a MUX, the steps are as below as performed in the lab.

 
 
 

Check for the RTL simulation in GTKWave as below.
 

Yosys Lab steps for Synthesis:
 
 
 
 
 
Below is the MUX design after synthsis in Yosys as expected using the gates.
 
The gatelevel netlist from Yosys tool can be generated as below:
 


Below is the snippet of the gatelevel netlist:
 
Simulation Mismatch (RTL Simulation v/s GLS):

                                                  
	Missing Sensitivity List:
During the GLS the simulator will check for the sensitivity list, however during synthesis the tool is interested only in functionality not the sensitivity list, so basically GLS checks for the proper working of a design. Below is the example of a simulation mismatch in the RTL design and GLS for MUX due to missing sensitivity list. The design are referred as bad and good MUX as below.


 
 
 
 
 
 

 
CONCLUSION: 
We can clearly see the GLS and RTL simulation mismatch for bad_mux design and the difference are shown below marked.
 

	Blocking v/s Non-Blocking Assignment:

	Inside Always block
	“=”  Blocking
	Executes the statement in the order it is written
	So, the first statement is evaluated before the second statement
	“<=”  Non-Blocking
	Executes all the RHS when always block is entered and assigns to LHS
	Parallel evaluation


 
	After analyzing the above code ‘x’ looks like a flopped output 
The simulation for the above design is as below and the discrepancy is marked.
 

Logic after synthesis is as below: -
 

After synthesis the GLS is as below.
 


CONCLUSION: -
We can clearly see the GLS and RTL simulation mismatch due to blocking statement for blocking_caveat design and the difference are shown above marked. Always be careful while you use the blocking statement

Session 5
if, case, for loop and for generate
	if, case
	“if ” is used to create priority logic.
	The syntax of “if” is as below.

 
	While you use the if, case statement the hardware realized is a MUX as below.

 

Care to be taken while you use the “if, case” statement.
	The “if” statement should be complete, if incomplete it leads to INFERRED LATCHES. This leads to bad coding style. The example is as below.

 
	Above statement cannot be generalized for counter design as below, where you use incomplete if, case statement, where if no “en” count should latch on to previous value, hence depends on the intent of the design. Always draw the design before you code.

 
	If, case statement is used inside the always block
	Code for the default statement and avoid partial assignments in “case” else it will lead to inferred latches in hardware. Assign all the outputs in all segments of case:-

Acknowledgement



