# Design library cell using Magic Layout and ngspice characterization

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








