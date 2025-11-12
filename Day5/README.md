# Final Step for RTL to GDS using tritonRoute and OpenSTA

## Introduction to Maze Routing – Lee’s Algorithm
**Concept:**  
Lee’s algorithm is a grid-based maze routing method that finds the shortest path between two points using a breadth-first search (wave expansion). Once the destination (sink) is reached, it backtracks to form the route.  

**Why it matters:**  
It guarantees a valid path if one exists, making it foundational for understanding grid-based routing and modern rip-up-and-reroute methods.  

**Practical notes:**  
While accurate, it is computationally intensive and memory-heavy, making it slow for large designs.

---

## Lee’s Algorithm — Conclusion
**Concept:**  
Although robust and reliable, Lee’s algorithm doesn’t scale efficiently for full-chip routing.  

**Why it matters:**  
Modern tools like **TritonRoute** use heuristic-based and variant maze routing algorithms to achieve faster and more efficient results.

---

## Design Rule Check (DRC)
**Concept:**  
DRC ensures the layout complies with foundry-specified geometric constraints (e.g., minimum spacing, metal width, via enclosure, and overlaps).  

**Why it matters:**  
Passing DRC is mandatory before tape-out; any violation makes a design non-manufacturable.  

**Practical notes:**  
Use **Magic** or **KLayout** to detect and correct DRC errors before final GDS generation.

---

## Power Distribution Network (PDN) — Lab Steps
**Concept:**  
The PDN provides a robust power delivery structure using hierarchical connections: global rails, metal stripes, and cell-level links.  

**Why it matters:**  
Ensures stable power supply, minimizes IR-drop, and maintains signal integrity.  

**Practical notes:**  
- Reserve specific metal layers for VDD/VSS distribution.  
- Add via arrays and power straps for low-impedance paths.  
- Maintain symmetry and coverage across the die.

---

## Connecting Power Straps to Standard Cells
**Concept:**  
Connect global power rails to the power pins of individual standard cells using metal tracks and vias.  

**Why it matters:**  
Provides reliable and consistent power delivery to every cell in the design.  

**Practical notes:**  
Include power rings around the core area, ensure via redundancy, and add decoupling capacitors where necessary.

---

## Global & Detailed Routing using TritonRoute
**Concept:**  
Routing occurs in two phases:
- **Global Routing:** Coarse assignment of routing regions and metal layers.  
- **Detailed Routing:** Exact wire placement, via generation, and DRC compliance.  

**Why it matters:**  
Proper configuration ensures efficient routing with minimal congestion and DRC errors.  

**Practical notes:**  
Set routing layer preferences, via rules, and provide routing guide files for optimal results.

---

## TritonRoute Features

### Feature 1 – Route Guide Compliance
**Concept:**  
TritonRoute can follow pre-generated global routing guides to maintain preferred routing channels and reduce congestion.  
**Why it matters:**  
Improves predictability and routing quality.  
**Practical notes:**  
Use guide files from the global router to direct detailed routing.

### Feature 2 & 3 – Inter-Guide and Multi-Layer Connectivity
**Concept:**  
Supports connectivity across multiple guides and transitions between metal layers using vias while following DRC and layer preferences.  
**Why it matters:**  
Enables complete and reliable interconnect routing across the chip.  
**Practical notes:**  
Define allowed metal stacks and via types in the routing configuration.

---

## Handling Connectivity and Congestion in TritonRoute
**Concept:**  
TritonRoute employs incremental **rip-up and reroute**, **conflict resolution**, and **localized maze searches** to resolve blocked or congested areas.  
**Why it matters:**  
Ensures all nets are routed while maintaining DRC compliance.  
**Practical notes:**  
Analyze `route_summary.log` and overflow reports to fine-tune routing parameters.

---

## Routing Topology & Post-Route Outputs
**Concept:**  
Routers compute net topologies (e.g., Steiner trees) for multi-pin nets, generating the final routed design.  

**Why it matters:**  
Post-route outputs are used for **sign-off verification** (DRC, LVS, STA, and fabrication).  

do all the process as we done in Day1 to Day4 and then 

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

---

## Conclusion

Day 5 provided a deep understanding of the routing process, design verification, and power distribution in VLSI design.  
Starting with **Lee’s algorithm**, we explored the fundamentals of grid-based maze routing — the basis for modern routing techniques used in tools like **TritonRoute**.  

We learned the importance of **Design Rule Checks (DRC)** to ensure the layout adheres to manufacturing rules, and how **Power Distribution Networks (PDN)** maintain stable voltage and prevent IR-drop across the chip.  

Finally, the session introduced **TritonRoute’s capabilities**, including global and detailed routing, route guide handling, multi-layer connectivity, and congestion management.  
The day concluded with the generation of key post-route outputs — **DEF, GDS, and SPEF files** — which are essential for timing analysis and tape-out readiness.  

In summary, this day emphasized how accurate routing, robust power planning, and strict rule adherence form the foundation of a successful and manufacturable integrated circuit design.
