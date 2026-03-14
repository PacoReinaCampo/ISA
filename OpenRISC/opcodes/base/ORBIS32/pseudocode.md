## INSTRUCTION PSEUDO-CODE

Format of a line in the table:

`<instruction name> "<instruction pseudo code>"`

| instruction name       | instruction pseudo code                                                                 |
|------------------------|:----------------------------------------------------------------------------------------|
| `l.add rD,rA,rB`       | `rD[31:0] <- rA[31:0] + rB[31:0]`                                                       |
|                        | `SR[CY] <- carry (unsigned overflow)`                                                   |
|                        | `SR[OV] <- signed overflow`                                                             |
| `l.addc rD,rA,rB`      | `rD[31:0] <- rA[31:0] + rB[31:0] + SR[CY]`                                              |
|                        | `SR[CY] <- carry (unsigned overflow)`                                                   |
|                        | `SR[OV] <- signed overflow`                                                             |
| `l.addi rD,rA,I`       | `rD[31:0] <- rA[31:0] + exts(Immediate)`                                                |
|                        | `SR[CY] <- carry (unsigned overflow)`                                                   |
|                        | `SR[OV] <- signed overflow`                                                             |
| `l.addic rD,rA,I`      | `rD[31:0] <- rA[31:0] + exts(Immediate) + SR[CY]`                                       |
|                        | `SR[CY] <- carry (unsigned overflow)`                                                   |
|                        | `SR[OV] <- signed overflow`                                                             |
| `l.and rD,rA,rB`       | `rD[31:0] <- rA[31:0] AND rB[31:0]`                                                     |
| `l.andi rD,rA,K`       | `rD[31:0] <- rA[31:0] AND extz(Immediate)`                                              |
| `l.bf N`               | `EA <- exts(Immediate << 2) + BranchInsnAddr`                                           |
|                        | `PC <- EA if SR[F] set`                                                                 |
| `l.bnf N`              | `EA <- exts(Immediate << 2) + BranchInsnAddr`                                           |
|                        | `PC <- EA if SR[F] cleared`                                                             |
| `l.cmov rD,rA,rB`      | `rD[31:0] <- SR[F] ? rA[31:0] : rB[31:0]`                                               |
| `l.csync`              | `context-synchronization`                                                               |
| `l.cust1`              | `N/A`                                                                                   |
| `l.cust2`              | `N/A`                                                                                   |
| `l.cust3`              | `N/A`                                                                                   |
| `l.cust4`              | `N/A`                                                                                   |
| `l.cust5 rD,rA,rB,L,K` | `N/A`                                                                                   |
| `l.cust6`              | `N/A`                                                                                   |
| `l.cust7`              | `N/A`                                                                                   |
| `l.cust8`              | `N/A`                                                                                   |
| `l.div rD,rA,rB`       | `rD[31:0] <- rA[31:0] / rB[31:0]`                                                       |
|                        | `SR[OV] <- rB[31:0] == 0`                                                               |
| `l.divu rD,rA,rB`      | `rD[31:0] <- rA[31:0] / rB[31:0]`                                                       |
|                        | `SR[CY] <- rB[31:0] == 0`                                                               |
| `l.extbs rD,rA`        | `rD[31:8] <- rA[7]`                                                                     |
|                        | `rD[7:0] <- rA[7:0]`                                                                    |
| `l.extbz rD,rA`        | `rD[31:8] <- 0`                                                                         |
|                        | `rD[7:0] <- rA[7:0]`                                                                    |
| `l.exths rD,rA`        | `rD[31:16] <- rA[15]`                                                                   |
|                        | `rD[15:0] <- rA[15:0]`                                                                  |
| `l.exthz rD,rA`        | `rD[31:16] <- 0`                                                                        |
|                        | `rD[15:0] <- rA[15:0]`                                                                  |
| `l.extws rD,rA`        | `rD[31:0] <- rA[31:0]`                                                                  |
| `l.extwz rD,rA`        | `rD[31:0] <- rA[31:0]`                                                                  |
| `l.ff1 rD,rA,rB`       | `rD[31:0] <- rA[0] ? 1 : rA[1] ? 2 ... rA[31] ? 32 : 0`                                 |
| `l.fl1 rD,rA,rB`       | `rD[31:0] <- rA[31] ? 32 : rA[30] ? 31 ... rA[0] ? 1 : 0`                               |
| `l.j N`                | `PC <- exts(Immediate << 2) + JumpInsnAddr`                                             |
| `l.jal N`              | `PC <- exts(Immediate << 2) + JumpInsnAddr`                                             |
|                        | `LR <- CPUCFGR[ND] ? JumpInsnAddr + 4 : DelayInsnAddr + 4`                              |
| `l.jalr rB`            | `PC <- rB`                                                                              |
|                        | `LR <- CPUCFGR[ND] ? JumpInsnAddr + 4 : DelayInsnAddr + 4.`                             |
| `l.jr rB`              | `PC <- rB`                                                                              |
| `l.lbs rD,I(rA)`       | `EA <- exts(Immediate) + rA[31:0]`                                                      |
|                        | `rD[7:0] <- (EA)[7:0]`                                                                  |
|                        | `rD[31:8] <- (EA)[7]`                                                                   |
| `l.lbz rD,I(rA)`       | `EA <- exts(Immediate) + rA[31:0]`                                                      |
|                        | `rD[7:0] <- (EA)[7:0]`                                                                  |
|                        | `rD[31:8] <- 0`                                                                         |
| `l.ld rD,I(rA)`        | `N/A`                                                                                   |
| `l.lhs rD,I(rA)`       | `EA <- exts(Immediate) + rA[31:0]`                                                      |
|                        | `rD[15:0] <- (EA)[15:0]`                                                                |
|                        | `rD[31:16] <- (EA)[15]`                                                                 |
| `l.lhz rD,I(rA)`       | `EA <- exts(Immediate) + rA[31:0]`                                                      |
|                        | `rD[15:0] <- (EA)[15:0]`                                                                |
|                        | `rD[31:16] <- 0`                                                                        |
| `l.lwa rD,I(rA)`       | `EA <- exts(Immediate) + rA[31:0]`                                                      |
|                        | `rD[31:0] <- (EA)[31:0]`                                                                |
|                        | `atomic_reserve[to_phys(EA)] <- 1`                                                      |
| `l.lws rD,I(rA)`       | `EA <- exts(Immediate) + rA[31:0]`                                                      |
|                        | `rD[31:0] <- (EA)[31:0]`                                                                |
| `l.lwz rD,I(rA)`       | `EA <- exts(Immediate) + rA[31:0]`                                                      |
|                        | `rD[31:0] <- (EA)[31:0]`                                                                |
| `l.mac rA,rB`          | `MACHI[31:0]MACLO[31:0] <- MACHI[31:0]MACLO[31:0] + rA[31:0] * rB[31:0]`                |
|                        | `SR[OV] <- signed overflow during addition stage`                                       |
| `l.maci rA,I`          | `MACHI[31:0]MACLO[31:0] <- MACHI[31:0]MACLO[31:0] + rA[31:0] * exts(Immediate)`         |
|                        | `SR[OV] <- signed overflow during addition stage`                                       |
| `l.macrc rD`           | `synchronize-mac`                                                                       |
|                        | `rD[31:0] <- MACLO[31:0]`                                                               |
|                        | `MACLO[31:0], MACHI[31:0] <- 0`                                                         |
| `l.macu rA,rB`         | `MACHI[31:0]MACLO[31:0] <- MACHI[31:0]MACLO[31:0] + rA[31:0] * rB[31:0]`                |
|                        | `SR[CY] <- unsigned overflow during addition stage`                                     |
| `l.mfspr rD,rA,K`      | `rD[31:0] <- spr(rA OR Immediate)`                                                      |
| `l.movhi rD,K`         | `rD[31:0] <- extz(Immediate) << 16`                                                     |
| `l.msb rA,rB`          | `MACHI[31:0]MACLO[31:0] <- MACHI[31:0]MACLO[31:0] - rA[31:0] * rB[31:0]`                |
|                        | `SR[OV] <- signed overflow during subtraction stage`                                    |
| `l.msbu rA,rB`         | `MACHI[31:0]MACLO[31:0] <- MACHI[31:0]MACLO[31:0] - rA[31:0] * rB[31:0]`                |
|                        | `SR[CY] <- unsigned overflow during subtraction stage`                                  |
| `l.msync`              | `Memory-synchronization`                                                                |
| `l.mtspr rA,rB,K`      | `spr(rA OR Immediate) <- rB[31:0]`                                                      |
| `l.mul rD,rA,rB`       | `rD[31:0] <- rA[31:0] * rB[31:0]`                                                       |
|                        | `SR[OV] <- signed overflow`                                                             |
| `l.muld rA,rB`         | `MACHI[31:0]MACLO[31:0] <- rA[31:0] * rB[31:0]`                                         |
| `l.muldu rA,rB`        | `MACHI[31:0]MACLO[31:0] <- rA[31:0] * rB[31:0]`                                         |
| `l.muli rD,rA,I`       | `rD[31:0] <- rA[31:0] * exts(Immediate)`                                                |
|                        | `SR[OV] <- signed overflow`                                                             |
| `l.mulu rD,rA,rB`      | `rD[31:0] <- rA[31:0] * rB[31:0]`                                                       |
|                        | `SR[CY] <- carry (unsigned overflow)`                                                   |
| `l.nop K`              | `N/A`                                                                                   |
| `l.or rD,rA,rB`        | `rD[31:0] <- rA[31:0] OR rB[31:0]`                                                      |
| `l.ori rD,rA,K`        | `rD[31:0] <- rA[31:0] OR extz(Immediate)`                                               |
| `l.psync`              | `pipeline-synchronization`                                                              |
| `l.rfe`                | `PC <- EPCR`                                                                            |
|                        | `SR <- ESR`                                                                             |
| `l.ror rD,rA,rB`       | `rD[31-rB[4:0]:0] <- rA[31:rB[4:0]]`                                                    |
|                        | `rD[31:32-rB[4:0]] <- rA[rB[4:0]-1:0]`                                                  |
| `l.rori rD,rA,L`       | `rD[31-L:0] <- rA[31:L]`                                                                |
|                        | `rD[31:32-L] <- rA[L-1:0]`                                                              |
| `l.sb I(rA),rB`        | `EA <- exts(Immediate) + rA[31:0]`                                                      |
|                        | `(EA)[7:0] <- rB[7:0]`                                                                  |
| `l.sd I(rA),rB`        | `N/A`                                                                                   |
| `l.sfeq rA,rB`         | `SR[F] <- rA[31:0] == rB[31:0]`                                                         |
| `l.sfeqi rA,I`         | `SR[F] <- rA[31:0] == exts(Immediate)`                                                  |
| `l.sfges rA,rB`        | `SR[F] <- rA[31:0] >= rB[31:0]`                                                         |
| `l.sfgesi rA,I`        | `SR[F] <- rA[31:0] >= exts(Immediate)`                                                  |
| `l.sfgeu rA,rB`        | `SR[F] <- rA[31:0] >= rB[31:0]`                                                         |
| `l.sfgeui rA,I`        | `SR[F] <- rA[31:0] >= exts(Immediate)`                                                  |
| `l.sfgts rA,rB`        | `SR[F] <- rA[31:0] > rB[31:0]`                                                          |
| `l.sfgtsi rA,I`        | `SR[F] <- rA[31:0] > exts(Immediate)`                                                   |
| `l.sfgtu rA,rB`        | `SR[F] <- rA[31:0] > rB[31:0]`                                                          |
| `l.sfgtui rA,I`        | `SR[F] <- rA[31:0] > exts(Immediate)`                                                   |
| `l.sfles rA,rB`        | `SR[F] <- rA[31:0] <= rB[31:0]`                                                         |
| `l.sflesi rA,I`        | `SR[F] <- rA[31:0] <= exts(Immediate)`                                                  |
| `l.sfleu rA,rB`        | `SR[F] <- rA[31:0] <= rB[31:0]`                                                         |
| `l.sfleui rA,I`        | `SR[F] <- rA[31:0] <= exts(Immediate)`                                                  |
| `l.sflts rA,rB`        | `SR[F] <- rA[31:0] < rB[31:0]`                                                          |
| `l.sfltsi rA,I`        | `SR[F] <- rA[31:0] < exts(Immediate)`                                                   |
| `l.sfltu rA,rB`        | `SR[F] <- rA[31:0] < rB[31:0]`                                                          |
| `l.sfltui rA,I`        | `SR[F] <- rA[31:0] < exts(Immediate)`                                                   |
| `l.sfne rA,rB`         | `SR[F] <- rA[31:0] != rB[31:0]`                                                         |
| `l.sfnei rA,I`         | `SR[F] <- rA[31:0] != exts(Immediate)`                                                  |
| `l.sh I(rA),rB`        | `EA <- exts(Immediate) + rA[31:0]`                                                      |
|                        | `(EA)[15:0] <- rB[15:0]`                                                                |
| `l.sll rD,rA,rB`       | `rD[31:rB[4:0]] <- rA[31-rB[4:0]:0]`                                                    |
|                        | `rD[rB[4:0]-1:0] <- 0`                                                                  |
| `l.slli rD,rA,L`       | `rD[31:L] <- rA[31-L:0]`                                                                |
|                        | `rD[L-1:0] <- 0`                                                                        |
| `l.sra rD,rA,rB`       | `rD[31-rB[4:0]:0] <- rA[31:rB[4:0]]`                                                    |
|                        | `rD[31:32-rB[4:0]] <- rA[31]`                                                           |
| `l.srai rD,rA,L`       | `rD[31-L:0] <- rA[31:L]`                                                                |
|                        | `rD[31:32-L] <- rA[31]`                                                                 |
| `l.srl rD,rA,rB`       | `rD[31-rB[4:0]:0] <- rA[31:rB[4:0]]`                                                    |
|                        | `rD[31:32-rB[4:0]] <- 0`                                                                |
| `l.srli rD,rA,L`       | `rD[31-L:0] <- rA[31:L]`                                                                |
|                        | `rD[31:32-L] <- 0`                                                                      |
| `l.sub rD,rA,rB`       | `rD[31:0] <- rA[31:0] - rB[31:0]`                                                       |
|                        | `SR[CY] <- carry (unsigned overflow)`                                                   |
|                        | `SR[OV] <- signed overflow`                                                             |
| `l.sw I(rA),rB`        | `EA <- exts(Immediate) + rA[31:0]`                                                      |
|                        | `(EA)[31:0] <- rB[31:0]`                                                                |
| `l.swa I(rA),rB`       | `EA <- exts(Immediate) + rA[31:0]`                                                      |
|                        | `if (atomic) (EA)[31:0] <- rB[31:0]`                                                    |
|                        | `SR[F] <- atomic`                                                                       |
| `l.sys K`              | `system-call-exception(K)`                                                              |
| `l.trap K`             | `trap-exception()`                                                                      |
| `l.xor rD,rA,rB`       | `rD[31:0] <- rA[31:0] XOR rB[31:0]`                                                     |
| `l.xori rD,rA,I`       | `rD[31:0] <- rA[31:0] XOR exts(Immediate)`                                              |
| `lf.add.d rD,rA,rB`    | `N/A`                                                                                   |
| `lf.add.s rD,rA,rB`    | `rD[31:0] <- rA[31:0] + rB[31:0]`                                                       |
| `lf.cust1.d rA,rB`     | `N/A`                                                                                   |
| `lf.cust1.s rA,rB`     | `N/A`                                                                                   |
| `lf.div.d rD,rA,rB`    | `N/A`                                                                                   |
| `lf.div.s rD,rA,rB`    | `rD[31:0] <- rA[31:0] / rB[31:0]`                                                       |
| `lf.ftoi.d rD,rA`      | `N/A`                                                                                   |
| `lf.ftoi.s rD,rA`      | `rD[31:0] <- ftoi(rA[31:0])`                                                            |
| `lf.itof.d rD,rA`      | `N/A`                                                                                   |
| `lf.itof.s rD,rA`      | `rD[31:0] <- itof(rA[31:0])`                                                            |
| `lf.madd.d rD,rA,rB`   | `N/A`                                                                                   |
| `lf.madd.s rD,rA,rB`   | `FPMADDHI[31:0]FPMADDLO[31:0] <- rA[31:0] * rB[31:0] + FPMADDHI[31:0]FPMADDLO[31:0]`    |
| `lf.mul.d rD,rA,rB`    | `N/A`                                                                                   |
| `lf.mul.s rD,rA,rB`    | `rD[31:0] <- rA[31:0] * rB[31:0]`                                                       |
| `lf.rem.d rD,rA,rB`    | `N/A`                                                                                   |
| `lf.rem.s rD,rA,rB`    | `rD[31:0] <- rA[31:0] % rB[31:0]`                                                       |
| `lf.sfeq.d rA,rB`      | `N/A`                                                                                   |
| `lf.sfeq.s rA,rB`      | `SR[F] <- rA[31:0] == rB[31:0]`                                                         |
| `lf.sfge.d rA,rB`      | `N/A`                                                                                   |
| `lf.sfge.s rA,rB`      | `SR[F] <- rA[31:0] >= rB[31:0]`                                                         |
| `lf.sfgt.d rA,rB`      | `N/A`                                                                                   |
| `lf.sfgt.s rA,rB`      | `SR[F] <- rA[31:0] > rB[31:0]`                                                          |
| `lf.sfle.d rA,rB`      | `N/A`                                                                                   |
| `lf.sfle.s rA,rB`      | `SR[F] <- rA[31:0] <= rB[31:0]`                                                         |
| `lf.sflt.d rA,rB`      | `N/A`                                                                                   |
| `lf.sflt.s rA,rB`      | `SR[F] <- rA[31:0] < rB[31:0]`                                                          |
| `lf.sfne.d rA,rB`      | `N/A`                                                                                   |
| `lf.sfne.s rA,rB`      | `SR[F] <- rA[31:0] != rB[31:0]`                                                         |
| `lf.sub.d rD,rA,rB`    | `N/A`                                                                                   |
| `lf.sub.s rD,rA,rB`    | `rD[31:0] <- rA[31:0] - rB[31:0]`                                                       |
| `lv.add.b rD,rA,rB`    | `N/A`                                                                                   |
| `lv.add.h rD,rA,rB`    | `N/A`                                                                                   |
| `lv.adds.b rD,rA,rB`   | `N/A`                                                                                   |
| `lv.adds.h rD,rA,rB`   | `N/A`                                                                                   |
| `lv.addu.b rD,rA,rB`   | `N/A`                                                                                   |
| `lv.addu.h rD,rA,rB`   | `N/A`                                                                                   |
| `lv.addus.b rD,rA,rB`  | `N/A`                                                                                   |
| `lv.addus.h rD,rA,rB`  | `N/A`                                                                                   |
| `lv.all_eq.b rD,rA,rB` | `N/A`                                                                                   |
| `lv.all_eq.h rD,rA,rB` | `N/A`                                                                                   |
| `lv.all_ge.b rD,rA,rB` | `N/A`                                                                                   |
| `lv.all_ge.h rD,rA,rB` | `N/A`                                                                                   |
| `lv.all_gt.b rD,rA,rB` | `N/A`                                                                                   |
| `lv.all_gt.h rD,rA,rB` | `N/A`                                                                                   |
| `lv.all_le.b rD,rA,rB` | `N/A`                                                                                   |
| `lv.all_le.h rD,rA,rB` | `N/A`                                                                                   |
| `lv.all_lt.b rD,rA,rB` | `N/A`                                                                                   |
| `lv.all_lt.h rD,rA,rB` | `N/A`                                                                                   |
| `lv.all_ne.b rD,rA,rB` | `N/A`                                                                                   |
| `lv.all_ne.h rD,rA,rB` | `N/A`                                                                                   |
| `lv.and rD,rA,rB`      | `N/A`                                                                                   |
| `lv.any_eq.b rD,rA,rB` | `N/A`                                                                                   |
| `lv.any_eq.h rD,rA,rB` | `N/A`                                                                                   |
| `lv.any_ge.b rD,rA,rB` | `N/A`                                                                                   |
| `lv.any_ge.h rD,rA,rB` | `N/A`                                                                                   |
| `lv.any_gt.b rD,rA,rB` | `N/A`                                                                                   |
| `lv.any_gt.h rD,rA,rB` | `N/A`                                                                                   |
| `lv.any_le.b rD,rA,rB` | `N/A`                                                                                   |
| `lv.any_le.h rD,rA,rB` | `N/A`                                                                                   |
| `lv.any_lt.b rD,rA,rB` | `N/A`                                                                                   |
| `lv.any_lt.h rD,rA,rB` | `N/A`                                                                                   |
| `lv.any_ne.b rD,rA,rB` | `N/A`                                                                                   |
| `lv.any_ne.h rD,rA,rB` | `N/A`                                                                                   |
| `lv.avg.b rD,rA,rB`    | `N/A`                                                                                   |
| `lv.avg.h rD,rA,rB`    | `N/A`                                                                                   |
| `lv.cmp_eq.b rD,rA,rB` | `N/A`                                                                                   |
| `lv.cmp_eq.h rD,rA,rB` | `N/A`                                                                                   |
| `lv.cmp_ge.b rD,rA,rB` | `N/A`                                                                                   |
| `lv.cmp_ge.h rD,rA,rB` | `N/A`                                                                                   |
| `lv.cmp_gt.b rD,rA,rB` | `N/A`                                                                                   |
| `lv.cmp_gt.h rD,rA,rB` | `N/A`                                                                                   |
| `lv.cmp_le.b rD,rA,rB` | `N/A`                                                                                   |
| `lv.cmp_le.h rD,rA,rB` | `N/A`                                                                                   |
| `lv.cmp_lt.b rD,rA,rB` | `N/A`                                                                                   |
| `lv.cmp_lt.h rD,rA,rB` | `N/A`                                                                                   |
| `lv.cmp_ne.b rD,rA,rB` | `N/A`                                                                                   |
| `lv.cmp_ne.h rD,rA,rB` | `N/A`                                                                                   |
| `lv.cust1`             | `N/A`                                                                                   |
| `lv.cust2`             | `N/A`                                                                                   |
| `lv.cust3`             | `N/A`                                                                                   |
| `lv.cust4`             | `N/A`                                                                                   |
| `lv.madds.h rD,rA,rB`  | `N/A`                                                                                   |
| `lv.max.b rD,rA,rB`    | `N/A`                                                                                   |
| `lv.max.h rD,rA,rB`    | `N/A`                                                                                   |
| `lv.merge.b rD,rA,rB`  | `N/A`                                                                                   |
| `lv.merge.h rD,rA,rB`  | `N/A`                                                                                   |
| `lv.min.b rD,rA,rB`    | `N/A`                                                                                   |
| `lv.min.h rD,rA,rB`    | `N/A`                                                                                   |
| `lv.msubs.h rD,rA,rB`  | `N/A`                                                                                   |
| `lv.muls.h rD,rA,rB`   | `N/A`                                                                                   |
| `lv.nand rD,rA,rB`     | `N/A`                                                                                   |
| `lv.nor rD,rA,rB`      | `N/A`                                                                                   |
| `lv.or rD,rA,rB`       | `N/A`                                                                                   |
| `lv.pack.b rD,rA,rB`   |                                                                                         |
| `lv.pack.h rD,rA,rB`   | `N/A`                                                                                   |
| `lv.packs.b rD,rA,rB`  |                                                                                         |
| `lv.packs.h rD,rA,rB`  | `N/A`                                                                                   |
| `lv.packus.b rD,rA,rB` |                                                                                         |
| `lv.packus.h rD,rA,rB` | `N/A`                                                                                   |
| `lv.perm.n rD,rA,rB`   |                                                                                         |
| `lv.rl.b rD,rA,rB`     | `N/A`                                                                                   |
| `lv.rl.h rD,rA,rB`     | `N/A`                                                                                   |
| `lv.sll rD,rA,rB`      | `N/A`                                                                                   |
| `lv.sll.b rD,rA,rB`    | `N/A`                                                                                   |
| `lv.sll.h rD,rA,rB`    | `N/A`                                                                                   |
| `lv.sra.b rD,rA,rB`    | `N/A`                                                                                   |
| `lv.sra.h rD,rA,rB`    | `N/A`                                                                                   |
| `lv.srl rD,rA,rB`      | `N/A`                                                                                   |
| `lv.srl.b rD,rA,rB`    | `N/A`                                                                                   |
| `lv.srl.h rD,rA,rB`    | `N/A`                                                                                   |
| `lv.sub.b rD,rA,rB`    | `N/A`                                                                                   |
| `lv.sub.h rD,rA,rB`    | `N/A`                                                                                   |
| `lv.subs.b rD,rA,rB`   | `N/A`                                                                                   |
| `lv.subs.h rD,rA,rB`   | `N/A`                                                                                   |
| `lv.subu.b rD,rA,rB`   | `N/A`                                                                                   |
| `lv.subu.h rD,rA,rB`   | `N/A`                                                                                   |
| `lv.subus.b rD,rA,rB`  | `N/A`                                                                                   |
| `lv.subus.h rD,rA,rB`  | `N/A`                                                                                   |
| `lv.unpack.b rD,rA,rB` | `N/A`                                                                                   |
| `lv.unpack.h rD,rA,rB` | `N/A`                                                                                   |
| `lv.xor rD,rA,rB`      | `N/A`                                                                                   |

:OpenRISC 32-Bit - "OpenRISC 32-Bit Base Integer Instruction Set"
