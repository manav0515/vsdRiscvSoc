Task 1 – RISC-V Toolchain Setup & Uniqueness Test (VSD SoC Lab)

- This repository contains the setup steps, verification outputs, and code related to Task 1 of the **VSD RISC-V SoC Lab**. The task includes setting up the complete RISC-V GCC toolchain, building the Spike ISA simulator and Proxy Kernel, and validating the setup by compiling and running a uniqueness test program.

## What's Implemented

- Installed the RISC-V toolchain (`riscv64-unknown-elf-gcc`)
- Built and tested Spike (ISA simulator)
- Installed and verified Proxy Kernel (`pk`)
- Ran a C-based uniqueness test on `spike pk`
- Platform used: **Rocky Linux** (RHEL-based alternative to Ubuntu)

## Task 1 — Install base developer tools
`sudo apt-get update
sudo apt-get install -y git vim autoconf automake autotools-dev curl \
libmpc-dev libmpfr-dev libgmp-dev gawk build-essential bison flex \
texinfo gperf libtool patchutils bc zlib1g-dev libexpat1-dev gtkwave \
device-tree-compiler`
