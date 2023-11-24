# VSD-HDP
VLSI SYSTEM DESIGN - HARDWARE DESIGN PROGRAM <br />
This repoitory includes the entire ASIC flow from RTL Design to GDSII along with RTL Verification, Logic Synthesis, Post synthesis STA Analysis, Floor Planning, Placement, CTS, Routing.<br />
**DAY 0** <br />
**1.** Creating GIT Hub repo.<br />
**2.** Tools Installation.<br />
For Tools Installation OS should be ubuntu 20.04LTS and set the Hardware requirements as 4GB RAM, 70GB HDD.<br />
## TOOLS TO BE INSTALLED:<br />
*__Yosys :__*<br />
```
$ git clone https://github.com/YosysHQ/yosys.git 
$ cd yosys 
$ sudo apt install make (If make is not installed please install it)  
$ sudo apt-get install build-essential clang bison flex \
    libreadline-dev gawk tcl-dev libffi-dev git \
    graphviz xdot pkg-config python3 libboost-system-dev \
    libboost-python-dev libboost-filesystem-dev zlib1g-dev ![yosys](https://github.com/Gowthami-GNS/vsd-hdp/assets/22699982/8f678c2e-68de-4a15-871f-b9e811962486)

$ make config-gcc 
$ make 
$ sudo make install
```
![yosys](https://github.com/Gowthami-GNS/vsd-hdp/assets/22699982/b2661fac-8bf2-4942-9c55-4d654406f7ea)

*__Iverilog :__*
It is a simulator tool used for simulating the design. <br />
```
sudo apt-get install iverilog
```
![iverilog](https://github.com/Gowthami-GNS/vsd-hdp/assets/22699982/2aaecd4f-99f5-496c-9c50-1d907e7b6b87)

*__gtkwave :__*
```
sudo apt update
sudo apt install gtkwave
```
![gtkwave](https://github.com/Gowthami-GNS/vsd-hdp/assets/22699982/9c534e35-ce37-40d9-ac63-26d537f0c6b5)

*__Open STA :__*
```
https://github.com/The-OpenROAD-Project/OpenSTA
```
*__ngspice :__*
```
After downloading the tarball from https://sourceforge.net/projects/ngspice/files/ to a local directory, unpack it using:
$ tar -zxvf ngspice-37.tar.gz
$ cd ngspice-37
$ mkdir release
$ cd release
$ ../configure  --with-x --with-readline=yes --disable-debug
$ make
$ sudo make install
```
![ngspice](https://github.com/Gowthami-GNS/vsd-hdp/assets/22699982/e0cb9ef1-e2e6-4227-8c52-bf6681414efb)

*__magic :__*
```
$   sudo apt-get install m4
$   sudo apt-get install tcsh
$   sudo apt-get install csh
$   sudo apt-get install libx11-dev
$   sudo apt-get install tcl-dev tk-dev
$   sudo apt-get install libcairo2-dev
$   sudo apt-get install mesa-common-dev libglu1-mesa-dev
$   sudo apt-get install libncurses-dev
git clone https://github.com/RTimothyEdwards/magic
cd magic
./configure
make
make install
```
*__OpenLane :__*
```
sudo apt-get update
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

# After reboot
docker run hello-world
```
## Dependencies
git --version <br />
docker --version <br />
python3 --version <br />
python3 -m pip --version <br />
make --version <br />
python3 -m venv -h <br />

## Steps to install PDKs and Tools
```
cd $HOME
git clone https://github.com/The-OpenROAD-Project/OpenLane
cd OpenLane
make
make test
```
**DAY 1** <br />
**1.** Introduction to Verilog RTL Design and Synthesis.<br />
**RTL Design** : RTL Design is checked for adherence to spec by simulating the design. The Design is a verilog code(or a set of verilog codes) which has the intended functionality to meet the requirements.<br />
**Test Bench** : Test bench is the setup to apply stimulus (test_vectors) to the design to check its functionality.<br />
**2.** Introduction to Open source Iverilog Simulator.<br />
Simulator looks for the changes on the input.<br />
***NOTE*** : **If no change in the input,no change in the output**. <br />
![iverilog simulation flow](https://github.com/Gowthami-GNS/vsd-hdp/assets/22699982/9946ed21-9aaa-4d89-9fcd-7d31fea3ff96)
**Lab 1 & Lab 2** : Implementing an example design 2x1 multiplexer using Iverilog and gtkwave.<br />
The Design and Testbench are the stimulus to the simulator which generates a vcd (value change dump) file as output. To obtain the waveform, this vcd file is processed by the gtkwave to verify the funcionality of the design.<br />
The design and sky130 library files are cloned from the below repository : <br >
<https://github.com/kunalg123/sky130RTLDesignAndSynthesisWorkshop.git> <br />
**syntax for iverilog and gtkwave**
```
iverilog good_mux.v tb_good_mux.v
./a.out //generates vcd file
gtkwave tb_good_mux.vcd
```
![gtkwave_2x1mux](https://github.com/Gowthami-GNS/vsd-hdp/assets/22699982/f342e2b9-d749-4697-8f70-88820541475b)
**3.** Introduction to Yosys and Logic Syntthesis.<br />
Yosys is a synthesis tool used for converting RTL to Netlist.<br />
![yosys](https://github.com/Gowthami-GNS/vsd-hdp/assets/22699982/34724562-77c9-4bf9-b084-d03fea33638c)
Synthesis is the process of mapping RTL and the standard cells present in the .lib into gate level netlist.<br />
read_verilog to read the verilog file, read_liberty to read the .lib and write_verilog to write the netlist.<br />
***NOTE*** : **Netlist is the representation of the design in standard cells**.<br />
**Lab 3** : Implementing an example design 2x1 multiplexer using Yosys and sky130 PDKs.<br />
```
Go to verilog_files folder cloned for doing Labs and invoke yosys there. <br />
In that repository we find the lib folder, where we find all the .lib files required for synthesis.<br />
yosys> read_liberty -lib <lib_path> <filename> <br />
yosys> read_verilog good_mux.v <br />
yosys> synth -top <top_module>. //This indicates which module we are synthesizing.<br />
yosys> abc -liberty <lib_path> <filename>. //Command used to generate the netliist.<br />
It also gives you report on what are the cells that are inferrred.
yosys> show //Graphical representation of logic realised.
yosys> write_verilog -noattr good_mux_netlist.v //Command to write netlist <br />
/* Generated by Yosys 0.34+55 (git sha1 672375ed0, gcc 9.4.0-1ubuntu1~20.04.2 -fPIC -Os) */
module good_mux(i0, i1, sel, y);
  wire _0_;
  wire _1_;
  wire _2_;
  wire _3_;
  input i0;
  wire i0;
  input i1;
  wire i1;
  input sel;
  wire sel;
  output y;
  wire y;
  sky130_fd_sc_hd__mux2_1 _4_ (
    .A0(_0_),
    .A1(_1_),
    .S(_2_),
    .X(_3_)
  );
  assign _0_ = i0;
  assign _1_ = i1;
  assign _2_ = sel;
  assign y = _3_;
endmodule
```
![yosys_commands](https://github.com/Gowthami-GNS/vsd-hdp/assets/22699982/d072a3c3-b998-4983-9307-5609e74a2e93)
![abc](https://github.com/Gowthami-GNS/vsd-hdp/assets/22699982/0b18202b-08b9-4b92-ac4b-809fddba8b74)
![cellsinferred](https://github.com/Gowthami-GNS/vsd-hdp/assets/22699982/4c38efc4-3687-41c9-a731-03cdcdc95099)
![netlist](https://github.com/Gowthami-GNS/vsd-hdp/assets/22699982/9ddec4ca-a2e7-4905-b92c-bed2a7171813)

**DAY 2** : Timing libs, hierarchial vs flat synthesis and effecient flop coding styles.<br />
**1.** Introduction to Timing.libs <br />
**Lab 4** : Introduction to dot lib
The library file used for this project is "sky130_fd_sc_hd__tt_025c_1v80".//sky130 indicates the name of the library, tt indicates the process (typical), 025c indicates temperature and 1v80 indicates voltage .<br />
```
operating_conditions ("tt_025C_1v80") {
        voltage : 1.8000000000;
        process : 1.0000000000;
        temperature : 25.000000000;
```
**Lab 5.** Hierarchial vs Flat Synthesis using multiple modules example <br />
write_verilog noattr multiple_modules_hier.v <br />
flatten is the command to write flat netlist.<br />
write_verilog noattr multiple_modules_flat.v <br />
**Hierarchial synthesis vs Flat synthesis**: <br />
In Hierarchial synthesis, hierarchy is preserved. <br />
![hiervsflat](https://github.com/Gowthami-GNS/vsd-hdp/assets/22699982/cc9b6566-a0fb-4653-a2dc-17278106a1c3)
Hierarchial synthesis: <br />
![hier_net](https://github.com/Gowthami-GNS/vsd-hdp/assets/22699982/853c5316-1a84-46b0-872b-bec45e2495c5)
![submodule1](https://github.com/Gowthami-GNS/vsd-hdp/assets/22699982/32761861-e0d4-4883-a71c-92fc5e3a3131)     ![submodule2](https://github.com/Gowthami-GNS/vsd-hdp/assets/22699982/2e17e4b1-79fd-4c53-9cb8-62fc60e457c8)

Flat synthesis: <br />
![flatnet](https://github.com/Gowthami-GNS/vsd-hdp/assets/22699982/1e51d2c8-0631-4243-9b2e-24ed95b6bf86)
To synthesis any submodule we give synth -top <module_name> <br />
**2.** : **Various Flop coding styles and optimization**.<br />
Flops are the storage elements introdued in between combnational ciruits to avoid the propagation og glitches. <br />
Asynchronous reset : The reset is independant of clock. <br />
***Verilog code of D Flipflop with async reset, simulation and synthesis***:
```
module dff_asyncres ( input clk ,  input async_reset , input d , output reg q );
always @ (posedge clk , posedge async_reset)
begin
        if(async_reset)
                q <= 1'b0;
        else
                q <= d;
end
endmodule

Simulation:
iverilog dff_asyncres.v tb_dff_asyncres.v
./a.out
gtkwave tb_dff_asyncres.vcd
```
![dff_asyncres_simulation](https://github.com/Gowthami-GNS/vsd-hdp/assets/22699982/526f6001-5c47-410a-96af-c770886b1ea2)
![asyncre_netlist](https://github.com/Gowthami-GNS/vsd-hdp/assets/22699982/997fb421-75fe-486d-8bcf-93b070dee073)

Synchronous reset : The reset is awaiting the clock edge.
***Verilog code of D Flipflop with sync reset,simulation and synthesis***:
```
module dff_syncres ( input clk , input async_reset , input sync_reset , input d , output reg q );
always @ (posedge clk )
begin
        if (sync_reset)
                q <= 1'b0;
        else
                q <= d;
end
endmodule
Simulation:
iverilog dff_syncres.v tb_dff_syncres.v
./a.out
gtkwave tb_dff_syncres.vcd
```
![dff_syncres_simlt](https://github.com/Gowthami-GNS/vsd-hdp/assets/22699982/5c7ecf72-c4a0-4e27-b0dd-5786e369f570)
![syncres_netlist](https://github.com/Gowthami-GNS/vsd-hdp/assets/22699982/249adcd3-bd0b-49eb-86cb-f68f4a88c380)

***Verilog code of D Flipflop with async and sync reset, simulaion and synthesis***:
```
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
Simulation:
iverilog dff_asyncres_syncres.v tb_dff_asyncres_syncres.v
./a.out
gtkwave tb_dff_asyncres_syncres.vcd
```
![dff_async_sync_simul](https://github.com/Gowthami-GNS/vsd-hdp/assets/22699982/10be1146-7b02-483a-b509-38744dc3fbaa)
![asyncres_syncres_netlist](https://github.com/Gowthami-GNS/vsd-hdp/assets/22699982/f56f4c79-7b00-4907-b668-82cc92dfc3d3)

***Verilog code for mult2***:
```
module mul2 (input [2:0] a, output [3:0] y);
        assign y = a * 2;
endmodule

Netlist:
/* Generated by Yosys 0.34+55 (git sha1 672375ed0, gcc 9.4.0-1ubuntu1~20.04.2 -fPIC -Os) */
module mul2(a, y);
  input [2:0] a;
  wire [2:0] a;
  output [3:0] y;
  wire [3:0] y;
  assign y = { a, 1'h0 };
endmodule
```
![mult2_netlist](https://github.com/Gowthami-GNS/vsd-hdp/assets/22699982/9a8f8fb1-7b46-40ec-8539-2849d580dbb2)

***Verilog code for mult8***:
```
module mult8 (input [2:0] a , output [5:0] y);
        assign y = a * 9;
endmodule

Netlist:
/* Generated by Yosys 0.34+55 (git sha1 672375ed0, gcc 9.4.0-1ubuntu1~20.04.2 -fPIC -Os) */
module mult8(a, y);
  input [2:0] a;
  wire [2:0] a;
  output [5:0] y;
  wire [5:0] y;
  assign y = { a, a };
endmodule
```
![mult8_netlist](https://github.com/Gowthami-GNS/vsd-hdp/assets/22699982/e4bac068-b8c6-4ba7-a14c-afc5902c0532)

**DAY 3**: Combinational and sequential optimizations.<br />
**Combinational logic optimization** : is the squeezing the logic to get the most optimized design in terms of Area and Power savings. It is of two types.<br />
1. Constant proagaton (Direct propagation). <br />
2. Boolean Logic Optimization. <br />
**Sequential logic optimizations** : are of 2 types: <br />
1. Basic - Sequential constant Propagation : constant value is propagated throghout the flop. <br /> 
2. Advanced - State Optimization, Retiming, Sequential logic cloning. <br />

**Lab 06** : Combinational Logic optimzations <br />
1. **opt_check.v** : <br />
```
module opt_check (input a , input b , output y);
        assign y = a?b:0;
endmodule

Synthesis :
yosys> read_liberty -lib <lib_path> <filename> <br />
yosys> read_verilog good_mux.v <br />
yosys> synth -top <top_module>. //This indicates which module we are synthesizing.<br />
yosys> opt_clean -purge //command used for constant propagation and other optimization techniques. <br />
yosys> abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
```
![opt_check](https://github.com/Gowthami-GNS/vsd-hdp/assets/22699982/03ab584f-f244-4c82-913b-f32aabba5b64)

2. **opt_check2.v** : <br />
```
module opt_check2 (input a , input b , output y);
        assign y = a?1:b;
endmodule
```
![opt_check2](https://github.com/Gowthami-GNS/vsd-hdp/assets/22699982/84520072-dd59-4f23-aa7f-7beaaa2496ee)

3. **opt_check3.v** : <br />
```
module opt_check3 (input a , input b, input c , output y);
        assign y = a?(c?b:0):0;
endmodule
```
![opt3](https://github.com/Gowthami-GNS/vsd-hdp/assets/22699982/ae2ee7af-869f-416d-95a2-51bf76277be4)

4. **opt_check4.v** : <br />
```
module opt_check4 (input a , input b , input c , output y);
 assign y = a?(b?(a & c ):c):(!c);
 endmodule
```
![opt4](https://github.com/Gowthami-GNS/vsd-hdp/assets/22699982/d5ccafba-344a-48e6-b23e-f36f8e5d5f15)

5. **multiple_module_opt.v** : <br />
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

synthesis:
yosys> read_liberty -lib <lib_path> <filename> <br />
yosys> read_verilog mutilple_module_opt.v <br />
yosys> synth -top <top_module>. //This indicates which module we are synthesizing.<br />
yosys> flatten
yosys> write_verilog mutilple_module_opt_flat.v
yosys> opt_clean -purge //command used for constant propagation and other optimization techniques. <br />
yosys> abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
```
![mm](https://github.com/Gowthami-GNS/vsd-hdp/assets/22699982/2700ef06-a3be-4308-ab91-c34da7b7674c)

6. **multiple_module_opt2.v** <br />
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
![mmo2](https://github.com/Gowthami-GNS/vsd-hdp/assets/22699982/cdb3630c-51e3-431e-a46c-6249f662e042)

**Lab 07**: **Sequential logic optimization**. <br />
1. **dff_const1.v**: <br />
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

synthesis:
yosys> read_liberty -lib <lib_path> <filename> <br />
yosys> read_verilog dff_const1.v <br />
yosys> synth -top <top_module>. //This indicates which module we are synthesizing.<br />
yosys> dfflibmap -liberty <lib_path> <filename> //For seq ckts only. <br />
yosys> abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
yosys> show
```
![dffc1](https://github.com/Gowthami-GNS/vsd-hdp/assets/22699982/54a08461-2100-4a44-aed3-99f913e7bc0e)
![dff_c1](https://github.com/Gowthami-GNS/vsd-hdp/assets/22699982/383c4c62-26a0-4e49-a053-9745eaeadf9c)

2. **dff_const2.v**: <br />
```                                                                                                                          1,1            All
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
![dffc2](https://github.com/Gowthami-GNS/vsd-hdp/assets/22699982/f2ae1c06-83d0-4c79-8d52-84616049cc7a)
![dff_c2](https://github.com/Gowthami-GNS/vsd-hdp/assets/22699982/642e79bc-ac97-4a3f-97f9-8ecaef405c09)

3. **dff_const3.v** : <br />
```module dff_const3(input clk, input reset, output reg q);
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
![dffc3](https://github.com/Gowthami-GNS/vsd-hdp/assets/22699982/a1caf486-44eb-4f66-8e8c-3befd1378f1e)
![dff_c3](https://github.com/Gowthami-GNS/vsd-hdp/assets/22699982/80b18898-a432-49ac-9691-1c41c2920f0a)

4. **dff_const4.v** : <br />
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
![dffc4](https://github.com/Gowthami-GNS/vsd-hdp/assets/22699982/70035dab-1bc2-42c2-8969-7edf5b505ec3)
![dff_c4](https://github.com/Gowthami-GNS/vsd-hdp/assets/22699982/58a7a60b-0dd1-48de-a773-d2f4320f56eb)

5. **dff_const5.v** : <br />
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
![dffc5](https://github.com/Gowthami-GNS/vsd-hdp/assets/22699982/1b496891-5e79-4591-92d5-7ed7fca523ec)
![dff_c5](https://github.com/Gowthami-GNS/vsd-hdp/assets/22699982/5e7bf6b9-c80f-4c09-8d7d-a11068690410)

**Sequential optimization for unused outputs** :
Ex: 1. counter_opt.v <br />
```
module counter_opt (input clk , input reset , output q);
reg [2:0] count;
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
![count_opt](https://github.com/Gowthami-GNS/vsd-hdp/assets/22699982/1569f8e4-38f3-4e27-a6f6-a189ecff151e)

2. counter_opt2.v <br />
```
module counter_opt (input clk , input reset , output q);
reg [2:0] count;
assign q = (count[2:0] == 3'b100);

always @(posedge clk ,posedge reset)
begin
        if(reset)
                count <= 3'b000;
        else
                count <= count + 1;
end
endmodule
```
![c_opt2](https://github.com/Gowthami-GNS/vsd-hdp/assets/22699982/577cfd3d-6278-4129-8644-d4f9cb468cab)

**Day 4** : GLS, blocking vs non-blocking and synthesis-simulation mismatch <br />
***GLS (Gate leve Simulation)*** : Running the testbench with netlist as Design under test. We run GLS to verify the correctness of design after synthesis and also to ensure that the timing of the design is met. <br />
**GLS using iverilog**: <br />
![gls](https://github.com/Gowthami-GNS/vsd-hdp/assets/22699982/50d0ff86-f82e-447b-81a2-fad675d9e319)

***Synthesis - Siualtion mismatch*** : can happen because of missing sensitivity list, blocking vs non blocking assignments, non standard verilog coding. <br />
**Lab** : ****ternary_operator_mux.v***
```
module ternary_operator_mux (input i0 , input i1 , input sel , output y);
	assign y = sel?i1:i0;
endmodule

simulation:
iverilog <file_name>.v <tb_filename>.v <br />
./a.out <br />
gtkwave <tb_filename>.vcd <br />

synthesis:
yosys> read_liberty -lib <lib_path> <filename> <br />
yosys> read_verilog ternary_opertor_mux.v <br />
yosys> synth -top <top_module>. //This indicates which module we are synthesizing.<br />
yosys> abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib <br />
yosys> write_verilog -noattr ternary_opertor_mux_net.v <br />
yosys> show <br />

GLS:
iverilog ../my_lib/verilog_model/primitives.v ../my_lib/verilog_model/sky130_fd_sc_hd.v ternary_operator_mux_net.v tb_ternary_operator_mux.v <br />
./a.out
gtkwave tb_ternary_operator_mux.vcd <br />
```
![tom](https://github.com/Gowthami-GNS/vsd-hdp/assets/22699982/ecb0b69f-dbf0-4ed3-9450-2fa6e25d0e73)
![toms](https://github.com/Gowthami-GNS/vsd-hdp/assets/22699982/762e9473-5b9c-4940-aa5f-a4b616fa93c4)
![glstom](https://github.com/Gowthami-GNS/vsd-hdp/assets/22699982/47303f98-4dbd-4952-bd05-c9a15a723287)

***bad_mux.v***
```
module bad_mux (input i0 , input i1 , input sel , output reg y);
always @ (sel)
begin
	if(sel)
		y <= i1;
	else 
		y <= i0;
end
endmodule
```
![badmussimul](https://github.com/Gowthami-GNS/vsd-hdp/assets/22699982/017fcae7-6728-4a80-9de1-c703d8031081)
![badmux](https://github.com/Gowthami-GNS/vsd-hdp/assets/22699982/7a0138ca-5120-4631-8f7a-18b452a40b02)
![badmuxgls](https://github.com/Gowthami-GNS/vsd-hdp/assets/22699982/05aa30ff-cdb9-488b-8bec-508076907a58)

***blocking_caveat.v*** : synthesis - simulation mismatch is due to blocking statement. <br />
```
module blocking_caveat (input a , input b , input  c, output reg d); 
reg x;
always @ (*)
begin
	d = x & c;
	x = a | b;
end
endmodule
```
![blocking](https://github.com/Gowthami-GNS/vsd-hdp/assets/22699982/bc0e4416-c6c7-43af-ae6e-0b756f50449f)
![bc](https://github.com/Gowthami-GNS/vsd-hdp/assets/22699982/6017005e-c09b-4927-b0ae-cc005e436461)
![bcgls](https://github.com/Gowthami-GNS/vsd-hdp/assets/22699982/32371e6f-276a-4d41-96a1-3c2c912f2302)








        




                                                                                                                                                                        1,1           Top














