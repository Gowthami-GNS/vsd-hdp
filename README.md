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
**Hierarchial synthesis vs Flat synthesis**:
In Hierarchial synthesis, hierarchy is preserved.
![hiervsflat](https://github.com/Gowthami-GNS/vsd-hdp/assets/22699982/cc9b6566-a0fb-4653-a2dc-17278106a1c3)
Hierarchial synthesis:
![hier_net](https://github.com/Gowthami-GNS/vsd-hdp/assets/22699982/853c5316-1a84-46b0-872b-bec45e2495c5)
Flat synthesis:
![flatnet](https://github.com/Gowthami-GNS/vsd-hdp/assets/22699982/1e51d2c8-0631-4243-9b2e-24ed95b6bf86)
To synthesis any submodule we give synth -top <module_name>
**2.** : Various Flat coding styles and optimization.<br />




                                                                                                                                                                        1,1           Top














