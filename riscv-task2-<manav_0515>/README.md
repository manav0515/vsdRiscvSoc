# Task 2 — Proving RISC-V Toolchain Setup (Run, Disassemble, Decode)

## This repository is part of the VSD RISC-V SoC Workshop. In Task 2, the goal is to prove that the RISC-V toolchain is correctly installed and functional on the local machine.

## The following steps were performed: -
- Compiled 4 unique C programs using `riscv64-unknown-elf-gcc`
- Embedded user, host, machine ID, and timestamps for build uniqueness
- Ran each program on the RISC-V simulator (`spike pk`)
- Captured disassembly (`.objdump`) and source-level assembly (`.s`) of each
- Manually decoded at least 5 RISC-V integer instructions
- Documented all outputs, binaries, and screenshots as evidence

## Toolchain Verification

### Spike Version
#### Output of ``` spike -version ```
#### (Note: - ``` spike --help | head -1 ``` used instead of ``` spike -version```)
<img width="752" height="49" alt="spike -version" src="https://github.com/user-attachments/assets/cdea4e35-a52f-4033-ba04-b613a1fffade" />

### riscv64-unknown-elf-gcc -v
#### Output of ``` riscv64-unknown-elf-gcc -v ```
<img width="1198" height="327" alt="riscv64-unknown-elf-gcc -v" src="https://github.com/user-attachments/assets/dde55d4a-0067-46ab-bd9c-cf863f78bdfb" />

### Compile Commands: -

#### For factorial.c
```
riscv64-unknown-elf-gcc -O0 -g -march=rv64imac -mabi=lp64 \
-DUSERNAME="\"$U\"" -DHOSTNAME="\"$H\"" -DMACHINE_ID="\"$M\"" \
-DBUILD_UTC="\"$T\"" -DBUILD_EPOCH=$E \
factorial.c -o factorial
```
#### For max_array.c
```
riscv64-unknown-elf-gcc -O0 -g -march=rv64imac -mabi=lp64 \
-DUSERNAME="\"$U\"" -DHOSTNAME="\"$H\"" -DMACHINE_ID="\"$M\"" \
-DBUILD_UTC="\"$T\"" -DBUILD_EPOCH=$E \
max_array.c -o max_array
```
#### For bitops.c
```
riscv64-unknown-elf-gcc -O0 -g -march=rv64imac -mabi=lp64 \
-DUSERNAME="\"$U\"" -DHOSTNAME="\"$H\"" -DMACHINE_ID="\"$M\"" \
-DBUILD_UTC="\"$T\"" -DBUILD_EPOCH=$E \
bitops.c -o bitops
```
#### For bubble_sort.c
```
riscv64-unknown-elf-gcc -O0 -g -march=rv64imac -mabi=lp64 \
-DUSERNAME="\"$U\"" -DHOSTNAME="\"$H\"" -DMACHINE_ID="\"$M\"" \
-DBUILD_UTC="\"$T\"" -DBUILD_EPOCH=$E \
bubble_sort.c -o bubble_sort
```

## Proof of Uniqueness

### Each program output includes a clearly visible `ProofID` and `RunID`, which are generated using a 64-bit FNV-1a hash based on: -

- `USERNAME`
- `HOSTNAME`
- `MACHINE_ID`
- `BUILD_UTC`
- `BUILD_EPOCH`
- `Program name`

#### These fields ensure the build is unique to my machine and identity. All screenshots and output files (e.g., `factorial_output.png`, `bitops_output.png`) clearly show these values for verification.

