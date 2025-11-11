# Good floorplan vs Bad floorplan and Introduction to library cells



```bash
run_floorplan
```

<img width="1919" height="949" alt="Screenshot 2025-10-31 153755" src="https://github.com/user-attachments/assets/109a1bba-6d33-4a88-bfad-8f43d67f69cd" />

<img width="1439" height="993" alt="image" src="https://github.com/user-attachments/assets/dddd2b1f-81ea-46bf-936b-fbffdc024e31" />

```bash
magic -T ~/soc-design-and-planning-nasscom-vsd/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def &
```

<img width="1824" height="958" alt="image" src="https://github.com/user-attachments/assets/226131ec-a334-4ad4-910c-89669f3f8aa7" />

```bash
run_placement
```

<img width="1916" height="964" alt="image" src="https://github.com/user-attachments/assets/cea94322-0fc2-44db-9016-3d7f62e8f770" />

<img width="1108" height="914" alt="image" src="https://github.com/user-attachments/assets/5b75540e-0003-4466-892b-60dcd8ca7d92" />

```bash
magic -T ~/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def &
```
<img width="1834" height="981" alt="image" src="https://github.com/user-attachments/assets/87fd2437-6dc9-4d33-8622-1f179c2a87b0" />

```bash
run_cts
```

<img width="1919" height="941" alt="image" src="https://github.com/user-attachments/assets/d50b6570-cf28-460c-a1de-64f0e4975946" />

<img width="1538" height="989" alt="image" src="https://github.com/user-attachments/assets/659d361e-3c08-4813-860c-3b341aac8bf3" />

<img width="2048" height="2048" alt="image" src="https://github.com/user-attachments/assets/67c89605-299c-46cf-8086-10299bafea2a" />

```bash
run_routing
```

<img width="1917" height="991" alt="image" src="https://github.com/user-attachments/assets/dc5464ff-02ee-4087-b0ae-ef45c4541dcb" />

<img width="2048" height="2048" alt="image" src="https://github.com/user-attachments/assets/22e2abfa-12c4-4fe1-a964-094c4a20f3a2" />


















