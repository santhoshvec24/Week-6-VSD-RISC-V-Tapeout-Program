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

<img width="1919" height="989" alt="image" src="https://github.com/user-attachments/assets/b2bb40d8-5c01-4987-8b0a-72cee099a960" />

RC extraction is done

<img width="1914" height="990" alt="image" src="https://github.com/user-attachments/assets/59659a16-7b2f-4bc6-9e5a-94f3e2960b03" />



