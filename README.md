
## Overview
In this project, a 5-bit Carry Lookahead Adder is first designed and simulated in ngspice, then implemented as a physical layout in MAGIC, followed by post-layout simulation to verify performance. The same adder is also implemented in Verilog for RTL-level functional verification.

## Design Flow

1. **Schematic Design (ngspice)**
    - Used [NGSPICE/TSMC_180nm.txt] technology.
   - Designed the individual gates at transistor level and verified functionality
   - Used the verified gates to build the CLA.

2. **Layout (MAGIC)**
   - Converted the schematic into a physical layout using MAGIC.
   - Extracted the layout netlist (including parasitics) and re-ran simulation in ngspice to verify post-layout behavior matched the schematic-level results.

3. **RTL (Verilog)**
   - Implemented the same 5-bit CLA behaviorally/structurally in Verilog.
   - Verified functional correctness against expected outputs using a testbench.
   
## Tools Used

- **ngspice** — circuit simulation
- **MAGIC VLSI** — layout design and extraction
- **Verilog** (+ [simulator used, e.g. Icarus Verilog / ModelSim]) — RTL design and testbench simulation

