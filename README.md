# VSD-HDP
VLSI SYSTEM DESIGN - HARDWARE DESIGN PROGRAM <br />
This repoitory includes the entire ASIC flow from RTL Design, RTL Verification, Logic Synthesis, Post synthesis STA Analysis, Floor Planning, Placement, CTS, Routing.<br />
**DAY 0** : Created GIT Hub repo.<br />
**DAY 1** : Tools Installation.<br />
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
    libboost-python-dev libboost-filesystem-dev zlib1g-dev 
$ make config-gcc 
$ make 
$ sudo make install
```





