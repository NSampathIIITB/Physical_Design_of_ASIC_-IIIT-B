# Physical_Design_of_ASIC_IIIT-B

This github repository summarises the progress made in the Physical Design of ASIC program. Quick links:

[Day-0 : Installation of required Software Tools](#day-0)

[Day-1 : Introduction to Verilog RTL Design and Synthesis](#day-1)

[Day-2 : Timing libs, Hierarchical vs Flat synthesis and Various flop coding styles and Optimisation](#day-2)

[Day-3 : Combinational and Sequential Optmizations](#day-3)

[Day-4 : GLS, Blocking vs Non-blocking and Synthesis-Simulation mismatch](#day-4)

[Day-5 : If, Case, For loop and For generate](#day-5)




[Acknowledgement](#acknowledgement)

[Reference](#reference)


## Day-0 
<details>
 <summary> Summary </summary>
 
	
I installed all the needed Software tools.

</details>	

<details>
 <summary> Yosys </summary>


 I installed Yosys using the following commands:
 
```
git clone https://github.com/YosysHQ/yosys.git
cd yosys-master 
sudo apt install make 
sudo apt-get install build-essential clang bison flex \
    libreadline-dev gawk tcl-dev libffi-dev git \
    graphviz xdot pkg-config python3 libboost-system-dev \
    libboost-python-dev libboost-filesystem-dev zlib1g-dev
make 
sudo make install

```

Below is the screenshot showing sucessful installation:

![Screenshot from 2023-07-31 18-25-48](https://github.com/NSampathIIITB/Physical_Design_of_ASIC_IIIT-B/assets/141038460/edbd81f3-dc1f-4618-91b2-b6cbc66876a9)
</details>

 <details>
 <summary> OpenSTA </summary>


 I installed and built OpenSTA (including the needed packages) using the following commands:
 ```
sudo apt-get install cmake clang gcctcl swig bison flex
git clone https://github.com/The-OpenROAD-Project/OpenSTA.git
cd OpenSTA
mkdir build
cd build
cmake ..
make
```
Below is the screenshot showing sucessful installation:

![Screenshot from 2023-07-31 18-52-06](https://github.com/NSampathIIITB/Physical_Design_of_ASIC_IIIT-B/assets/141038460/45fca339-3b10-4afa-9e49-48c358cc07f1)
</details>

<details>
 <summary> Iverilog </summary>


 I installed Iverilog using the following command:
  ```
sudo apt-get install iverilog
 ```
 Below is the screenshot showing sucessful installation:

 ![Screenshot from 2023-07-31 18-26-28](https://github.com/NSampathIIITB/Physical_Design_of_ASIC_IIIT-B/assets/141038460/39cb367f-8681-41db-a1ef-9de239845657)
</details>

<details>
 <summary> GTKWave </summary>


 I installed GTKWave using the following command:
  ```
sudo apt-get install gtkwave
 ```
 Below is the screenshot showing sucessful installation:
![Screenshot from 2023-07-31 18-27-35](https://github.com/NSampathIIITB/Physical_Design_of_ASIC_IIIT-B/assets/141038460/6fcb06cc-816a-41b4-9e53-b55f9315b92a)
</details>

<details>
 <summary> ngspice </summary>


 I downloaded the tarball from https://sourceforge.net/projects/ngspice/files/ to a local directory and unpacked it using the following commands:
 ```
tar -zxvf ngspice-37.tar.gz
cd ngspice-37
mkdir release
cd release
../configure  --with-x --with-readline=yes --disable-debug
make
sudo make install
 ```
Below is the screenshot showing sucessful installation:

![Screenshot from 2023-07-31 19-00-53](https://github.com/NSampathIIITB/Physical_Design_of_ASIC_IIIT-B/assets/141038460/4f8b2756-fa2a-4e9a-8a06-1b7a7fdc6d5c)
</details>

<details>
 <summary> OpenLANE </summary>


 I installed gtkwave using the following command:
 
  ```sudo apt-get update
sudo apt-get upgrade
sudo apt install -y build-essential python3 python3-venv python3-pip make git
sudo apt install apt-transport-https ca-certificates curl software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt update
sudo apt install docker-ce docker-ce-cli containerd.io
sudo docker run hello-world
sudo groupadd docker
sudo usermod -aG docker $USER
sudo reboot
 ```
 Below is the screenshot showing sucessful installation:

 ![Screenshot from 2023-07-31 19-33-48](https://github.com/NSampathIIITB/Physical_Design_of_ASIC_IIIT-B/assets/141038460/82feea18-9b24-4377-83bd-ccafdd2205c5)
 </details>

 ## Day-1
 <details>
 <summary> Summary </summary>
	 
 In this class we had briefly discussed about Simulation and Synthesis and we also performed simulation and synthesis of 2x1 Mux using Iverilog ,GTKWave and Yosys.

 </details>
 
 <details>
 <summary> Simulation </summary>

 This section gives a brief explanation about Simulation


<b> Simulator: </b> It is a tool used to check if it adheres to the designed specs by simualting the code. <br>
<br>
<b> Design: </b> It is the actual verilog code or set of verilog codes which has the intended functionality to meet with the required functionality/speciifications. Design file contains one or more input/output ports.<br>
<br>
<b> TestBench: </b> It is the setup to apply stimulus to the design to check its functionality. Testbench doesnot contain any input/output ports. <br>
<br>
<b> How does a Simulator Works ? </b> <br>
- Simulator looks for change on the input signal to produce a output signal.<br>
- Upon change in the input signal the output signal is evaluated. i.e, If there is no change in input the output will not be evaluated.<br>
<br>
<p align="center">
<img src="https://user-images.githubusercontent.com/62461290/183845210-c3b9712f-c56f-4d62-98d4-34d22ad78f10.png"> <br>
General Simulation Flow
</p>
<br>
<p align="center">
<img src="https://user-images.githubusercontent.com/62461290/183845405-c8a1de5c-f949-4962-9952-6bf8e68c164f.png"> <br>
iVerilog Based Simulation Flow
</p>
 
</details>	

<details>
 <summary> Simulation of 2x1 Mux using Iverilog and GTKWave </summary>

We were introducted to Linux operating system and were made aware of the basic commands. Using **git clone** command we've cloned library files like standard cell library, primitives which are used for synthesis and few verilog codes for practice.

**Steps to download the lab folder**</br>
```
mkdir VLSI
cd VLSI
git clone https://github.com/kunalg123/vsdflow.git
git clone https://github.com/kunalg123/sky130RTLDesignAndSynthesisWorkshop.git

```
![Screenshot from 2023-08-09 10-09-10](https://github.com/NSampathIIITB/Physical_Design_of_ASIC_IIIT-B/assets/141038460/fcb5c437-08f6-485e-9da3-c2b8d069fd76)


In this session, I've performed simulation of 2x1 multiplexer. I've added both the RTL design code and testbench code in iverilog to generate vcd file which I used in gtkwave generator to get the output waveformes after simulation. The output was generated by taking the inputs from the testbench code.

**Iverilog**:Iverilog stands for Icarus Verilog. It is a widely-used open-source Verilog simulation and synthesis tool that allows designers to simulate and synthesize digital hardware designs described in Verilog HDL.It supports the 1995, 2001 and 2005 versions of the standard, portions of SystemVerilog, and some extensions.

**GTKWave**: GTKWave is a popular open-source waveform viewer designed to visualize and analyze simulation results of digital designs. As an essential tool in digital hardware development, GTKWave allows users to examine waveforms generated by Verilog or VHDL simulation, making it easier to debug and verify the behavior of complex digital circuits.It  reads LXT, LXT2, VZT, FST, and GHW files as well as standard Verilog VCD/EVCD files and allows their viewing.

These are the following commands that I used to simulate and view the plots of the RTL design:
	
 ```
 iverilog <name verilog: good_mux.v> <name testbench: tb_good_mux.v>
 ./a.out
 gtkwave tb_good_mux.vcd

 ```
Below is the screenshot of the gtkwave plots:

![Screenshot from 2023-08-09 10-27-23](https://github.com/NSampathIIITB/Physical_Design_of_ASIC_IIIT-B/assets/141038460/0a6c3a5f-74bc-47e8-ab41-62598baf9cb6)


Here is the verilog code :<br />

	module good_mux (input i0 , input i1 , input sel , output reg y); 
		always @ (*)
		begin
			if(sel)
			y <= i1;
			else 
			y <= i0;
		end
	endmodule


	`timescale 1ns / 1ps
	module tb_good_mux;
	// Inputs
	reg i0,i1,sel;
	// Outputs
	wire y;
      		// Instantiate the Unit Under Test (UUT), name based instantiation
		good_mux uut (.sel(sel),.i0(i0),.i1(i1),.y(y));
		//good_mux uut (sel,i0,i1,y);  //order based instantiation
	initial begin
		$dumpfile("tb_good_mux.vcd");
		$dumpvars(0,tb_good_mux);
		// Initialize Inputs
		sel = 0;
		i0 = 0;
		i1 = 0;
		#300 $finish;
	end
	always #75 sel = ~sel;
	always #10 i0 = ~i0;
	always #55 i1 = ~i1;
	endmodule
 
 uut(unit under test) : It is the normal convention to name the top level module called in testbench as an uut. <br>

 </details>
 
 <details>
 <summary> Synthesis </summary>
 This section gives a brief explanation about Synthesis.

 <b> Synthesis: </b> <br>
- The RTL design is converted into gates and the connections are made between gates. <br>
- This is given out as a file called netlist. <br>

 <b> Synthesis takes place in multiple steps: </b> <br>
- Converting RTL into simple logic gates.
- Mapping those gates to actual technology-dependent logic gates available in the technology libraries.
- Optimizing the mapped netlist keeping the constraints set by the designer intact.


**Synthesizer**: It is a tool we use to convert out RTL design code to netlist. Yosys is the tool I've used in this workshop.
Here is the flow of above processess.

<p align="center">
<img src="https://user-images.githubusercontent.com/62461290/183910992-4910d098-f175-484f-8dcc-20a989d41967.png"> <br>
</p>

**Yosys**:Yosys is a framework for RTL synthesis and more. It currently has extensive Verilog-2005 support and provides a basic set of synthesis algorithms for various application domains. Yosys is the core component of most our implementation and verification flows.

I was given an overview of the operation of the tool and the files we'll need to provide the tool to give the required netlist. We give RTL design code, .lib file which has all the building blocks of the netlist. Using these two files, Yosys synthesizer generates a netlist file. .lib basically is a collection of logical modules like, And, Or, Not etc.... These are equivalent gate level representation of the RTL code. 

Below are the commands to perform above synthesis.
```
 RTL Design  - read_verilog
 .lib        - read_liberty
 netlist file- write_verilog
```

**Operational flow of Yosys Synthesizer**

![Synthesizer](https://user-images.githubusercontent.com/104454253/166094901-27c70c0d-8ef2-4a34-a4b2-7307af492698.JPG)

**Verification of Synthesized design**: In order to make sure that there are no errors in the netlist, we'll have to verify the synthesized circuit. The netlist verification flow can be seen in the below image:

![Synthesisgtkwave](https://user-images.githubusercontent.com/104454253/166095185-f82dbbe0-afb4-43ac-8ec6-6b75491d6b58.JPG)

The gtkwave output for the netlist should match the output waveform for the RTL design file. As netlist and design code have same set of inputs and outputs, we can use the same testbench and compare the waveforms.

**Introduction to logic synthesis**: Below is the snippet RTL code and equivalent digital circuit:

![sample rtl](https://user-images.githubusercontent.com/104454253/166097112-0fb5685c-fe88-4ca0-8ecf-bc014de46088.JPG)

In the above image, mapping of code and digital circuit is done using Synthesis.

<b> .lib </b>
- It contains all different kind of logic modules. like AND, OR, NOR etc.<br>
- It contains different variants of the same gate as well. like 2-input, 3-input, 4-input, slow, fast, medium gates etc.<br>

**Need for different flavours of gate**: In order to make a faster circuit, the clock frequency should be high. For that the time period of the clock should be as low as possible. However, in a sequential circuit, clock period depends on three factors so that data is not lost or to be glitch free.

For the below circuit the three factors are
- Clock to Q of flipflop A
- Propagation delay of combinational circuit
- Setuptime of flipflop B
![Timedelay circuit](https://user-images.githubusercontent.com/104454253/166098730-33bf0734-abec-466f-abe2-a2ac6813b5e0.JPG)

The equation is as follows

![Time](https://user-images.githubusercontent.com/104454253/166097710-2c1099e3-6323-496c-8eb7-12ee04c12096.JPG)

As per the above equation, for a smaller propagation delay, we need faster cells.
But again, why do we have faster cells? This is to ensure that there are no HOLD time violations at B flipflop.
**This complete collection forms .lib**

There are different kind of gates available to take in account the performance parameters like Delay, Area, Power into consideration. <br>
- If we choose speed we trade off area and power likewise if we choose area we trade off delay. Hence we have to choose them either based on the design constrains or find a sweet spot between all of them.
- Load in a digital logic circuit is a capacitor. <br>
- Faster the charging and discharging of capacitance the lesser is the delay. <br>
- To charge/Discharge the capacitor fast, we need transistors capable of sourcing more current. <br>
- Wider transistors -> low delay -> More Power and Area. <br>
- Narrow transitor -> More delay -> Less Area and Power. <br>

<b> Selection of Cells </b> <br>
- Need to guide the synthesizer to select the flavour of cells that is optimum for the implementation of logic circuits. <br>
- More use of fast cells can be bad interms of power and area. <br>
- More use of slow cells can lead to a sluggish circuit. <br>
- The guidence offered to the synthesizer is called constraints <br>

Below is an illustration of Synthesis.

![Screenshot (44)](https://user-images.githubusercontent.com/104454253/166099264-e3842e91-1a27-44ae-830c-0757dc5b1a5e.png)

</details>
 
 <details>
 <summary> Synthesis of 2x1 Mux netlist using Yosys </summary>

 These are the following commands that I used in Yosys.
 
 ```
cd /home/nsaisampath/vsd/VLSI/sky130RTLDesignAndSynthesisWorkshop/verilog_files
yosys
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
read_verilog good_mux.v
synth -top good_mux
bc -liberty /home/nsaisampath/vsd/VLSI/sky130RTLDesignAndSynthesisWorkshop/lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
write_verilog good_mux_netlist.v 
!vim good_mux_netlist.v 
 write_verilog -noattr good_mux_netlist.v
 !vim good_mux_netlist.v
```

**read_liberty**- Read cells from liberty file as modules into current design. The ***-lib*** switch creates empty blackbox modules.</br>
**read_verilog** - Loads modules from  verilog file to the current design.</br>
**read_liberty** - Read cells from liberty file as modules into current design. The ***-lib*** switch creates empty blackbox modules.</br>
**read_verilog** - Loads modules from  verilog file to the current design.</br>
**synth** - command runs the default synthesis script. The ***-top*** switch use the specified module as top module.</br>
**abc** -  This command uses the ABC tool for technology mapping of yosys's internal gate library to a target architecture. The ***-lib*** switch liberty <file>
generate netlists for the specified cell library using the liberty file format.</br>
**show** - Creates a graphviz DOT file for the selected part of the design and compile it to a graphics file. It generates a schematic.</br>
**write_verilog** - Writes the current design to a Verilog file. The ***-noattr** switch skips the attributes from included in the output netlist</br>
 

	 
**Invoking Yosys:**
![Screenshot from 2023-08-09 10-49-26](https://github.com/NSampathIIITB/Physical_Design_of_ASIC_IIIT-B/assets/141038460/b0c70c5b-ede5-41af-bdcf-56c60677497f)
![Screenshot from 2023-08-09 10-55-23](https://github.com/NSampathIIITB/Physical_Design_of_ASIC_IIIT-B/assets/141038460/aa350caf-c05b-49d4-8599-042412035ec0)

**Reading the verilog design file:**
![Screenshot from 2023-08-09 11-01-00](https://github.com/NSampathIIITB/Physical_Design_of_ASIC_IIIT-B/assets/141038460/46aec4a8-48c5-4cdf-9982-7bc576845daf)

**Synthesize the verilog file:**
![Screenshot from 2023-08-09 11-07-33](https://github.com/NSampathIIITB/Physical_Design_of_ASIC_IIIT-B/assets/141038460/757a57f3-7ba5-4e45-9ef6-3d8062cca145)

**Netlist generation:**
![Screenshot from 2023-08-09 11-08-13](https://github.com/NSampathIIITB/Physical_Design_of_ASIC_IIIT-B/assets/141038460/6970db67-c4e7-4898-97ab-dc1531070324)
![Screenshot from 2023-08-09 11-08-29](https://github.com/NSampathIIITB/Physical_Design_of_ASIC_IIIT-B/assets/141038460/8d5b1d7c-26db-46ca-a04f-348186c6a108)
![Screenshot from 2023-08-09 11-09-10](https://github.com/NSampathIIITB/Physical_Design_of_ASIC_IIIT-B/assets/141038460/f7bf8bc7-a936-402b-b466-e21a01c7c08a)

**Netlist code:**
![Screenshot from 2023-08-09 11-19-03](https://github.com/NSampathIIITB/Physical_Design_of_ASIC_IIIT-B/assets/141038460/02b63c60-5b8d-4e71-8825-4804664216dd)


**Simplified netlist code:** This code consisits of additional switch. To further simplify, we use below command
![Screenshot from 2023-08-09 11-20-48](https://github.com/NSampathIIITB/Physical_Design_of_ASIC_IIIT-B/assets/141038460/99b31ffd-27d9-4090-a4e2-ea8a9e48758f)


</details>	

## Day-2
<details>
 <summary> Exploring the Timing.lib files </summary>
	
 To view the contents inside the .lib file type the following command :
```
cd ASIC/sky130RTLDesignAndSynthesisWorkshop/lib/gvim sky130_fd_sc_hd__tt_025C_1v80.lib
```
![Screenshot from 2023-08-09 16-32-14](https://github.com/NSampathIIITB/Physical_Design_of_ASIC_IIIT-B/assets/141038460/3211e9a1-aafb-4790-8a14-dbde553f55a6)

This lab guides us through the .lib files where we have all the gates coded in. According to the below parameters the libraries will be characterized to model the variations.

![lib1](https://user-images.githubusercontent.com/104454253/166105787-19a638a3-fe01-4fcf-828d-0b56a6acb8f7.JPG)

With in the lib file, the gates are delared as follows to meet the variations due to process, temperatures and voltages.

 **Different flavour cells in the .lib:**
 ![Screenshot from 2023-08-09 16-45-34](https://github.com/NSampathIIITB/Physical_Design_of_ASIC_IIIT-B/assets/141038460/cae6da02-a104-4166-90b5-0c619b0ed09b)
 
This image displays the power consumtion comparision.

![lib5](https://user-images.githubusercontent.com/104454253/166107259-6fa398a4-2099-4da3-9b93-818c2c3f2404.JPG)

Below image is the delay order for the different flavor of gates.

![delay_libraries](https://user-images.githubusercontent.com/104454253/166187423-d21465e1-abc3-4ad0-a534-60f8e706ab6f.JPG)


</details>

<details>
<summary> Hierarchical Synthesis v/s Flat Synthesis </summary>
	
**Hierarchial Synthesis:**
	
Hierarchical synthesis is breaking a complex modules into smaller, more manageable sub-modules or blocks. Each of these sub-modules can be synthesized or designed independently before being integrated into the larger system. This approach allows for efficient design, optimization, and verification of individual components while maintaining a structured and organized design process.The design hierarchy can have multiple levels, with modules containing sub- modules and so on.

**Flat Synthesis:**
In flat synthesis, the entire digital circuit is synthesized as a single monolithic unit, without breaking it down into smaller modules. This approach is suitable for smaller designs where the complexity doesn't warrant a hierarchical organization.

In this section we are going to sythesize the same design in both Hierarchical and Flat to illustrate the difference in the netlist of both.


An illustration of the hierarchical synthesis is shown below :

Consider the verilog file multiple module which is given in the verilog_files directory
 ```
module sub_module2 (input a, input b, output y);
	assign y = a | b;
endmodule

module sub_module1 (input a, input b, output y);
	assign y = a&b;
endmodule


module multiple_modules (input a, input b, input c , output y);
	wire net1;
	sub_module1 u1(.a(a),.b(b),.y(net1));  //net1 = a&b
	sub_module2 u2(.a(net1),.b(c),.y(y));  //y = net1|c ,ie y = a&b + c;
endmodule
 ```
This is the schematic as per the connections in the above module.

![WhatsApp Image 2023-08-12 at 10 35 37](https://github.com/NSampathIIITB/Physical_Design_of_ASIC_IIIT-B/assets/141038460/1734474c-2aa1-427e-9318-465924588777)

However, the yosys synthesizer generates the following schematic instead of the above one and with in the submodules, the connections are made

```
$ yosys
yosys> read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
yosys> read_verilog multiple_modules.v
yosys> synth -top multiple_modules
yosys> show multiple_modules 

```
![Screenshot from 2023-08-12 00-00-51](https://github.com/NSampathIIITB/Physical_Design_of_ASIC_IIIT-B/assets/141038460/0f9fdab5-2d4c-42e9-adc4-ceba121a1ef7)

The synthesizer considers the module hierarcy and does the mapping accordting to instantiation. Here is the hierarchical netlist code for the  multiple_modules:

	module multiple_modules(a, b, c, y);
		  input a;
 		 input b;
 		 input c;
		  wire net1;
 		 output y;
 	  sub_module1 u1 (.a(a),.b(b),.y(net1) );
	  sub_module2 u2 (.a(net1),.b(c),.y(y));
	endmodule
	
	module sub_module1(a, b, y);
 	 wire _0_;
 	 wire _1_;
 	 wire _2_;
 	 input a;
 	 input b;
 	 output y;
 	 sky130_fd_sc_hd__and2_0 _3_ (.A(_1_),.B(_0_),.X(_2_));
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
 	 sky130_fd_sc_hd__lpflow_inputiso1p_1 _3_ (.A(_1_),.SLEEP(_0_),.X(_2_) );
 	 assign _1_ = b;
 	 assign _0_ = a;
 	 assign y = _2_;
	endmodule

Flattened netlist:

In flattened netlist, the hierarcies are flattend out and there is single module i.e, gates are instantiated directly instead of sub_modules. Here is the flattened netlist code for the  multiple_modules:

	module multiple_modules(a, b, c, y);
 		 wire _0_;
  		 wire _1_;
 		 wire _2_;
 		 wire _3_;
		 wire _4_;
		 wire _5_;
 		 input a;
 		 input b;
 		 input c;
 		 wire net1;
 		 wire \u1.a ;
		 wire \u1.b ;
		 wire \u1.y ;
		 wire \u2.a ;
		 wire \u2.b ;
 		 wire \u2.y ;
  		output y;
 		 sky130_fd_sc_hd__and2_0 _6_ (
  		  .A(_1_),
  		 .B(_0_),
   		 .X(_2_)
  		);
 		 sky130_fd_sc_hd__lpflow_inputiso1p_1 _7_ (
  		  .A(_4_),
 		  .SLEEP(_3_),
  		  .X(_5_)
 		 );
 		 assign _4_ = \u2.b ;
 		 assign _3_ = \u2.a ;
 		 assign \u2.y  = _5_;
 		 assign \u2.a  = net1;
		 assign \u2.b  = c;
 		 assign y = \u2.y ;
		 assign _1_ = \u1.b ;
		 assign _0_ = \u1.a ;
		 assign \u1.y  = _2_;
		 assign \u1.a  = a;
		 assign \u1.b  = b;
 		 assign net1 = \u1.y ;
		endmodule

The commands to get the hierarchical and flattened netlists is shown below:

**yosys> write_verilog -noattr multiple_modules_hier.v**

8. Executing Verilog backend.
Dumping module `\multiple_modules'.
Dumping module `\sub_module1'.
Dumping module `\sub_module2'.

**yosys> !gvim multiple_modules_hier.v**

11. Shell command: gvim multiple_modules_hier.v

**yosys> flatten**

12. Executing FLATTEN pass (flatten design).
Deleting now unused module sub_module1.
Deleting now unused module sub_module2.
<suppressed ~2 debug messages>

**yosys> write_verilog -noattr multiple_modules_flat.v**

13. Executing Verilog backend.
Dumping module `\multiple_modules'.

**yosys> !gvim multiple_modules_flat.v**

14. Shell command: gvim multiple_modules_flat.v

This is the synthyesized circuit for a flattened netlist. Here u1 and u2 are flattened and directly or gates are realized.

![Screenshot from 2023-08-12 10-15-43](https://github.com/NSampathIIITB/Physical_Design_of_ASIC_IIIT-B/assets/141038460/d7a98ae8-39b2-425d-a8ad-81e21166cf74)


Here is the synthesized circuit of sub_module1. We are also generating module level synthesis so that if there is a top module with multiple and same sub_modules, we can synthesize it once and can use and connect the same netlist multiple times in the top module netlist.

Another reason to generate module level synthesis and then stictch them together is to avoid errors in a top module if its massive and consists of several sub modules. Generating netlist for synthesis and then stiching it together in top level becomes easier and reduces risk of output mismatch.

We control this synthesis using **synth -top <module_name>** command

![Screenshot from 2023-08-12 10-27-32](https://github.com/NSampathIIITB/Physical_Design_of_ASIC_IIIT-B/assets/141038460/cb3e29da-6e92-4863-9534-36473078c486)

 </details>
 
 <details>
<summary> Various Flop Coding styles and Optimisation </summary>
	 
**Why Flops and Flop coding styles**

In this session, the discussion was about how to code various types of flops and various styles of coding a flop.

**Why a Flop?**

 In a combinational circuit, the output changes after the propagation delay of the circuit once inputs are changed. During the propagation of data, if there are different paths with different propagation delays, there might be a chance of getting a glitch at the output.<br />
 
 **Here is an example showing how a glitch is formed**
 
![WhatsApp Image 2023-08-12 at 11 55 42](https://github.com/NSampathIIITB/Physical_Design_of_ASIC_IIIT-B/assets/141038460/8d2233a3-8c47-4093-8280-a3cc63d8182c)

 In our design we are going to have more no of combinational circuits if there are multiple combinational circuits in the design, the occurances of glitches are more thereby making the output unstable.<br />

![WhatsApp Image 2023-08-12 at 12 08 23](https://github.com/NSampathIIITB/Physical_Design_of_ASIC_IIIT-B/assets/141038460/eedd9847-6435-474f-bc39-eeb534a0882b)
 
To curb this drawback, we are going for flops to store the data from the cominational circuits. When a flop is used, the output of combinational circuit is stored in it and it is propagated only at the posedge or negedge of the clock so that the next combinational circuit gets a glitch free input thereby stabilising the output.

![WhatsApp Image 2023-08-12 at 12 08 23(1)](https://github.com/NSampathIIITB/Physical_Design_of_ASIC_IIIT-B/assets/141038460/41204024-efa6-4d3c-add0-7fdbf9a04942)
 
 We use initialize signals or control pins called **set** and **reset** on a flop to initialize the flop, other wise a garbage value to sent out to the next combinational circuit. These control pins can be synchronous or asynchronous.

 **How do I code the Flop:**
 
 The various coding styles of flops are: <br>
1. Flop with Synchronous Reset : It resets the flop with respect to condition of the clock
2. Flop with Synchronous Set : It sets the flop with respect to condition of the clock
3. Flop with Asynchronous Reset : It resets the flop irrespect of the condition of the clock
4. Flop with Asynchronous Set : It sets the flop irrespect of the condition of the clock
5. Flop with both Synchronous and Asynchronous Reset : It resets the flop both with respect to condition of the clock and irrespective of it.

**Simulation and Synthesis of Various D Flipflops:**

**d-flipflop with asynchronous reset**- Here the output **q** goes low whenever reset is high and will not wait for the clock's posedge, i.e irrespective of clock, the output is changed to low.

![WhatsApp Image 2023-08-12 at 14 53 20](https://github.com/NSampathIIITB/Physical_Design_of_ASIC_IIIT-B/assets/141038460/9da8658b-149c-4eb9-8fa2-4992826c418a)
 
	 module dff_asyncres ( input clk ,  input async_reset , input d , output reg q );
		always @ (posedge clk , posedge async_reset)
		begin
			if(async_reset)
				q <= 1'b0;
			else	
				q <= d;
		end
	endmodule

**Simulation**:

![Screenshot from 2023-08-12 15-07-08](https://github.com/NSampathIIITB/Physical_Design_of_ASIC_IIIT-B/assets/141038460/2788889b-f09b-4a11-95ab-f0636f88940b)

**Synthesized circuit**:

![Screenshot from 2023-08-12 15-49-50](https://github.com/NSampathIIITB/Physical_Design_of_ASIC_IIIT-B/assets/141038460/62cd33d4-8cf9-4fed-bebc-af76b123ab90)

**d-flipflop with asynchronous set**- Here the output **q** goes high whenever set is high and will not wait for the clock's posedge, i.e irrespective of clock, the output is changed to high.

![WhatsApp Image 2023-08-12 at 15 11 35](https://github.com/NSampathIIITB/Physical_Design_of_ASIC_IIIT-B/assets/141038460/d2dd91f0-06b8-4f91-955a-7901c6ff6abc)
 

	module dff_async_set ( input clk ,  input async_set , input d , output reg q );
		always @ (posedge clk , posedge async_set)
		begin
			if(async_set)
				q <= 1'b1;
			else
				q <= d;
		end
	endmodule

**Simulation**:

![Screenshot from 2023-08-12 15-14-46](https://github.com/NSampathIIITB/Physical_Design_of_ASIC_IIIT-B/assets/141038460/29823b69-b836-41d7-95d1-acef472e8e73)

**Synthesized circuit**:

![Screenshot from 2023-08-12 15-51-52](https://github.com/NSampathIIITB/Physical_Design_of_ASIC_IIIT-B/assets/141038460/14b784cc-8147-45f6-8c78-fd95c7175e77)


**d-flipflop with synchronous reset**- Here the output **q** goes low whenever reset is high and at the positive edge of the clock. Here the reset of the output depends on the clock.

![WhatsApp Image 2023-08-12 at 15 00 57](https://github.com/NSampathIIITB/Physical_Design_of_ASIC_IIIT-B/assets/141038460/68017004-8197-4c0a-9506-0f465a34baae)


        module dff_syncres ( input clk , input async_reset , input sync_reset , input d , output reg q );
		always @ (posedge clk )
		begin
			if (sync_reset)
				q <= 1'b0;
			else	
				q <= d;
		end
	endmodule
 
 **Simulation**
 
 ![Screenshot from 2023-08-12 15-20-24](https://github.com/NSampathIIITB/Physical_Design_of_ASIC_IIIT-B/assets/141038460/5ec7f4ab-aa4b-457f-8d8c-a20b6305b3ef)

 **Synthesised Circuit**

 ![Screenshot from 2023-08-12 15-54-37](https://github.com/NSampathIIITB/Physical_Design_of_ASIC_IIIT-B/assets/141038460/4fccd840-41af-41f5-b0aa-e3e6c9de2d79)

 **d-flipflop with synchronous and asynchronbous reset**- Here the output **q** goes low whenever asynchronous reset is high where output doesn't depend on clock and also when synchronous reset is high and posedge of clock occurs.
 
 ![WhatsApp Image 2023-08-12 at 14 54 09](https://github.com/NSampathIIITB/Physical_Design_of_ASIC_IIIT-B/assets/141038460/25a33962-103e-4fb8-a536-aa17f1112693)

       module dff_asyncres_syncres ( input clk , input async_reset , input sync_reset , input d , output reg q );
		always @ (posedge clk , posedge async_reset)
		begin
			if(async_reset)
				q <= 1'b0;
			else if (sync_reset)
				q <= 1'b0;
			else	
				q <= d;
		end
	endmodule

 **Simulation**

 ![Screenshot from 2023-08-12 15-46-10](https://github.com/NSampathIIITB/Physical_Design_of_ASIC_IIIT-B/assets/141038460/b98c74b3-70f1-405c-a8fb-db3f39c47ee2)

 **Synthesized Circuit**

 ![Screenshot from 2023-08-12 15-56-53](https://github.com/NSampathIIITB/Physical_Design_of_ASIC_IIIT-B/assets/141038460/42dd1894-0691-430f-83d5-e3f566a50805)
 

 **Interesting Optimisations:**

 This lab session deals with some automatic and interesting optimisations of the circuits based on logic. In the below example, multiplying a number with 2 doesn't need any additional hardware  and only needs connecting the bits from **a** to **y** and grounding the LSB bit of y is enough and the same is realized by Yosys.

	module mul2 (input [2:0] a, output [3:0] y);
		assign y = a * 2;
	endmodule

 
 **Synthesized Circuit**

 ![Screenshot from 2023-08-12 16-23-45](https://github.com/NSampathIIITB/Physical_Design_of_ASIC_IIIT-B/assets/141038460/06e26061-f044-4abe-aeae-f58cbfffacc1)

 When it comes to multiplying with powers of 2, it just needs shifting as shown in the below image:

![WhatsApp Image 2023-08-12 at 17 00 07](https://github.com/NSampathIIITB/Physical_Design_of_ASIC_IIIT-B/assets/141038460/c4c34eb7-d6e5-498c-8969-74e36ae97584)

**Netlist for the above schematic**

![Screenshot from 2023-08-12 16-27-49](https://github.com/NSampathIIITB/Physical_Design_of_ASIC_IIIT-B/assets/141038460/a28761bc-ec9f-4657-80b4-4e54f74421be)

Special case of multiplying **a** with **9**. The result is shown in the below image:

![WhatsApp Image 2023-08-12 at 17 03 16](https://github.com/NSampathIIITB/Physical_Design_of_ASIC_IIIT-B/assets/141038460/1a74708c-5d36-41a0-8662-078ebaa836b7)

**Synthesized Circuit**

![Screenshot from 2023-08-12 16-29-57](https://github.com/NSampathIIITB/Physical_Design_of_ASIC_IIIT-B/assets/141038460/0abddba0-de17-4003-b66e-1a477173f17f)


**Netlist for the above schematic**

![Screenshot from 2023-08-12 16-31-15](https://github.com/NSampathIIITB/Physical_Design_of_ASIC_IIIT-B/assets/141038460/c1efa065-8026-49a4-bc0b-2128c75acc99)

</details>

## Day-3
<details>
<summary> Introduction to Logic Optimisation</summary>
	
Logic optimization in VLSI ASIC flow refers to the process of simplifying and reducing the complexity of a digital circuit design in order to improve its performance and reduce its power consumption. This is typically done by applying various techniques such as Boolean algebra, algebraic manipulation, and circuit simplification. The goal of logic optimization is to minimize the number of gates and transistors required to implement the circuit, while still maintaining its functionality. This can help to reduce the overall cost and power consumption of the ASIC, as well as improve its performance and reliability.

There are two types of logic optimisations</br>
1. Combinational logic optimisation</br>
2. Sequential logic optimisation</br>

</details>

<details>
<summary> Combinational Logic Optimisation</summary>

	
**Why Combinational logic Optimisation:**

 Combinational logic optimisation is mainly used to squeeze the logic to get the most optimised design .The most optimised design will be efficient interms of **area and power savings**. </br>

**Techniques used for combinational logic optimisation:** </br>

1. Constant Propogation which is Direct optimisation technique</br>
2. Boolean logic optimisation using K-maps or Quine McKluskey</br>

**Example of Combinational logic optimisation**

![WhatsApp Image 2023-08-12 at 21 14 18](https://github.com/NSampathIIITB/Physical_Design_of_ASIC_IIIT-B/assets/141038460/b7a076a0-187d-4594-bf1e-b14f5a2e0e0b)

In the above example, if we considor the trasnsistor level circuit of output Y, it has 6 MOS trasistors and when it changes to invertor, only 2 transistors will be sufficient. This is achieved by considering  A as contstant and propagating the same to output.

**Example of Boolean logic optimisation**

![WhatsApp Image 2023-08-12 at 21 20 05](https://github.com/NSampathIIITB/Physical_Design_of_ASIC_IIIT-B/assets/141038460/c44e057c-30e0-4cc9-a711-51277d2016ff)

Here we have considered an concurrent statement assign **y=a?(b?c:(c?a:0)):(!c)**

The above expression is using a ternary operator which realizes a series of multiplexers, however, when we write the boolean expression at outputs of each mux and simplify them further using boolean reduction techniques, the outout **y** turns out be just **~(a^c)**

Command to optimize the circuit by yosys is yosys> **opt_clean -purge**

**The following codes are optimised and the synthesis circuits are generated automatically.**

```
module opt_check (input a , input b , output y);
	assign y = a?b:0;
endmodule
```
![Screenshot from 2023-08-12 21-50-16](https://github.com/NSampathIIITB/Physical_Design_of_ASIC_IIIT-B/assets/141038460/57d79aef-7031-40bf-8451-1ad73a7f5e12)
<br>

```
module opt_check2 (input a , input b , output y);
	assign y = a?1:b;
endmodule
```
![Screenshot from 2023-08-12 21-51-41](https://github.com/NSampathIIITB/Physical_Design_of_ASIC_IIIT-B/assets/141038460/5e869f20-dcf6-4de5-bd12-6391d21eded7)
<br>

```
module opt_check3 (input a , input b, input c , output y);
	assign y = a?(c?b:0):0;
endmodule
```
![Screenshot from 2023-08-12 21-58-45](https://github.com/NSampathIIITB/Physical_Design_of_ASIC_IIIT-B/assets/141038460/f53ab41a-3a9c-42fc-9d7d-cb9e1a38af64)
<br>

```
module opt_check4 (input a , input b , input c , output y);
 assign y = a?(b?(a & c ):c):(!c);
endmodule
```
![Screenshot from 2023-08-12 21-59-55](https://github.com/NSampathIIITB/Physical_Design_of_ASIC_IIIT-B/assets/141038460/420c8e43-87ba-43d0-8b39-a8720e815fc6)
<br>
```
module sub_module1(input a , input b , output y);
		 assign y = a & b;
		endmodule

		module sub_module2(input a , input b , output y);
		 assign y = a^b;
		endmodule

		module multiple_module_opt(input a , input b , input c , input d , output y);
		wire n1,n2,n3;
		sub_module1 U1 (.a(a) , .b(1'b1) , .y(n1));
		sub_module2 U2 (.a(n1), .b(1'b0) , .y(n2));
		sub_module2 U3 (.a(b), .b(d) , .y(n3));

		assign y = c | (b & n1); 
		endmodule
```
**The below image shows flattened synthesis**
![Screenshot from 2023-08-12 22-08-08](https://github.com/NSampathIIITB/Physical_Design_of_ASIC_IIIT-B/assets/141038460/cbc98602-ac72-45a7-9145-0c9d2649b27c)
**The below image shows unflattened synthesis**
![Screenshot from 2023-08-12 22-12-48](https://github.com/NSampathIIITB/Physical_Design_of_ASIC_IIIT-B/assets/141038460/5941af78-fa10-445f-88d5-9fd651deef7a)
<br>
```
module sub_module(input a , input b , output y);
		assign y = a & b;
	endmodule

	module multiple_module_opt2(input a , input b , input c , input d , output y);
		wire n1,n2,n3;
		sub_module U1 (.a(a) , .b(1'b0) , .y(n1));
		sub_module U2 (.a(b), .b(c) , .y(n2));
		sub_module U3 (.a(n2), .b(d) , .y(n3));
		sub_module U4 (.a(n3), .b(n1) , .y(y));
	endmodule
 ```
**The below image shows flattened synthesis**
![Screenshot from 2023-08-12 22-14-46](https://github.com/NSampathIIITB/Physical_Design_of_ASIC_IIIT-B/assets/141038460/370af4ef-d1fb-4560-a455-a30ed50632eb)
**The below image shows unflattened synthesis**
![Screenshot from 2023-08-12 22-16-22](https://github.com/NSampathIIITB/Physical_Design_of_ASIC_IIIT-B/assets/141038460/191b9dab-485a-45ec-8f9e-73bef2fa67dd)

</details>

<details>
<summary> Sequential Logic Optimisation </summary>
	
Sequential logic optimization refers to the process of improving the performance, area utilization, power consumption, or other relevant metrics of a digital circuit that includes sequential logic elements. Sequential logic elements include flip-flops, registers, and other components that store information over time, as opposed to combinational logic elements which directly derive outputs from inputs without memory.</br>

Below are the various techniques used for sequential logic optimisations:<br />
-Basic
  - Sequential contant propagation
- Advanced
  - State optimisation
  - Retiming
  - Sequential Logic Cloning (Floor Plan Aware Synthesis)

**Sequential constant propogation:**

Sequential constant propagation is a technique used in digital circuit design and optimization to identify and propagate constant values through sequential logic elements. It aims to replace variables or signals with constant values when it can be determined that those variables will always have the same value at a given point in time during the circuit's operation.</br>

**Here is an example of sequential constant propogation**

![WhatsApp Image 2023-08-13 at 10 34 59](https://github.com/NSampathIIITB/Physical_Design_of_ASIC_IIIT-B/assets/141038460/5a379edc-e256-48a0-b61d-915800719c5c)

**State Optimisation:**

Reducing the number of states in a finite state machine (FSM) can lead to simpler and more efficient designs. This can involve merging equivalent states, removing redundant states, and optimizing state transitions.</br>

**Retiming:**

Retiming involves moving flip-flops within the circuit to improve the timing characteristics, such as reducing critical paths and achieving better clock distribution. This can lead to better overall performance and reduced power consumption.</br>

**Sequential logic cloning:**

Sequential logic cloning, also known as logic duplication, is a technique used in digital circuit design and optimization. It involves creating multiple copies of a portion of sequential logic within a circuit to achieve specific design goals, such as improving performance, meeting timing constraints, or reducing power consumption.

**The following codes are optimised and the synthesis circuits are generated automatically.**  <br>

```
module dff_const1(input clk, input reset, output reg q);
always @(posedge clk, posedge reset)
begin
	if(reset)
		q <= 1'b0;
	else
		q <= 1'b1;
end
endmodule
```
**Simulation**
Here flop will be inferred as the output is not constant.

![Screenshot from 2023-08-13 10-57-40](https://github.com/NSampathIIITB/Physical_Design_of_ASIC_IIIT-B/assets/141038460/e3848a13-6c3b-44a1-9bec-9532c1908075)

**Synthesized circuit**

![Screenshot from 2023-08-13 11-09-43](https://github.com/NSampathIIITB/Physical_Design_of_ASIC_IIIT-B/assets/141038460/9db322ab-4370-4679-8bb2-8a5babebff2e)
<br>
```
module dff_const2(input clk, input reset, output reg q);
always @(posedge clk, posedge reset)
begin
	if(reset)
		q <= 1'b1;
	else
		q <= 1'b1;
end
endmodule
```
**Simulation**
Here flop will not be inferred as the output is always high. 

![Screenshot from 2023-08-13 11-12-48](https://github.com/NSampathIIITB/Physical_Design_of_ASIC_IIIT-B/assets/141038460/71a83b57-d08d-414e-a783-b90735b0d79f)

**Synthesized circuit**

![Screenshot from 2023-08-13 11-14-32](https://github.com/NSampathIIITB/Physical_Design_of_ASIC_IIIT-B/assets/141038460/21a0ee1b-54ff-4306-8006-e2e9f44644ee)
<br>
```
module dff_const3(input clk, input reset, output reg q);
reg q1;
always @(posedge clk, posedge reset)
begin
	if(reset)
	begin
		q <= 1'b1;
		q1 <= 1'b0;
	end
	else
	begin
		q1 <= 1'b1;
		q <= q1;
	end
end
endmodule
```
**Simulation**

![Screenshot from 2023-08-13 11-23-29](https://github.com/NSampathIIITB/Physical_Design_of_ASIC_IIIT-B/assets/141038460/2b574f36-f8a3-4d45-aaac-d43e8647674c)

**Synthesized circuit**

![Screenshot from 2023-08-13 11-25-20](https://github.com/NSampathIIITB/Physical_Design_of_ASIC_IIIT-B/assets/141038460/b06416f0-0895-447c-85c3-1060b919f890)
<br>
```
module dff_const4(input clk, input reset, output reg q);
reg q1;
always @(posedge clk, posedge reset)
begin
	if(reset)
	begin
		q <= 1'b1;
		q1 <= 1'b1;
	end
	else
	begin
		q1 <= 1'b1;
		q <= q1;
	end
end
endmodule
```
**Simulation**

![Screenshot from 2023-08-13 11-29-52](https://github.com/NSampathIIITB/Physical_Design_of_ASIC_IIIT-B/assets/141038460/ad66e7b3-b6b0-4e35-a907-6910801473f6)

**Synthesized circuit**

![Screenshot from 2023-08-13 11-44-02](https://github.com/NSampathIIITB/Physical_Design_of_ASIC_IIIT-B/assets/141038460/052cd9b6-ded0-43d4-b4e0-a8f2f082a089)
<br>

```
module dff_const5(input clk, input reset, output reg q);
reg q1;
always @(posedge clk, posedge reset)
begin
	if(reset)
	begin
		q <= 1'b0;
		q1 <= 1'b0;
	end
	else
	begin
		q1 <= 1'b1;
		q <= q1;
	end
end
endmodule
```
**Simulation**

![Screenshot from 2023-08-13 11-46-19](https://github.com/NSampathIIITB/Physical_Design_of_ASIC_IIIT-B/assets/141038460/bf717e87-1832-4743-97ef-863c5840c774)

**Synthesized circuit**

![Screenshot from 2023-08-13 11-47-33](https://github.com/NSampathIIITB/Physical_Design_of_ASIC_IIIT-B/assets/141038460/67e344bd-662c-478a-a3ff-24de4fb3c997)
<br>

</details>

<details>
<summary> Sequential optimisation of Unused outputs </summary>
	
**Sequential optimization of unused outputs** refers to a design technique aimed at optimizing digital circuits by identifying and addressing unused or redundant output signals in sequential logic elements. Unused outputs can consume unnecessary resources, increase power consumption, and complicate the design without providing any functional benefit. By identifying and optimizing these outputs, designers can improve the overall efficiency of the circuit.</br>

**Example-1:**

```
module counter_opt (input clk , input reset , output q);
reg [2:0] count
assign q = count[0];
always @(posedge clk ,posedge reset)
begin
	if(reset)
		count <= 3'b000;
	else
		count <= count + 1;
end
endmodule
```
**Synthesized circuit:**

![Screenshot from 2023-08-13 12-25-38](https://github.com/NSampathIIITB/Physical_Design_of_ASIC_IIIT-B/assets/141038460/c60e2dd0-972f-4732-8445-68dd402efc82)

**Example-2**

```
module counter_opt (input clk , input reset , output q);
		reg [2:0] count;
		assign q = {count[2:0]==3'b100};
		always @(posedge clk ,posedge reset)
		begin
		if(reset)
			count <= 3'b000;
		else
			count <= count + 1;
		end
	endmodule

```
In this update counter logic we need to synthesize all the three flipflops</br>

**Synthesized circuit:**

![Screenshot from 2023-08-13 12-27-23](https://github.com/NSampathIIITB/Physical_Design_of_ASIC_IIIT-B/assets/141038460/a3d807f6-c9b4-4cfb-8ade-79378877cb57)
![Screenshot from 2023-08-13 12-28-14](https://github.com/NSampathIIITB/Physical_Design_of_ASIC_IIIT-B/assets/141038460/38ffe7f0-ac00-4063-ad49-bc73c0524b2a)

</details>

## Day-4
<details>
<summary>GLS, Synthesis-Simulation mismatch and Blocking, Non-blocking statements</summary>

### GLS Concepts And Flow Using Iverilog

**What is GLS- Gate Level Simulation?**:<br />
GLS is generating the simulation output by running test bench with netlist file generated from synthesis as design under test. Netlist is logically same as RTL code, therefore, same test bench can be used for it.

**Why GLS?**:<br />
We perform this to verify logical correctness of the design after synthesizing it. Also ensuring the timing of the design is met.

Below picture gives an insight of the procedure. Here while using iverilog, we also include gate level verilog models to generate GLS simulation.

![Screenshot (49)](https://user-images.githubusercontent.com/104454253/166256679-1ac9167a-1358-4c60-bbdb-0f6423f0faa3.png)</br>

To invoke GLS we use the command 
```
iverilog ../my_lib/verilog_model/primitives.v ../my_lib/verilog_model/sky130_fd_sc_hd.v example_net.v tb_example.v
```

### Synthesis-Simulation Mismatch

There are three main reasons for Synthesis Simulation Mismatch:<br />
- Missing sensitivity list in always block
- Blocking vs Non-Blocking Assignments
- Non standard Verilog coding

**Missing sensitivity list in always block:** </br>

If we consider **Example-2**, we can see the only **sel** is mentioned in the sensitivity list. During the simulation, the waveforms will resemble a latched output but the simulation of netlist will not infer this, as the synthesizer will only look at the statements with in the procedural block and not the sensitivity list.

As the synthesizer doen't look for sensitivity list and it looks only for the statements in procedural block or the functionality , it infers the correct circuit and if we simulate the netlist code, there will be a synthesis-simulation mismatch.

To avoid the synthesis and simulation mismatch. It is very important to check the behaviour of the circuit first and then match it with the expected output seen in simulation and make sure there are no synthesis and simulation mismatches. This is why we use GLS.

**Blocking vs Non-Blocking Assignments**:

Blocking and Non Blocking statements comes into the picture when we use **always block**.</br>

**Blocking statements:**

1. Inside the always block if we use "=" to make statements that is called a Blocking Statement.</br>
2. Blocking statements execute the statemetns in the order they are written inside the always block.Here the behaviour is like C-program.</br>

**Non-Blocking statements:**

1. Inside the always block if we use "=" to make statements that is called a Blocking Statement.</br>
2. Non-Blocking statements execute all the RHS and once always block is entered, the values are assigned to LHS.
3. Parallel or Concurrent execution.
  
Improper usage of blocking statements can create latches which inturn creates Simulation-Synthesis mismatch. Get to see at **Example-4**</br>

**NOTE:** Always write Non blocking statements for sequential circuits

</details>

<details>
	<summary> Lab-GLS Synthesis-Simulation Mismatch </summary>

 **Example-1** There is no mismatch in this example as the netlist simulation and RTL simulation waveform are similar only

	module ternary_operator_mux (input i0 , input i1 , input sel , output y);
		assign y = sel?i1:i0;
	endmodule
	
**Simulation**

![Screenshot from 2023-08-13 15-42-57](https://github.com/NSampathIIITB/Physical_Design_of_ASIC_IIIT-B/assets/141038460/5966ac9c-1045-4e92-993b-d07618aeded6)

**Synthesis**

![Screenshot from 2023-08-13 15-45-06](https://github.com/NSampathIIITB/Physical_Design_of_ASIC_IIIT-B/assets/141038460/a8157dad-d7d3-4020-9324-687ee1d1c27d)

**Netlist Simulation**

![Screenshot from 2023-08-13 15-55-53](https://github.com/NSampathIIITB/Physical_Design_of_ASIC_IIIT-B/assets/141038460/9f27aaaf-0ca7-4ade-a50d-e8efe5f32891)


**Example-2**

	module bad_mux (input i0 , input i1 , input sel , output reg y);
		always @ (sel)
		begin
			if(sel)
				y <= i1;
			else 
				y <= i0;
		end
	endmodule

**Simulation**

![Screenshot from 2023-08-13 15-59-41](https://github.com/NSampathIIITB/Physical_Design_of_ASIC_IIIT-B/assets/141038460/a3869c49-6207-454c-81df-9f1336f14bbb)

**Synthesis**

![Screenshot from 2023-08-13 16-02-56](https://github.com/NSampathIIITB/Physical_Design_of_ASIC_IIIT-B/assets/141038460/56bc83b7-6c5b-4a0d-8e1c-b060f204ff0e)

**Netlist Simulation**

![Screenshot from 2023-08-13 16-05-20](https://github.com/NSampathIIITB/Physical_Design_of_ASIC_IIIT-B/assets/141038460/7ea749ce-0b6a-410c-9db2-f1603cd3d1d2)

**MISMATCH**<br /> Here first pic shows the netlist simulation which corrects the bad_mux design which was only changing waveform when sel was triggered while for a mux to work properly it should be sensitivity to all the input signals.
![Screenshot from 2023-08-13 16-05-20](https://github.com/NSampathIIITB/Physical_Design_of_ASIC_IIIT-B/assets/141038460/ee1f3e74-415a-48a4-9576-9df8623fe4f8)
![Screenshot from 2023-08-13 15-59-41](https://github.com/NSampathIIITB/Physical_Design_of_ASIC_IIIT-B/assets/141038460/b7e54997-9fc4-4ead-b4f5-2a78acf1177d)




**Example-3**

	module good_mux (input i0 , input i1 , input sel , output reg y);
		always @ (*)
		begin
			if(sel)
				y <= i1;
			else 
				y <= i0;
		end
	endmodule
	
**Simulation**

![Screenshot from 2023-08-13 16-07-49](https://github.com/NSampathIIITB/Physical_Design_of_ASIC_IIIT-B/assets/141038460/a78d471d-b78b-4df4-981d-659edbb1d929)

**Synthesis**

![Screenshot from 2023-08-13 16-09-56](https://github.com/NSampathIIITB/Physical_Design_of_ASIC_IIIT-B/assets/141038460/307bd542-a44e-450c-b96a-d820694d586b)

**Netlist Simulation**

![Screenshot from 2023-08-13 16-11-41](https://github.com/NSampathIIITB/Physical_Design_of_ASIC_IIIT-B/assets/141038460/888607fa-dc97-4c60-b09d-dca8699c22f6)

</details>

<details>
<summary> Lab-Synthesis-Simulation mismatch blocking statement</summary>

 Here the output is depending on the past value of **x** which is dependednt on a and b and it appears like a **flop**.

**Example-4**

	module blocking_caveat (input a , input b , input  c, output reg d); 
	reg x;
	always @ (*)
		begin
		d = x & c;
		x = a | b;
	end
	endmodule

**Simulation**
![Screenshot from 2023-08-13 16-15-06](https://github.com/NSampathIIITB/Physical_Design_of_ASIC_IIIT-B/assets/141038460/b2c9a783-73d9-4a88-8c8e-aa81120a1f63)

**Synthesis**

![Screenshot from 2023-08-13 18-18-39](https://github.com/NSampathIIITB/Physical_Design_of_ASIC_IIIT-B/assets/141038460/73d54533-cd82-4acd-a23a-1546f16c90ab)

**Netlist Simulation**

![Screenshot from 2023-08-13 16-24-35](https://github.com/NSampathIIITB/Physical_Design_of_ASIC_IIIT-B/assets/141038460/37aedbef-3c25-4efd-9580-340af5379e58)

**MISMATCH** 
![Screenshot from 2023-08-13 18-22-36](https://github.com/NSampathIIITB/Physical_Design_of_ASIC_IIIT-B/assets/141038460/f66a05a0-3d5a-4122-85ee-69dc9348d8af)
![Screenshot from 2023-08-13 18-23-26](https://github.com/NSampathIIITB/Physical_Design_of_ASIC_IIIT-B/assets/141038460/9f7a9813-14df-4410-9e6d-5cbd2a0c1b1e)


Here this how the circuit should behave,but this correct waveform is only obtained while doing netlist simulation.</br>
Here first pic show the netlist simulation which shows the proper working of the DUT while the last pic shows the improper working of DUT as we have used blocking statement here which causes synthesis-simulation mismatch which is sorted out by GLS while providing netlist simulation  


</details>
	


## Day-5
<details>
	
</details>


 ## Acknowledgement
 
- Kunal Ghosh, VSD Corp. Pvt. Ltd.
- Skywater Foundry
- Alwin shaju,IIIT B
- DantuNandini,Senior,IIIT B
- Mariam Rakka
- chatgpt
  
## Reference 

- https://github.com/kunalg123
- https://github.com/kunalg123/sky130RTLDesignAndSynthesisWorkshop.git
- https://vsdiat.com
 
 

 
