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















