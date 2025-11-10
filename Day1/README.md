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

RC extraction is done

<img width="1914" height="990" alt="image" src="https://github.com/user-attachments/assets/59659a16-7b2f-4bc6-9e5a-94f3e2960b03" />



