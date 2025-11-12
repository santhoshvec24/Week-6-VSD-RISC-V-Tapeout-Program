# Pre-layout Timing Analysis and Importance of Good Clock Tree

## Layout & Library Preparation
- **Grid-to-Track Conversion:** Maps layout geometry to routing tracks so routers follow correct metal layers and spacing. Output: `tracks.lef`.
- **Magic Layout → Std Cell LEF:** Exports cell boundary, pins, and sites to LEF so placer/router can position cells accurately.
- **Timing Libraries (.lib):** Contain timing arcs and power data. Add new cells by updating `.lib`, `.lef`, and gate-level models in synthesis/STA setup.

---

## Delay Tables & STA Concepts
- **Delay Tables:** 2D lookup of delay vs. input slew and output load. Used by STA/synthesis for timing estimation.
- **Usage 1:** STA interpolates values to compute path delay and slack (positive/negative).
- **Usage 2:** Multiple `.lib` files model PVT corners; parasitics combine with delay data for final timing accuracy.

---

## Synthesis Optimization
- Adjust effort level, frequency targets, and include custom cells (e.g., `vsdinv`) to improve slack.
- Techniques: retiming, pipeline insertion, `set_max_area` tuning, or logic rebalancing.

---

## Static Timing Analysis (STA)
- **Setup Analysis:** Checks data arrival before flip-flop setup window.  
  *OpenSTA commands:* `read_liberty`, `read_verilog`, `create_clock`, `report_timing`.
- **Clock Jitter & Uncertainty:** Models variation and skew using `set_clock_uncertainty`.
- **Post-Synthesis STA:** Run timing with netlist + `.lib` (+ `SPEF` if available) to verify design before placement.

---

## Timing Closure & ECO
- Reduce violations by resynthesis, logic optimization, faster cells, or pipelines.
- **ECO (Engineering Change Order):** Quick post-synthesis fixes—add buffers, modify constraints, or swap cells.

---

## Clock Tree Synthesis (CTS)
- **TritonCTS:** Builds buffered H-tree or mesh for balanced clock distribution. Configure root, buffer types, and regions.
- **Signal Integrity:** Use shielding and spacing to reduce crosstalk, jitter, and skew on clock nets.
- **CTS Verification:** Check skew, latency, and setup/hold margins via `report_clock -skew` and `report_timing`.

---

## Real-Clock Timing Analysis
- **Setup (Post-CTS):** Uses actual clock insertion delays for accurate slack computation.
- **Hold Analysis:** Ensures data stability after capture; fix with delay buffers or clock skew adjustments.
- **OpenSTA Flow:** Load post-CTS netlist + corner `.lib` + `SPEF`; run `report_timing -setup/-hold`.

---

## Buffer Size Impact Study
- Larger CTS buffers ↓ skew but ↑ latency/power.  
- Explore trade-offs by sweeping buffer sizes and analyzing resulting setup/hold slacks.

---

In console area, type the following
```
help grid
```
<img width="1397" height="837" alt="image" src="https://github.com/user-attachments/assets/c3e9e112-22e8-4896-9fe1-c2fada1e517e" />

---

## Port Attributes Configuration
**Port Properties:**

- Port Class: Input, Output, Inout
- Port Use: Signal, Power, Ground, Clock
- Layer Attachment: Which metal layer the port connects to
- Port Name: A, Y, VPWR, VGND

---

## Port Class and Use Settings
```
grid 0.46um 0.34um 0.23um 0.17um
whats
```

<img width="1772" height="982" alt="image" src="https://github.com/user-attachments/assets/337bdd0d-adae-48c8-9862-62f8e4bd5daf" />

in console
```
save sky130_vsdinv.mag
lef write
```

<img width="1520" height="996" alt="image" src="https://github.com/user-attachments/assets/980a9213-6c93-438e-ab6d-402478091393" />

Viewing Generated LEF File
Commands to Open LEF:

```bash
cd vsdstdcelldesign
less sky130_vsdinv.lef
```
Opening LEF File

<img width="1522" height="982" alt="image" src="https://github.com/user-attachments/assets/813e1af0-4ef9-47fa-815c-63bb47ba3f26" />

```bash
cp sky130_vsdinv.lef ~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/
```
and also do the same for the following files or just copy and paste it in the src directory

<img width="1196" height="621" alt="image" src="https://github.com/user-attachments/assets/96399b3b-fecb-4fb8-9047-a384bfcc799a" />

Enter into `~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src`
```bash
ls -ltr
```

<img width="1622" height="991" alt="image" src="https://github.com/user-attachments/assets/5eee95ec-2e06-436d-86fe-9a94339ee2e8" />

in picorv32a directory 
```bash
gedit config.tcl
```
edit it as given below
```tcl
# Design
set ::env(DESIGN_NAME) "picorv32a"

set ::env(VERILOG_FILES) "./designs/picorv32a/src/picorv32a.v"
set ::env(SDC_FILE) "./designs/picorv32a/src/picorv32a.sdc"

set ::env(CLOCK_PERIOD) "5.000"
set ::env(CLOCK_PORT) "clk"

set ::env(CLOCK_NET) $::env(CLOCK_PORT)

set ::env(LIB_SYNTH) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__typical.lib"
set ::env(LIB_FASTEST) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__fast.lib"
set ::env(LIB_SLOWEST) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__slow.lib"
set ::env(LIB_TYPICAL) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__typical.lib"
set ::env(EXTRA_LEFS) [glob $::env(OPENLANE_ROOT)/designs/$::env(DESIGN_NAME)/src/*.lef]

set filename $::env(OPENLANE_ROOT)/designs/$::env(DESIGN_NAME)/$::env(PDK)_$::env(STD_CELL_LIBRARY)_config.tcl
if { [file exists $filename] == 1} {
	source $filename
}
```

as we know that just overwrite the run folder which contains all the process and files by using the commands in day 1
```
docker
...
prep -design picorv32a -tag 10-11_13-33 -overwrite
```
### Adding Custom LEF to Merged LEF
Additional Commands:
```bash
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs
```

### Running Synthesis with Custom Cell
Synthesis Command:
```bash
run_synthesis
```

<img width="1836" height="991" alt="image" src="https://github.com/user-attachments/assets/a131595b-0398-4675-b8a1-97cadc3b485f" />

---

### Summary Table
| Phase | Key Task | Tool | Output |
|--------|-----------|------|--------|
| Layout prep | Grid→track, LEF export | Magic | `tracks.lef`, `stdcell.lef` |
| Lib setup | Add timing data | Yosys / STA | `.lib` integration |
| STA | Analyze setup/hold | OpenSTA | Timing reports |
| CTS | Build & verify tree | TritonCTS | DEF with buffers |
| Optimization | Fix violations | Synthesis / ECO | Improved slack |

---






