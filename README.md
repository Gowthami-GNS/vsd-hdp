# VSD-HDP
VLSI SYSTEM DESIGN - HARDWARE DESIGN PROGRAM <br />
This repoitory includes the entire ASIC flow from RTL Design to GDSII along with RTL Verification, Logic Synthesis, Post synthesis STA Analysis, Floor Planning, Placement, CTS, Routing.<br />
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
    libboost-python-dev libboost-filesystem-dev zlib1g-dev ![yosys](https://github.com/Gowthami-GNS/vsd-hdp/assets/22699982/8f678c2e-68de-4a15-871f-b9e811962486)

$ make config-gcc 
$ make 
$ sudo make install
```
![yosys](https://github.com/Gowthami-GNS/vsd-hdp/assets/22699982/b2661fac-8bf2-4942-9c55-4d654406f7ea)

*__Iverilog :__*
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







