# Final Step for RTL to GDS using tritonRoute and OpenSTA

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




