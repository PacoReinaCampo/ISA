# RISC-V E Extension

## Formats

```
15     14     13     12     11     10     09     08     07     06     05     04     03     02     01     00 |
|-----------------------------------------------------------------------------------------------------------|
| funct4                 | rd/rs1                           | rs2                              | op         | R (Register)
|-----------------------------------------------------------------------------------------------------------|
| funct3          | imm  | rd/rs1                           | imm                              | op         | I (Immediate)
|-----------------------------------------------------------------------------------------------------------|
| funct3          | imm                                     | rs2                              | op         | SS (Stack-Store)
|-----------------------------------------------------------------------------------------------------------|
| funct3          | imm                                                   | rd                 | op         | IW (Wide-Immediate)
|-----------------------------------------------------------------------------------------------------------|
| funct3          | imm                | rs1                | imm         | rd                 | op         | L (Load)
|-----------------------------------------------------------------------------------------------------------|
| funct3          | imm                | rs1                | imm         | rs2                | op         | S (Store)
|-----------------------------------------------------------------------------------------------------------|
| funct6                               | rd                 | funct2      | rs2                | op         | A (Arithmetic)
|-----------------------------------------------------------------------------------------------------------|
| funct3          | offset             | rs1                | offset                           | op         | B (Branch)
|-----------------------------------------------------------------------------------------------------------|
| funct3          | jump target                                                                | op         | J (Jump)
|-----------------------------------------------------------------------------------------------------------|
```

## Instructions

* **RV32E - `RV32E Base Integer Instruction Set`**

  | **Name**  | **Pseudo-Code**                                                                         | **Notes**                        |
  |:----------|:----------------------------------------------------------------------------------------|:---------------------------------|
  | `lui`     | `rd = imm`                                                                              |                                  |
  | `auipc`   | `rd = pc + imm`                                                                         |                                  |
  | `jal`     | `rd = pc + length(inst); pc_offset = imm`                                               |                                  |
  | `jalr`    | `ux new_offset = (rs1 + imm - pc) & ~1; rd = pc + length(inst); pc_offset = new_offset` |                                  |
  | `beq`     | `if (sx(rs1) == sx(rs2)) pc_offset = imm`                                               |                                  |
  | `bne`     | `if (sx(rs1) != sx(rs2)) pc_offset = imm`                                               |                                  |
  | `blt`     | `if (sx(rs1) < sx(rs2)) pc_offset = imm`                                                |                                  |
  | `bge`     | `if (sx(rs1) >= sx(rs2)) pc_offset = imm`                                               |                                  |
  | `bltu`    | `if (ux(rs1) < ux(rs2)) pc_offset = imm`                                                |                                  |
  | `bgeu`    | `if (ux(rs1) >= ux(rs2)) pc_offset = imm`                                               |                                  |
  | `lb`      | `s8 t; mmu.load<s8>(rs1 + imm, t); rd = t`                                              | `rd = sx(*(s8*)ptr(rs1 + imm))`  |
  | `lh`      | `s16 t; mmu.load<s16>(rs1 + imm, t); rd = t`                                            | `rd = sx(*(s16*)ptr(rs1 + imm))` |
  | `lw`      | `s32 t; mmu.load<s32>(rs1 + imm, t); rd = t`                                            | `rd = sx(*(s32*)ptr(rs1 + imm))` |
  | `lbu`     | `u8 t; mmu.load<u8>(rs1 + imm, t); rd = t`                                              | `rd = ux(*(u8*)ptr(rs1 + imm))`  |
  | `lhu`     | `u16 t; mmu.load<u16>(rs1 + imm, t); rd = t`                                            | `rd = ux(*(u16*)ptr(rs1 + imm))` |
  | `lwu`     | `u32 t; mmu.load<u32>(rs1 + imm, t); rd = t`                                            | `rd = ux(*(u32*)ptr(rs1 + imm))` |
  | `sb`      | `mmu.store<s8>(rs1 + imm, s8(rs2))`                                                     | `*((u8*)ptr(rs1 + imm)) = rs2`   |
  | `sh`      | `mmu.store<s16>(rs1 + imm, s16(rs2))`                                                   | `*((u16*)ptr(rs1 + imm)) = rs2`  |
  | `sw`      | `mmu.store<s32>(rs1 + imm, s32(rs2))`                                                   | `*((u32*)ptr(rs1 + imm)) = rs2`  |
  | `addi`    | `rd = sx(rs1) + sx(imm)`                                                                |                                  |
  | `slti`    | `rd = sx(rs1) < sx(imm)`                                                                |                                  |
  | `sltiu`   | `rd = ux(rs1) < ux(imm)`                                                                |                                  |
  | `xori`    | `rd = ux(rs1) ^ ux(imm)`                                                                |                                  |
  | `ori`     | `rd = ux(rs1) \| ux(imm)`                                                               |                                  |
  | `andi`    | `rd = ux(rs1) & ux(imm)`                                                                |                                  |
  | `slli`    | `rd = ux(rs1) << imm`                                                                   |                                  |
  | `srli`    | `rd = ux(rs1) >> imm`                                                                   |                                  |
  | `srai`    | `rd = sx(rs1) >> imm`                                                                   |                                  |
  | `add`     | `rd = sx(rs1) + sx(rs2)`                                                                |                                  |
  | `sub`     | `rd = sx(rs1) - sx(rs2)`                                                                |                                  |
  | `sll`     | `rd = ux(rs1) << (rs2 & 0b1111111)`                                                     | `7-bit mask for RV128I`          |
  | `slt`     | `rd = sx(rs1) < sx(rs2)`                                                                |                                  |
  | `sltu`    | `rd = ux(rs1) < ux(rs2)`                                                                |                                  |
  | `xor`     | `rd = ux(rs1) ^ ux(rs2)`                                                                |                                  |
  | `srl`     | `rd = ux(rs1) >> (rs2 & 0b1111111)`                                                     | `7-bit mask for RV128I`          |
  | `sra`     | `rd = sx(rs1) >> (rs2 & 0b1111111)`                                                     | `7-bit mask for RV128I`          |
  | `or`      | `rd = ux(rs1) \| ux(rs2)`                                                               |                                  |
  | `and`     | `rd = ux(rs1) & ux(rs2)`                                                                |                                  |
  | `fence`   |                                                                                         |                                  |
  | `fence.i` |                                                                                         |                                  |

