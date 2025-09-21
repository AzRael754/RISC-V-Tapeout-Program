# My RISC-V Tapeout Program Journey 🚀

This repository documents my progress, learnings, and submissions for the RISC-V Tapeout Program.

---

## My Progress Log

<details>
<summary><h3>Day 0: Tools Installation</h3></summary>

As a Fedora user, I'm using a Distrobox container with an Ubuntu image to ensure compatibility with the required toolchain. This documents the installation of all required EDA tools.

#### 1. Setup the Ubuntu Container

First, I created and entered an Ubuntu container named `DevBox`.

```bash
# Create the container with a home directory in ~/Devel
distrobox create -n DevBox \
  --image ghcr.io/ublue-os/ubuntu-toolbox \
  --init \
  --home $HOME/Devel

# Enter the container shell
distrobox enter DevBox
```
![Distrobox Setup](assets/distrobox_setup.png)

#### 2. Yosys (Synthesis Tool)
Yosys is an open-source framework for Verilog RTL synthesis.

```bash
# Clone the repository
git clone [https://github.com/YosysHQ/yosys.git](https://github.com/YosysHQ/yosys.git)
cd yosys

# Install all required dependencies
sudo apt-get update
sudo apt-get install build-essential clang bison flex \
     libreadline-dev gawk tcl-dev libffi-dev git \
     graphviz xdot pkg-config python3 libboost-system-dev \
     libboost-python-dev libboost-filesystem-dev zlib1g-dev

# Compile and install Yosys
make
sudo make install
```
![Yosys Installation Complete](assets/yosys_install.png)

#### 3. Icarus Verilog (Simulation Tool)
Icarus Verilog (`iverilog`) is used for simulating the Verilog designs.

```bash
sudo apt-get install iverilog
```
![Iverilog Installed](assets/iverilog_version.png)

#### 4. GTKWave (Waveform Viewer)
GTKWave is used to visualize the simulation output (`.vcd` files).

```bash
sudo apt-get install gtkwave
```
![GTKWave Example](assets/gtkwave_example.png)

#### 5. ngspice (Circuit Simulator)
ngspice is an open-source spice simulator for circuit simulation.

```bash
# Download the tarball from [https://sourceforge.net/projects/ngspice/files/](https://sourceforge.net/projects/ngspice/files/)
# Assuming ngspice-37.tar.gz is in the current directory
tar -zxvf ngspice-*.tar.gz
cd ngspice-*
mkdir release
cd release
../configure --with-x --with-readline=yes --disable-debug
make
sudo make install
```
![ngspice Installed](assets/ngspice_install.png)

#### 6. Magic (VLSI Layout Tool)
Magic is a venerable VLSI layout tool.

```bash
# Install dependencies for Magic
sudo apt-get install m4 tcsh csh libx11-dev tcl-dev tk-dev \
     libcairo2-dev mesa-common-dev libglu1-mesa-dev libncurses-dev

# Clone, configure, and install
git clone [https://github.com/RTimothyEdwards/magic.git](https://github.com/RTimothyEdwards/magic.git)
cd magic
./configure
make
sudo make install
```
![Magic VLSI Layout Tool](assets/magic_install.png)

#### 7. OpenLane (RTL to GDSII Flow)
OpenLane is an automated RTL to GDSII flow based on several open-source EDA tools.
Since OpenLane is dockerized by default we will install it directly on our host fedora system,
but with podman instead of docker since its more secure

```bash
# Install Podman
sudo dnf update
sudo dnf install python3 python3-venv python3-pip make git
sudo dnf ca-certificates curl podman podman-docker

# podman-docker is a wrapper around podman to make it work like docker
# Test Docker installation
docker run hello-world

# Clone OpenLane and build the environment
cd $HOME
git clone --depth 1 https://github.com/The-OpenROAD-Project/OpenLane.git
cd OpenLane
make
# There was an error with the Makefile so had to update it with a commit hash
# Also we need the --privileged flag in docker options to run the container as root,
# Since podman by default runs it as user
# Test the OpenLane installation
make test
```
![OpenLane Installation Complete](assets/openlane_test.png)

</details>

---
