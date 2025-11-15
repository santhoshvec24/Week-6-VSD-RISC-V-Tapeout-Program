# Design library cell using Magic Layout and ngspice characterization

Focuses on understanding the complete inverter design flow — from circuit simulation to layout fabrication, verification, and characterization using the Sky130 PDK.

---

### 1. IO Placer Revision

- Optimize pad and pin placement to ensure short routing paths and minimal crossovers.

- Proper IO placement improves board routing, signal timing, and connectivity between package → die → PCB.

---

### 2. SPICE Deck Creation

- Build a SPICE file including transistor netlist, Sky130 model files, power supplies, input stimuli, and measurement commands.

- Used for functional and timing characterization of the CMOS inverter.

---

### 3. SPICE Simulation Lab

- Run DC, transient, and parametric analyses to measure VOH, VOL, rise/fall times, propagation delay, and power.

- Validate circuit performance and extract switching threshold Vm

---

### 4. Switching Threshold (Vm)
​
- Vm is the point where input equals output (Vout = Vin).

- Determines inverter balance and noise margins; ideally ≈ VDD/2.

- Controlled by adjusting the PMOS/NMOS width ratio.

---

### 5. Static vs Dynamic Simulation

- Static (DC): Logic levels, leakage, voltage thresholds.

- Dynamic (Transient): Switching delay and dynamic power (∝ C·V²·f).

- Both are essential for performance and power analysis.

---

### 6. Git Clone – vsdstdcelldesign

- Clone the VSD standard cell design repo to replicate the inverter flow.

- Explore files, check PDK setup, and run simulations within a Docker/container environment.

---

### 7. CMOS Layout Fabrication Process

- Step-by-step transistor formation:

- Define active regions (diffusion areas).

- Form N-well/P-well regions for PMOS/NMOS isolation.

- Deposit and pattern gate poly.

- Perform LDD doping to reduce hot-carrier effects.

- Form source/drain contacts.

- Add local interconnects within cells.

- Build higher metal layers for global routing.

---

### 8. Sky130 Layers & LEF

- Learn Sky130 PDK layer mapping (poly, diff, metal1).

- Generate LEF file describing cell geometry and pins for place-and-route tools.

---

### 9. Standard Cell Layout & Extraction

- Create inverter layout in Magic using sky130.tech.

- Run extraction to produce a SPICE netlist with parasitics for LVS and post-layout simulation.

---

### 10. Sky130 Tech File Labs

- Combine extracted netlist, Sky130 models, and stimuli into a final SPICE deck.

- Simulate under TT/SS/FF corners to validate fabrication-accurate behavior.

---

### 11. Inverter Characterization

- Measure delay and power under varying voltage, load, and temperature.

- Use .measure in SPICE to capture timing and power metrics for standard cell library generation.

---

### 12. Magic DRC Rules

- Learn Design Rule Checking (DRC) commands (drc check, drc why) to locate and fix layout violations.

- Ensures fabrication-safe geometries.

---

### 13. Sky130 PDK Setup

- Download the open-source SkyWater PDK, which includes tech files, SPICE models, and LEF data.

- Configure Magic using the correct Sky130 tech rules.

---

### 14. DRC Debug & Fix Labs

- Fix poly.9 errors: Adjust poly spacing or add implants.

- Poly resistor spacing: Maintain isolation from diff/tap using guard rings.

- DRC explanation exercise: Interpret rule IDs into geometric issues.

- Tech rule correction: Identify missing or mismatched rules and fix them with version control.

---

## Repository Setup & Tech Configuration

Before designing, prepare the working environment and Sky130 tech files.

```bash
git clone https://github.com/nickson-jose/vsdstdcelldesign
cd vsdstdcelldesign
cp /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech .
ls -la
```

<img width="1836" height="782" alt="image" src="https://github.com/user-attachments/assets/c2d958c1-2706-40b5-a2bc-36146dff08c7" />

---
## Load Layout in Magic
Open the CMOS inverter layout in Magic to explore the device layers and geometries.
```bash
magic -T sky130A.tech sky130_inv.mag &
```

<img width="1782" height="914" alt="image" src="https://github.com/user-attachments/assets/1c6ba79c-0d3a-4102-8228-c181ebc860ed" />