* **RV64E - `RV64E Base Integer Instruction Set (in addition to RV32E)`**

  | **Name**  | **Pseudo-Code**                              | **Notes**                        |
  |:----------|:---------------------------------------------|:---------------------------------|
  | `ld`      | `s64 t; mmu.load<s64>(rs1 + imm, t); rd = t` | `rd = sx(*(s64*)ptr(rs1 + imm))` |
  | `sd`      | `mmu.store<s64>(rs1 + imm, s64(rs2))`        | `*(u64*)ptr(rs1 + imm) = rs2`    |
  | `addiw`   | `rd = s32(s32(rs1) + imm)`                   | `clang requires -fwrapv`         |
  | `slliw`   | `rd = s32(u32(rs1) << imm)`                  |                                  |
  | `srliw`   | `rd = s32(u32(rs1) >> imm)`                  |                                  |
  | `sraiw`   | `rd = s32(rs1) >> imm`                       |                                  |
  | `addw`    | `rd = s32(s32(rs1) + s32(rs2))`              | `clang requires -fwrapv`         |
  | `subw`    | `rd = s32(s32(rs1) - s32(rs2))`              | `clang requires -fwrapv`         |
  | `sllw`    | `rd = s32(u32(rs1) << (rs2 & 0b11111))`      |                                  |
  | `srlw`    | `rd = s32(u32(rs1) >> (rs2 & 0b11111))`      |                                  |
  | `sraw`    | `rd = s32(s32(rs1) >> (rs2 & 0b11111))`      |                                  |

## Registers

| name   | alias   | type    | save      |  description                          |
|--------|:--------|:--------|:----------|:--------------------------------------|
| `x0`   | `zero`  | `ireg`  | `zero`    | `Hard-wired zero`                     |
| `x1`   | `ra`    | `ireg`  | `caller`  | `Return address Caller`               |
| `x2`   | `sp`    | `ireg`  | `callee`  | `Stack pointer Callee`                |
| `x3`   | `gp`    | `ireg`  | `global`  | `Global pointer`                      |
| `x4`   | `tp`    | `ireg`  | `callee`  | `Thread pointer Callee`               |
| `x5`   | `t0`    | `ireg`  | `caller`  | `Temporaries Caller`                  |
| `x6`   | `t1`    | `ireg`  | `caller`  | `Temporaries Caller`                  |
| `x7`   | `t2`    | `ireg`  | `caller`  | `Temporaries Caller`                  |
| `x8`   | `s0`    | `ireg`  | `callee`  | `Saved register/frame pointer Callee` |
| `x9`   | `s1`    | `ireg`  | `callee`  | `Saved registers Callee`              |
| `x10`  | `a0`    | `ireg`  | `caller`  | `Function arguments Caller`           |
| `x11`  | `a1`    | `ireg`  | `caller`  | `Function arguments Caller`           |
| `x12`  | `a2`    | `ireg`  | `caller`  | `Function arguments Caller`           |
| `x13`  | `a3`    | `ireg`  | `caller`  | `Function arguments Caller`           |
| `x14`  | `a4`    | `ireg`  | `caller`  | `Function arguments Caller`           |
| `x15`  | `a5`    | `ireg`  | `caller`  | `Function arguments Caller`           |
