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

