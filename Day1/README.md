# Inception of open-source EDA, OpenLANE and Sky130 PDK

## 1. Open-Source EDA & Sky130 Overview

- Motivation: Enable reproducible, affordable, and community-driven chip design.

- Key Components:

    - OpenLANE – complete RTL-to-GDS flow (synthesis → P&R → signoff).

    - Sky130 PDK – open-source process design kit with real foundry data (LEF, DEF, SPICE, DRC rules).

- Impact: Democratizes silicon design for students, startups, and researchers using open tools (Magic, ngspice, Yosys, OpenROAD, etc.).

---

## 2. How Computers Understand Designers

- **Abstraction Flow**: Human idea → Algorithm → High-level code → Compiler → Assembly → Machine → Hardware.

- **ASIC Flow**: Algorithm → RTL → Gates → Layout → Masks → Silicon.

- **Key Insight**: Hardware designers express logic in RTL while managing timing, area, and power constraints.

---

## 3. Package, Chip, and Die (QFN-48)

- **Chip**: Packaged silicon die.

- **Die**: Bare silicon implementing logic.

- **Package**: Interface between die and PCB (QFN-48 = 48 pins).

- **Core vs Pads**:

   - Core = logic area

   - Pads = I/O interface

- **Why It Matters**: Packaging affects I/O count, floorplan, and thermal design.

---

## 4. Introduction to RISC-V

- **Concept**: Open, modular instruction set (RV32I/RV64I + extensions).

- **Benefits**: Customizable, royalty-free ISA.

- **Tools**: GCC/LLVM, Spike, QEMU, Verilator.

- **Use Case**: Great for SoC and tapeout projects (e.g., PicoRV32).

---

## 5. From Software to Hardware

- **Goal**: Identify performance-critical software parts and convert to hardware accelerators.

- **Process**: Profiling → Hotspot detection → RTL design → Integration.

- **Example**: FFT or encryption cores.

- **Benefit**: Optimized power, latency, and performance.

---

## 6. SoC Design & OpenLANE Flow Overview

- **Components**: RTL, synthesis, placement, routing, STA, DRC/LVS, SPICE.

- **Tools**: Yosys, OpenROAD, Magic, TritonRoute, OpenSTA.

- **Project Structure**: src/, synth/, layout/, reports/, runs/.

---

## 7. Simplified RTL-to-GDS Flow

1. RTL
2. Synthesis
3. Floorplan
4. Placement
5. CTS
6. Routing
7. Extraction
8. Signoff (DRC/LVS/STA)

Purpose: Understand data handoff between stages (DEF/LEF flow).

---

## 8. OpenLANE & Strive Chipsets

- **OpenLANE**: Automated flow orchestrator for RTL-to-GDS.

- **Strive**: Example SoC or design platform used to demonstrate OpenLANE usage.

## 9. OpenLANE Directory & Design Preparation

**Folders:**

- `flow/` – scripts

- `designs/` – user projects

- `pdks/` – technology files

- `runs/` – results/logs

Design Prep Tasks: Lint RTL, define constraints (.sdc), verify libraries, and prepare config files.

---

## 10. Synthesis & Result Characterization

- **Check Outputs**: Synthesized netlist, timing reports, cell utilization.

- **Analyze**: Area, slack, critical paths, and register/logic ratio.

- **Purpose**: Early identification of timing or logic issues before layout.

---

## Practical Implementation
### Step 1: Launching OpenLANE and Setting Up the Environment

To begin, I entered the OpenLANE directory and invoked the interactive Docker environment.

```bash
cd~/Desktop/work/tools/openlane_working_dir/openlane
```
 **Building PDKs from Source**

```bash
export PDK_ROOT=/home/vsduser/Desktop/work/tools/openlane_working_dir/pdks
cd ~/Desktop/work/tools/openlane_working_dir/openlane
alias docker='docker run -it -v $(pwd):/openLANE_flow -v $PDK_ROOT:$PDK_ROOT -e PDK_ROOT=$PDK_ROOT -u $(id -u $USER):$(id -g $USER) efabless/openlane:v0.21'
docker
./flow.tcl -interactive
```

<img width="1858" height="894" alt="Screenshot 2025-10-31 151940" src="https://github.com/user-attachments/assets/28914114-9cde-4c33-ba1d-c52353527194" />

```bash
package require openlane 0.9
```

```bash
prep -design picorv32a
```
<img width="1911" height="892" alt="Screenshot 2025-10-31 152830" src="https://github.com/user-attachments/assets/e33b9ef4-9d9a-4aa6-8638-ca831b8a1841" />

```bash
run_synthesis
```

<img width="1918" height="985" alt="image" src="https://github.com/user-attachments/assets/95c12060-dfab-40c9-94a8-27b39bc5b9ba" />

<img width="1919" height="989" alt="image" src="https://github.com/user-attachments/assets/b2bb40d8-5c01-4987-8b0a-72cee099a960" />

```
vsduser@santhosh:~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/10-11_13-33/reports/synthesis$ ls
10-opensta_post_resizer.min_max.rpt  22-opensta_spef.rpt
10-opensta_post_resizer.rpt          22-opensta_spef.slew.rpt
10-opensta_post_resizer.slew.rpt     22-opensta_spef.timing.rpt
10-opensta_post_resizer.timing.rpt   22-opensta_spef_tns.rpt
10-opensta_post_resizer_tns.rpt      22-opensta_spef_wns.rpt
10-opensta_post_resizer_wns.rpt      2-opensta.min_max.rpt
1-yosys_4.chk.rpt                    2-opensta.rpt
1-yosys_4.stat.rpt                   2-opensta.slew.rpt
1-yosys_dff.stat                     2-opensta.timing.rpt
1-yosys_pre.stat                     2-opensta_tns.rpt
22-opensta_spef.min_max.rpt          2-opensta_wns.rpt
```

```bash
gedit 1-yosys_4.stat.rpt 
```

<img width="1831" height="964" alt="image" src="https://github.com/user-attachments/assets/2245d28f-7f50-4001-a576-8da4622f4eb0" />

---

## In Essence:
Day 1 builds foundational understanding of open-source silicon design — from concept to synthesis — using OpenLANE, Sky130 PDK, and RISC-V as practical learning platforms.

---
RC extraction is done

<img width="1914" height="990" alt="image" src="https://github.com/user-attachments/assets/59659a16-7b2f-4bc6-9e5a-94f3e2960b03" />
