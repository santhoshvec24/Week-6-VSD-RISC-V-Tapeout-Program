# Good floorplan vs Bad floorplan and Introduction to library cells

Day 2 Summary — Floorplan, Libraries & Placement

---

### 1. Utilization & Aspect Ratio:
Defines how much of the core is used by standard cells (60–75% ideal) and the width–height ratio of the core. Both affect congestion, timing, and routing efficiency.

### 2. Pre-Placed Cells:
Large macros, memories, and I/O blocks are fixed early to reserve routing channels and guide standard-cell placement.

### 3. Decoupling Capacitors:
Provide instant current during switching to reduce voltage noise, IR drop, and ground bounce—key for power integrity.

### 4. Power Planning:
Designing the power grid (rails, straps, vias) ensures stable supply and reliability; improper planning causes timing and IR-drop issues.

### 5. Pin Placement & Blockages:
Proper pin locations reduce routing length; placement blockages prevent cells from being placed in reserved or congested zones.

### 6. Floorplan Flow in OpenLANE:
Set core size, utilization, aspect ratio, and macro positions; generate DEF and inspect floorplan for correctness.

### 7. Floorplan Files & Viewing:
DEF/LEF and TCL scripts describe floorplans; inspect them using Magic, KLayout, or OpenROAD to verify placements and blockages.

### 8. Magic Floorplan Review:
Use Magic to visualize the physical layout with the Sky130 PDK and verify DRC compliance.

### 9. Library Binding & Placement Optimization:
Logical cells are mapped to physical library cells; placement is optimized to reduce wirelength and meet timing constraints.

### 10. Final Placement Optimization:
Refine placement using timing-driven methods and rebuffering to improve timing and routability.

### 11. Libraries & Characterization:
Standard-cell libraries (.lib, .lef) define cell area, timing, and power; characterized from SPICE simulations at multiple PVT corners.

### 12. Congestion-Aware Placement (RePlAce):
Global placer that balances cell density and connectivity to improve routability.

### 13. Cell Design & Characterization Flow:
Starts with schematic and layout design, followed by parasitic extraction, SPICE timing analysis, and Liberty file generation.

### 14. Timing Basics:
Defines setup, hold, propagation delay, and transition time — essential for timing analysis and ensuring correct flip-flop operation.

---
## Running Floorplan in OpenLANE
Once synthesis is complete, floorplanning can be executed using OpenLANE’s interactive shell:

As usual, start by opening the Docker container from the OpenLANE directory, then continue the flow beginning from the synthesis stage of the Day 1 task.
```bash
run_floorplan
```

<img width="1919" height="949" alt="Screenshot 2025-10-31 153755" src="https://github.com/user-attachments/assets/109a1bba-6d33-4a88-bfad-8f43d67f69cd" />

<img width="1439" height="993" alt="image" src="https://github.com/user-attachments/assets/dddd2b1f-81ea-46bf-936b-fbffdc024e31" />

### Die Area Calculation  in microns
From `picorv32a.floorplan.def` :

```def
DESIGN picorv32a ;
UNITS DISTANCE MICRONS 1000 ;
DIEAREA ( 0 0 ) ( 660685 671405 ) ;
```

Die Width = 660685 / 1000 = 660.685 μm

Die Height = 671405 / 1000 = 671.405 μm

Area = 660.685 × 671.405 = 443,587.21 μm²

---

Then enter into the directory `~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/10-11_15-34/results/floorplan`

```bash
magic -T ~/soc-design-and-planning-nasscom-vsd/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def &
```

<img width="1452" height="994" alt="image" src="https://github.com/user-attachments/assets/bab69a30-2f04-4903-8c61-6bc6eead11da" />

<img width="1829" height="978" alt="image" src="https://github.com/user-attachments/assets/b80a3a9f-ce1e-459c-bf94-55922df72ca4" />

---

## What is Placement?
Placement is the process of determining the exact physical location of each standard cell on the chip layout.

This stage aims to minimize total wire length, satisfy timing constraints, and maintain balanced cell density across the core area.

It consists of two main phases:

- **Global Placement**: Performs an initial coarse positioning of cells.

- **Detailed Placement**: Refines the placement and ensures legalization by removing any overlaps.

### Placement in OpenLANE
OpenLANE automates both placement phases, optimizing cell arrangement for better timing and routability.
```bash
run_placement
```

<img width="1916" height="964" alt="image" src="https://github.com/user-attachments/assets/cea94322-0fc2-44db-9016-3d7f62e8f770" />

<img width="1108" height="914" alt="image" src="https://github.com/user-attachments/assets/5b75540e-0003-4466-892b-60dcd8ca7d92" />

Then enter into the directory `~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/10-11_15-34/results/placement`

```bash
magic -T ~/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def &
```
<img width="1834" height="981" alt="image" src="https://github.com/user-attachments/assets/87fd2437-6dc9-4d33-8622-1f179c2a87b0" />

<img width="1838" height="997" alt="image" src="https://github.com/user-attachments/assets/80b1e487-ff7a-4d78-a193-37093a190161" />

---

## Standard Cell Design & Characterization Flow

### a) Cell Design Flow

Each standard cell (such as an inverter, NAND, etc.) follows a well-defined development sequence before being added to the standard cell library:

1. **Specification & Logic Design**
2. **Schematic Creation & Functional Simulation**
3. **Layout Design (Physical Implementation)**
4. **DRC and LVS Verification**
5. **Electrical Characterization (Timing, Power, and Function)**
6. **Library File Generation (.lib, .lef, .gds)**

After successful verification, these cells become part of the standard cell library used in the **synthesis, placement, and routing** phases of chip design.

---

### b) Cell Characterization Flow

Cell characterization defines the **electrical behavior** of each cell by extracting timing, power, and constraint data through **SPICE simulations**.

#### Typical Steps:

1. **Netlist Extraction**
2. **Parameter Definition**
3. **Model Selection**
4. **SPICE Simulation and Data Measurement**
5. **Model Generation (.lib)**
6. **Verification and Validation**

The resulting **.lib files** provide precise **delay and power information** essential for **Static Timing Analysis (STA)** and synthesis tools.

---

### Summary Table

| Step | Task              | Tool / Command  | Output / Result                           |
| ---- | ----------------- | --------------- | ----------------------------------------- |
| 1    | Execute floorplan | `run_floorplan` | `picorv32a.floorplan.def`                 |
| 2    | View floorplan    | Magic           | Floorplan visualization                   |
| 3    | Execute placement | `run_placement` | `picorv32a.placement.def`                 |
| 4    | View placement    | Magic           | Standard-cell placement layout            |
| 5    | Review cell flow  | Conceptual      | Cell design and characterization overview |

---

### Next Step

Proceed to **Day 3 — Custom Library Cell Design using Magic & ngspice**
You’ll design a **CMOS inverter**, perform **DRC/LVS checks**, extract a **SPICE netlist**, and measure **delay and power characteristics**.

---
