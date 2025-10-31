# Inception of open-source EDA, OpenLANE and Sky130 PDK



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

```bash
run_floorplan
```

<img width="1919" height="949" alt="Screenshot 2025-10-31 153755" src="https://github.com/user-attachments/assets/109a1bba-6d33-4a88-bfad-8f43d67f69cd" />

```bash
run_placement
```

<img width="1916" height="964" alt="image" src="https://github.com/user-attachments/assets/cea94322-0fc2-44db-9016-3d7f62e8f770" />

```bash
run_cts
```
photo
```bash
run_routing
```