## Running Design Rule Check (DRC)
Magic provides built-in DRC features that verify the design against Sky130A technology constraints.
```bash
drc check
drc why
```
<img width="1273" height="735" alt="image" src="https://github.com/user-attachments/assets/641dfe88-0ea9-47ea-ae35-c3bd207e0240" />

---

## Extracting the SPICE Netlist
Once the layout is DRC-clean, the next step is to generate its SPICE netlist for circuit-level verification.
```bash
extract all
ext2spice cthresh 0 rthresh 0
ext2spice
```

<img width="1273" height="735" alt="image" src="https://github.com/user-attachments/assets/b28f467c-59c6-4573-9d07-d1825575a83d" />

---

## Editing SPICE for Transient Simulation

Modify the generated netlist to include input sources, power rails, and transient analysis commands.
```bash
* SPICE3 netlist for sky130_inv.ext - tech: sky130A

.option scale=0.01u
.include libs/pshort.lib
.include libs/nshort.lib

M1000 Y A VPWR VPWR pshort_model.0 w=37 l=23
M1001 Y A VGND VGND nshort_model.0 w=35 l=23

VDD VPWR 0 3.3V
VSS VGND 0 0V
Va A VGND PULSE(0 3.3 0 0.1ns 0.1ns 2ns 4ns)

.tran 1n 20n
.control
run
.endc
.end
```

<img width="1190" height="717" alt="image" src="https://github.com/user-attachments/assets/9e6afcd8-111e-4df4-aafe-01a2a41c97a8" />

---

## Simulating in NGSPICE
Run the transient analysis and visualize the inverter’s switching waveform.
```bash
ngspice sky130_inv.spice
```

<img width="1836" height="978" alt="image" src="https://github.com/user-attachments/assets/a21b4b80-92fc-46ed-8de3-9d91bd366c2c" />

<img width="1368" height="967" alt="image" src="https://github.com/user-attachments/assets/a30521dd-4c29-437e-a205-5ebac0b4ba32" />

---

## Re-Validation — DRC Clean Confirmation
Once all corrections are made, verify that the layout is now error-free.
```bash
magic -T sky130A.tech sky130_inv.mag &
```

In tkcon 2.3 Main console, run the following command
```bash
drc check
drc why
```
<img width="1360" height="782" alt="image" src="https://github.com/user-attachments/assets/95d75528-930e-4952-9e07-b3907fdc031b" />

---

### Complete Flow Recap

| Step | Description | Tool | Result |
| :---: | :--- | :---: | :--- |
| 1 | Setup repository and Sky130 tech files | **Shell** | Ready workspace |
| 2 | Load inverter layout | **Magic** | Inverter displayed |
| 3 | Perform DRC check | **Magic** | Initial violations fixed |
| 4 | Extract SPICE netlist | **Magic** | `sky130_inv.spice` generated |
| 5 | Add voltage sources & simulation setup | **Text Editor** | Testbench ready |
| 6 | Run transient simulation | **NGSPICE** | Input/output waveforms plotted |
| 7 | Re-run DRC and verify | **Magic** | Layout finalized and DRC-clean |

---

### Key Concepts Learned

| Concept | Description |
| :--- | :--- |
| **Magic Layout** | Open-source VLSI layout tool supporting PDK-based design and rule checking. |
| **DRC Verification** | Validates that layout geometries follow fabrication limits for yield and reliability. |
| **SPICE Extraction** | Converts physical layout into a transistor-level netlist for post-layout analysis. |
| **NGSPICE** | Open-source circuit simulator used for DC and transient analyses. |
| **Delay Measurement** | Determines circuit speed and propagation delays for performance evaluation. |

---

### Session Summary

By completing **Day 3**, you have:

- Designed and visualized a **CMOS inverter layout** in *Magic*  
- Extracted and refined its **SPICE netlist**  
- Simulated and analyzed **transient behavior** in *ngspice*  
- Verified the layout is **DRC-clean** and ready for **standard-cell integration**

---

### Next Up

➡ **Day 4 — Pre-Layout Timing Analysis and Clock Tree Role**

Learn how to:
- Convert standard cells into **LEF** format  
- Perform **Static Timing Analysis (STA)**  
- Understand and apply **Clock Tree Synthesis (CTS)** principles  

---
