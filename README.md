### Post-Synthesis GLS & STA Fundamentals 

### 🔁 Week 2 Recap — Pre-Synthesis Simulation Flow

Before moving to post-synthesis verification, let’s quickly revisit the pre-synthesis flow we established in Week 2.

```bash
# Clone the VSDBabySoC repository
git clone https://github.com/manili/VSDBabySoC.git
cd VSDBabySoC/

# Set up Python virtual environment and install SandPiper
python3 -m venv venv
source venv/bin/activate
pip install pyyaml click sandpiper-saas

# Convert TL-Verilog to SystemVerilog
sandpiper-saas -i ./src/module/*.tlv -o rvmyth.v --bestsv --noline -p verilog --outdir ./src/module/

# Compile and run pre-synthesis simulation
mkdir -p output/pre_synth_sim
iverilog -o output/pre_synth_sim/pre_synth_sim.out -DPRE_SYNTH_SIM -I src/include -I src/module src/module/testbench.v
cd output/pre_synth_sim/
./pre_synth_sim.out
gtkwave pre_synth_sim.vcd
```

**Result:**

![01](./images/01.png))

![02](./images/02.png))

* ✅ Functional verification of the BabySoC RTL using TL-Verilog to Verilog conversion.
* ✅ Waveform visualization of key signals (`CLK`, `reset`, `OUT`, `RV_TO_DAC[9:0]`).
* ✅ Verified that the pre-synthesis simulation produces the correct digital behavior.

---

Next, in **Week 3**, we’ll extend this flow to include:

* **Post-Synthesis Gate-Level Simulation (GLS)** using the synthesized netlist.
* **Static Timing Analysis (STA)** using **OpenSTA** to explore setup/hold checks, slack, and critical-path timing.

---
