[RISC-V TASK 1.pdf](https://github.com/user-attachments/files/21560845/RISC-V.TASK.1.pdf)
# Task 1 – RISC-V Toolchain Setup & Uniqueness Test (VSD SoC Lab) #

- This repository contains the setup steps, verification outputs, and code related to Task 1 of the **VSD RISC-V SoC Lab**. The task includes setting up the complete RISC-V GCC toolchain, building the Spike ISA simulator and Proxy Kernel, and validating the setup by compiling and running a uniqueness test program.

## What's Implemented

- Installed the RISC-V toolchain (`riscv64-unknown-elf-gcc`)
- Built and tested Spike (ISA simulator)
- Installed and verified Proxy Kernel (`pk`)
- Ran a C-based uniqueness test on `spike pk`
- Platform used: **Rocky Linux** (RHEL-based alternative to Ubuntu)

## Table Of Content: -
```
Task 1 — Install base developer tools
Task 2 — Create a clean workspace and capture your home path
Task 3 — Get a prebuilt RISC‑V GCC toolchain
Task 4 — Add toolchain to your PATH (current shell + persistent)
Task 5 — Install Device Tree Compiler (DTC)
Task 6 — Build and install Spike (RISC‑V ISA simulator)
Task 7 — Build and install the RISC‑V Proxy Kernel (riscv-pk)
Task 8 — Ensure the cross bin directory is in PATH
Task 9 — Install Icarus Verilog
Task 10 — Quick sanity checks
Create unique_test.c
Compile with injected identity and RISC‑V flags
Run on Spike with the proxy kernel
Final Expected Output
Conclusion
```

Results: -
Source file: - unique_test.c .
The exact compile command used .
The program output from spike pk ./unique_test .

### Task 1 — Install base developer tools
```
sudo apt-get install -y git vim autoconf automake autotools-dev curl \
libmpc-dev libmpfr-dev libgmp-dev gawk build-essential bison flex \
texinfo gperf libtool patchutils bc zlib1g-dev libexpat1-dev gtkwave
```


### Task 2 — Create a clean workspace and capture your home path
```
cd
pwd=$PWD
mkdir -p riscv_toolchain
cd riscv_toolchain
```

### Task 3 — Get a prebuilt RISC‑V GCC toolchain
```
Wget "https://static.dev.sifive.com/dev-tools/riscv64-unknown-elf-gcc-8.3.0-2019.08.0-x86_64-linux-ubuntu14.tar.gz" 
tar -xvzf riscv64-unknown-elf-gcc-8.3.0-2019.08.0-x86_64-linux-ubuntu14.tar.gz
ls -la
ls -la riscv64-unknown-elf-gcc-8.3.0-2019.08.0-x86_64-linux-ubuntu14.tar.gz
```
<img width="1199" height="271" alt="Screenshot from 2025-08-02 19-50-05" src="https://github.com/user-attachments/assets/82bbdd4c-f943-4be9-8baf-ba0976f7ad13" />



### Task 4 — Add toolchain to your PATH (current shell + persistent)

#### Command (current shell): -
```
export PATH=$pwd/riscv_toolchain/riscv64-unknown-elf-gcc-8.3.0-2019.08.0-x86_64-linux-ubuntu14/bin:$PATH
```
#### Command (persistent for new terminals): -
```
echo 'export PATH=$HOME/riscv_toolchain/riscv64-unknown-elf-gcc-8.3.0-2019.08.0-x86_64-linux-ubuntu14/bin:$PATH' >> ~/.bashrc
echo $PATH | grep riscv
```
<img width="1199" height="273" alt="Screenshot from 2025-08-02 20-09-56" src="https://github.com/user-attachments/assets/b9855f62-0660-4843-b828-34ee770553c8" />


#### If error pops up similar to: -
```
riscv64-unknown-elf-gdb: error while loading shared libraries: libncurses.so.5: cannot open shared object file: No such file or directory
```
#### Run the following command: -
```
# Install the legacy packages manually:
cd /tmp
wget http://archive.ubuntu.com/ubuntu/pool/universe/n/ncurses/libtinfo5_6.3-2ubuntu0.1_amd64.deb
wget http://archive.ubuntu.com/ubuntu/pool/universe/n/ncurses/libncurses5_6.3-2ubuntu0.1_amd64.deb
sudo dpkg -i libtinfo5_6.3-2ubuntu0.1_amd64.deb
sudo dpkg -i libncurses5_6.3-2ubuntu0.1_amd64.deb
# Find where libraries were installed:
find /usr -name "libncurses.so.5*" 2>/dev/null
find /usr -name "libtinfo.so.5*" 2>/dev/null
```
<img width="1199" height="726" alt="Screenshot from 2025-08-02 20-10-24" src="https://github.com/user-attachments/assets/2b3662ef-2039-478e-9060-7dbf060b2dd0" />

### Task 5 — Install Device Tree Compiler (DTC)
```
sudo apt-get install -y device-tree-compiler
```

### Task 6 — Build and install Spike (RISC‑V ISA simulator)
```
git clone https://github.com/riscv/riscv-isa-sim.git
cd riscv-isa-sim
mkdir -p build && cd build
../configure --prefix=$pwd/riscv_toolchain/riscv64-unknown-elf-gcc-8.3.0-2019.08.0-x86_64-linux-ubuntu14
make -j$(nproc)
sudo make install
cd $pwd/riscv_toolchain
```


### Task 7 — Build and install the RISC‑V Proxy Kernel (riscv-pk)
```
cd $pwd/riscv_toolchain
git clone https://github.com/riscv/riscv-pk.git
cd riscv-pk
mkdir -p build && cd build
../configure --prefix=$pwd/riscv_toolchain/riscv64-unknown-elf-gcc8.3.0-2019.08.0-x86_64-linux-ubuntu14 --host=riscv64-unknown-elf
make -j$(nproc)
sudo make install
```

### Task 8 — Ensure the cross bin directory is in PATH
#### Command (current shell): -
```
export PATH=$pwd/riscv_toolchain/riscv64-unknown-elf-gcc-8.3.0-
2019.08.0-x86_64-linux-ubuntu14/riscv64-unknown-elf/bin:$PATH
```
#### Command (persistent): -
```
echo 'export PATH=$HOME/riscv_toolchain/riscv64-unknown-elf-gcc-8.3.0-
2019.08.0-x86_64-linux-ubuntu14/riscv64-unknown-elf/bin:$PATH' >>
~/.bashrc
source ~/.bashrc
```
### Task 9 — (Optional) Install Icarus Verilog
```
cd $pwd/riscv_toolchain
git clone https://github.com/steveicarus/iverilog.git
cd iverilog
git checkout --track -b v10-branch origin/v10-branch
git pull
chmod +x autoconf.sh
./autoconf.sh
./configure
make -j$(nproc)
sudo make install
Task 10 — Quick sanity checks
which riscv64-unknown-elf-gcc
riscv64-unknown-elf-gcc -v
which spike
spike --version || spike -h
which pk
```
<img width="1198" height="770" alt="Screenshot from 2025-08-02 23-18-54" src="https://github.com/user-attachments/assets/32d5f734-a3c2-461d-8d33-9e40a905e36b" />

<img width="1198" height="770" alt="Screenshot from 2025-08-02 23-19-05" src="https://github.com/user-attachments/assets/28801abd-c406-46bc-9dd1-efcf2a466953" />

## Final Deliverable: - A Unique C Test (Username & Machine Dependent)
#### (Note: - Create in "riscv_toolchain" not in "iverilog")
### 1) Create unique_test.c
```
#include <stdint.h>
#include <stdio.h>
#ifndef USERNAME
#define USERNAME "unknown_user"
#endif
#ifndef HOSTNAME
#define HOSTNAME "unknown_host"
#endif
// 64-bit FNV-1a
static uint64_t fnv1a64(const char *s) {
const uint64_t FNV_OFFSET = 1469598103934665603ULL;
const uint64_t FNV_PRIME = 1099511628211ULL;
uint64_t h = FNV_OFFSET;
for (const unsigned char *p = (const unsigned char*)s; *p; ++p) {
h ^= (uint64_t)(*p);
h *= FNV_PRIME;
}
return h;
}
int main(void) {
const char *user = USERNAME;
const char *host = HOSTNAME;
char buf[256];
int n = snprintf(buf, sizeof(buf), "%s@%s", user, host);
if (n <= 0) return 1;
uint64_t uid = fnv1a64(buf);
printf("RISC-V Uniqueness Check\n");
printf("User: %s\n", user);
printf("Host: %s\n", host);
printf("UniqueID: 0x%016llx\n", (unsigned long long)uid);
#ifdef __VERSION__
unsigned long long vlen = (unsigned long long)sizeof(__VERSION__) -
1;
printf("GCC_VLEN: %llu\n", vlen);
#endif
return 0;
}
```

<img width="1198" height="770" alt="Screenshot from 2025-08-02 23-39-48" src="https://github.com/user-attachments/assets/7718d5b0-0f0a-4da0-9b3d-6dd1d434f225" />

### 2) Compile with injected identity and RISC‑V flags

#### Username and Hostname from the machine.
```
echo "Username: '$(id -un)'"
echo "Hostname: '$(hostname -s)'"
```
<img width="702" height="93" alt="Screenshot from 2025-08-02 20-39-01" src="https://github.com/user-attachments/assets/7cea11c9-e6c1-47ff-b4e1-8d3376bcea52" />

#### Compile Command: -
```
64-unknown-elf-gcc -O2 -Wall -march=rv64imac -mabi=lp64 \
-DUSERNAME='"root"' -DHOSTNAME='"Manav"' \
unique_test.c -o unique_test
```
<img width="836" height="72" alt="Screenshot from 2025-08-02 20-48-44 (1)" src="https://github.com/user-attachments/assets/a6a83044-ce74-44e8-bb40-f6b74ed6c6b1" />

### 3) Run on Spike with the proxy kernel
```
spike pk ./unique_test
```
## Output: -

<img width="633" height="129" alt="Screenshot from 2025-08-02 20-48-44" src="https://github.com/user-attachments/assets/c12f7949-41a2-43ab-82c8-ddfbe0e8157f" />

 ## Conclusion: -
This task helped me understand the full flow of bare-metal RISC-V development — from setting up the toolchain to running compiled programs on an ISA simulator. Successfully building and testing the toolchain on Rocky Linux also gave me deeper confidence with open-source hardware workflows and Linux-based development environments.
This setup forms the foundation for further phases of the VSD SoC Lab, including RTL simulation, synthesis, and SoC-level integration.




