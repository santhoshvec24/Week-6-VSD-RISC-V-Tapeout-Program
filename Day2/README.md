# Good floorplan vs Bad floorplan and Introduction to library cells



```bash
run_floorplan
```

<img width="1919" height="949" alt="Screenshot 2025-10-31 153755" src="https://github.com/user-attachments/assets/109a1bba-6d33-4a88-bfad-8f43d67f69cd" />

<img width="1439" height="993" alt="image" src="https://github.com/user-attachments/assets/dddd2b1f-81ea-46bf-936b-fbffdc024e31" />

Then enter into the directory `~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/10-11_15-34/results/floorplan`

```bash
magic -T ~/soc-design-and-planning-nasscom-vsd/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def &
```

<img width="1452" height="994" alt="image" src="https://github.com/user-attachments/assets/bab69a30-2f04-4903-8c61-6bc6eead11da" />

<img width="1829" height="978" alt="image" src="https://github.com/user-attachments/assets/b80a3a9f-ce1e-459c-bf94-55922df72ca4" />

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

```bash
run_cts
```

<img width="1919" height="941" alt="image" src="https://github.com/user-attachments/assets/d50b6570-cf28-460c-a1de-64f0e4975946" />

<img width="1538" height="989" alt="image" src="https://github.com/user-attachments/assets/659d361e-3c08-4813-860c-3b341aac8bf3" />

Then enter into the directory `~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/10-11_15-34/results/cts`

```bash
magic -T ~/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.cts.def
```
<img width="997" height="913" alt="image" src="https://github.com/user-attachments/assets/34d599ea-b96a-4ea8-93f0-9674e7aab9d4" />

<img width="1833" height="997" alt="image" src="https://github.com/user-attachments/assets/f1dc0d50-6bfa-47f5-ad31-0326a2542ed1" />

```bash
run_routing
```

<img width="1917" height="991" alt="image" src="https://github.com/user-attachments/assets/dc5464ff-02ee-4087-b0ae-ef45c4541dcb" />

<img width="2048" height="2048" alt="image" src="https://github.com/user-attachments/assets/22e2abfa-12c4-4fe1-a964-094c4a20f3a2" />

Then enter into the directory `~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/10-11_15-34/results/routing`
 
```bash
magic -T ~/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.def &

```

<img width="1799" height="986" alt="image" src="https://github.com/user-attachments/assets/b4cbb7e8-3d7b-49b4-8d3d-4585f11fb9ab" />

<img width="1832" height="987" alt="image" src="https://github.com/user-attachments/assets/2496870a-f973-4b81-aa96-1f5411d03ea9" />

tkcon 2.3 Main cocnsole view:

<img width="1702" height="994" alt="image" src="https://github.com/user-attachments/assets/be8d3404-820d-405a-9433-96ee928342c0" />















