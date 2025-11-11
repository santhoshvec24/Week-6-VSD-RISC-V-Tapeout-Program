# Pre-layout Timing Analysis and Importance of Good Clock Tree


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













