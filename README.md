# RISC-V tapeout program week 2
We'll try to get a solid understanding of SoC fundamentals and see how to practice functional modelling of the BabySoC using simulation tools (Icarus Verilog &amp; GTKWave)

<details>
	<summary> Part 1 </summary>

##  Throery

# 🚀 VSDBabySoC

This project brings together a complete **System on Chip (SoC)** built around the **RVMYTH** RISC-V processor. it's kind of a miniature computer on a single chip, which'll help to learn and experiment with digital-analog interfacing. 🎓


Cool what's the goal? Create a platform where we can test open-source IP cores simultaneously while learning how digital systems communicate with the analog world—like TVs 📺, speakers 🔊, and mobile devices 📱.


## 🔍 So What Exactly is a System on Chip?

Instead of having separate components scattered across a circuit board, everything gets packed into one tiny chip. That's an SoC!

### 🧩 What's Inside an SoC?

1. **Processor (CPU)** 🖥️
   - Executes instructions and crunches numbers
   - Runs your programs and handles logic

2. **Memory** 💾
   - **RAM**: Temporary storage for active tasks
   - **ROM/Flash**: Permanent storage that survives power-offs

3. **Input/Output Interfaces** 🔌
   - Connects to cameras, USB devices, displays, and sensors
   - Acts as the gateway between your chip and the outside world

4. **Graphics Engine (GPU)** 🎮
   - Renders visuals and animations
   - Powers everything from video playback to gaming

5. **Signal Processors (DSP)** 🎵
   - Handles audio and video processing
   - Cleans up noise, enhances quality, and manages multimedia

6. **Power Management** 🔋
   - Keeps energy consumption in check
   - Critical for battery-powered gadgets

7. **Wireless & Security** 📡
   - Wi-Fi, Bluetooth, encryption modules
   - Varies based on the chip's purpose

![0_uZg3P3cqRcKa7xQb](https://github.com/user-attachments/assets/2cd70c9d-517d-4e24-a1a9-fb83f66dcddc)


### ✨ Why SoCs Rule

- **Compact Design**: Everything fits in your pocket 📏
- **Power Sippers**: Use less energy, last longer 🔋
- **Lightning Fast**: Short distances = speedy data transfer ⚡
- **Cost-Effective**: One chip beats buying many parts 💰
- **Rock Solid**: Fewer components = fewer things that can break 🛡️

### 🌍 SoCs are everywhere! 

- Smartphones & tablets (Apple A-series, Snapdragon, Exynos)
- Smartwatches and fitness trackers
- Smart home devices and IoT sensors
- Gaming consoles (like Nintendo Switch with NVIDIA Tegra)
- Modern cars, TVs, and home appliances

<img width="665" height="512" alt="Screenshot 2025-10-04 at 5 26 05 PM" src="https://github.com/user-attachments/assets/6ae0e895-2c38-49a4-85dd-16b4943f3ec1" />


### 🚧 But comes with it's own challenges

- **Cost** : Goes upto milions of dollars
- **Complex Design**: Fitting everything together requires serious engineering chops (Just think of it, TSMC just the only company who pioneers this complex process)
- **Heat Management**: Cramped components can get toasty 🔥 (for ex: the Iphone heats up a lot while charging or while playing games)
- **Limited Flexibility**: Once fabricated, changes are tough to make
- And many more
<img width="661" height="499" alt="Screenshot 2025-10-04 at 5 36 34 PM" src="https://github.com/user-attachments/assets/1b973bba-1601-4a52-ad3d-21c900b33386" />


## 🎨 Types of SoCs

### 🔧 Microcontroller-Based SoC
Perfect for simple control tasks with minimal power draw. You'll find these in:
- Home appliances (smart thermostats, washing machines)
- Automotive systems (engine control units)
- IoT sensors and wearables

### 💪 Microprocessor-Based SoC
Built for heavy lifting—running operating systems and complex apps:
- Smartphones and tablets
- Portable gaming devices
- Media players

### 🎯 Application-Specific SoC
Custom-built for specialized, high-performance jobs:
- Graphics cards and AI accelerators
- Network routers and switches
- Industrial automation systems
- Financial trading terminals

## SoC design flow
<img width="661" height="515" alt="Screenshot 2025-10-04 at 5 26 28 PM" src="https://github.com/user-attachments/assets/e7614fab-992d-4f9e-8926-f1f76bc8a18d" />




## 🔬 Where does VSDBabySoC come into picture?

VSDBabySoC is a compact RISC-V-based SoC designed for education and experimentation. Built on **Sky130 technology**, it's perfect for learning how digital and analog worlds connect

### 🎭 The Three Main Characters

#### 1️⃣ **RVMYTH - The Brain** 🧠
A customizable RISC-V CPU that handles all the processing. It's open-source, which means you can peek under the hood and modify it. RVMYTH uses its `r17` register to cycle through data values that get sent to the DAC

#### 2️⃣ **PLL - The Heartbeat** 
Generates a stable, synchronized clock signal that keeps everything in perfect timing. Without it, your processor and DAC would be go in chaos!

**Why We Need PLLs:**
- **Clock Distribution**: Long wires cause delays; PLLs compensate for this
- **Jitter Reduction**: Eliminates timing variations in signals
- **Multiple Frequencies**: Different chip sections often need different clock speeds
- **Crystal Accuracy**: Real-world oscillators drift due to temperature, aging, and manufacturing tolerances (measured in parts per million)

**PLL Components:**
- **Phase Detector**: Compares input and output signals, detects phase differences
- **Loop Filter**: Smooths out the error signal
- **Voltage-Controlled Oscillator (VCO)**: Adjusts frequency based on the control voltage

![1600447087142](https://github.com/user-attachments/assets/fb39cdd5-73f3-4d02-b89d-1da30f47455f)


#### 3️⃣ **DAC - The Translator** 🔄
Converts digital values (ones and zeros) into smooth analog signals that real-world devices understand

**VSDBabySoC uses a 10-bit DAC**, meaning it can represent 1,024 different voltage levels (2^10)

**Common DAC Architectures:**
- **Weighted Resistor DAC**: Uses resistors of different values to create the analog output
- **R-2R Ladder DAC**: Uses a repeating pattern of resistors (R and 2R values) for simpler, more scalable designs

---

## ⚙️ How VSDBabySoC Works

Here's the flow from power-on to analog output:

1. **🔌 Power Up & Clock Generation**
   - BabySoC receives an input signal
   - The PLL kicks in and generates a stable clock
   - All components synchronize to this clock signal

2. **🧮 Data Processing**
   - RVMYTH executes instructions
   - Values cycle through the `r17` register
   - Data gets prepared for analog conversion

3. **📡 Analog Signal Output**
   - The DAC receives digital values from RVMYTH
   - Converts them into analog signals
   - Output can drive speakers, displays, or other analog devices
   - Results are saved to a file called `OUT`

---



</details>

<details>
<summary>Part 2</summary>


## Labs


# 🚀 VSDBabySoC - Functional Modeling and Simulation

This is a hands-on lab demonstrating functional modeling of a compact RISC-V-based System-on-Chip (SoC) that integrates a processor core, Phase-Locked Loop (PLL), and Digital-to-Analog Converter (DAC). The goal is to verify reset operations, clocking, and dataflow through simulations 🔬

***

## 📋 Project Overview

**Key Components:**

- 🔹 **RVMYTH (RISC-V Core)**: A 5-stage pipelined processor written in TL-Verilog (`rvmyth.tlv`), which executes instructions and outputs data via register r17
- 🔹 **AVSDPLL**: PLL module (`avsdpll.v`) that generates a stable clock (CLK) from reference inputs (REF, VCO_IN)
- 🔹 **AVSDDAC**: 10-bit DAC (`avsddac.v`) that converts digital data from the RISC-V core (via `RV_TO_DAC[9:0]` bus) to analog output (OUT)

The SoC flow: Reset initializes everything ➡️ PLL locks and clocks the core ➡️ Core executes code and sends data to DAC ➡️ DAC produces analog signals. Both pre-synthesis (RTL) and post-synthesis (gate-level) simulations confirm functional correctness ✅

### 🛠️ Tools Used

- 🔧 **Icarus Verilog (iverilog)**: Compiles/simulates Verilog
- 👁️ **GTKWave**: Views/analyzes VCD waveforms
- ⚙️ **SandPiper-SaaS**: TL-Verilog → Verilog conversion
- 🏗️ **Yosys**: RTL synthesis to gates 



***

## ⚙️ Setup & Workflow 


### 🛠️ Tool Installation

1. **Icarus Verilog \& GTKWave**: `brew install icarus-verilog gtkwave` (for compilation and waveform viewing)
2. **SandPiper-SaaS**: `npm install -g sandpiper-saas` (compiles TL-Verilog to Verilog)
3. **Yosys**:
```
 git clone https://github.com/YosysHQ/yosys.git
 brew install cmake gcc gawk tcl-tk libtool bison flex make
 brew install graphviz
 cd yosys
 git submodule update --init
 make
```
5. Verified: `iverilog -V`, `gtkwave --version`, `yosys -V`

### 📁 Project Setup

- Cloned base structure from reference repos (https://github.com/manili/VSDBabySoC.git)
- Organized files: `src/module/` (Verilog/TL-Verilog files), `src/include/` (headers like `sandpiper.vh`), `src/lib/` (Sky130 liberty files), `src/gls_model/` (gate primitives), `src/script/` (Yosys script `yosys.ys`)
- Created `output/` for results



### 🔧 Makefile Explanation

The `Makefile` automates the entire flow: TL-Verilog compilation, pre/post-synthesis simulations, and synthesis. It uses variables for paths (e.g., `SRC_PATH = src`, `OUTPUT_PATH = output`) and phony targets for clean builds

**Full Makefile Code** 

```makefile

SRC_PATH = src
LIB_PATH = $(SRC_PATH)/lib
GDS_PATH = $(SRC_PATH)/gds
LEF_PATH = $(SRC_PATH)/lef
SDC_PATH = $(SRC_PATH)/sdc
MODULE_PATH = $(SRC_PATH)/module
INCLUDE_PATH = $(SRC_PATH)/include
LAYOUT_CONF_PATH = $(SRC_PATH)/layout_conf
OUTPUT_PATH = output


STA_PATH = $(OUTPUT_PATH)/sta
SYNTH_PATH = $(OUTPUT_PATH)/synth
COMPILED_TLV_PATH = $(OUTPUT_PATH)/compiled_tlv
PRE_SYNTH_SIM_PATH = $(OUTPUT_PATH)/pre_synth_sim
POST_SYNTH_SIM_PATH = $(OUTPUT_PATH)/post_synth_sim

.PHONY: all sim clean pre_synth_sim post_synth_sim synth

all: sim

sim: pre_synth_sim post_synth_sim

clean:
	rm -rf $(OUTPUT_PATH)

# TL-Verilog compilation & Pre-synthesis simulation
pre_synth_sim: $(COMPILED_TLV_PATH)
	if [ ! -f "$(PRE_SYNTH_SIM_PATH)/pre_synth_sim.vcd" ]; then \
		mkdir -p $(PRE_SYNTH_SIM_PATH); \
		iverilog -o $(PRE_SYNTH_SIM_PATH)/pre_synth_sim.out -DPRE_SYNTH_SIM \
			$(MODULE_PATH)/testbench.v \
			-I $(INCLUDE_PATH) -I $(MODULE_PATH) -I $(COMPILED_TLV_PATH); \
		cd $(PRE_SYNTH_SIM_PATH); ./pre_synth_sim.out; \
	fi

$(COMPILED_TLV_PATH):
	mkdir -p $(COMPILED_TLV_PATH)
	sandpiper-saas -i $(MODULE_PATH)/rvmyth.tlv -o rvmyth.v \
		--bestsv --noline -p verilog --outdir $(COMPILED_TLV_PATH)

# Synthesis with local Yosys
synth: $(COMPILED_TLV_PATH)
	if [ ! -f "$(SYNTH_PATH)/vsdbabysoc.synth.v" ]; then \
		mkdir -p $(SYNTH_PATH); \
		cd $(SRC_PATH); yosys -s script/yosys.ys | tee ../$(SYNTH_PATH)/synth.log; \
	fi

# Post-synthesis simulation
post_synth_sim: synth
	if [ ! -f "$(POST_SYNTH_SIM_PATH)/post_synth_sim.vcd" ]; then \
		mkdir -p $(POST_SYNTH_SIM_PATH); \
		iverilog -o $(POST_SYNTH_SIM_PATH)/post_synth_sim.out -DPOST_SYNTH_SIM -DFUNCTIONAL -DUNIT_DELAY=#1 \
			-I $(INCLUDE_PATH) -I $(MODULE_PATH) -I $(SRC_PATH)/gls_model -I $(SYNTH_PATH) \
			$(MODULE_PATH)/testbench.v; \
		cd $(POST_SYNTH_SIM_PATH); ./post_synth_sim.out; \
	fi
	
```

**How It Works:**

- **Pre-synth (`make pre_synth_sim`)**: Compiles `rvmyth.tlv` to `rvmyth.v`, runs RTL sim with `-DPRE_SYNTH_SIM` (testbench includes RTL modules), dumps VCD
- **Synthesis (`make synth`)**: Yosys reads Verilog/liberty files, synthesizes to gate netlist (`vsdbabysoc.synth.v`), logs stats (e.g., gate count)
- **Post-synth (`make post_synth_sim`)**: Compiles netlist with `-DPOST_SYNTH_SIM` (testbench includes gates/primitives), adds unit delays for timing

***

## 📝 Lab Steps Followed

### 1️⃣ Clone the BabySoC Project Repo

```bash
https://github.com/manili/VSDBabySoC.git
cd VSDBabySoC
```


### 2️⃣ Compile the BabySoC Verilog Modules using iverilog

- TL-Verilog first: `sandpiper-saas` handles `rvmyth.tlv`
- Then: `make pre_synth_sim` compiles everything (testbench + modules) into executable


### 3️⃣ Simulate and Generate .vcd Waveform Files

- Pre-synth: creates `output/pre_synth_sim/pre_synth_sim.vcd`
- Post-synth: `make post_synth_sim` synthesizes first, then gate-level sim → `output/post_synth_sim/post_synth_sim.vcd`


### 4️⃣ Open .vcd Files in GTKWave and Analyze

```bash
cd output/pre_synth_sim && gtkwave pre_synth_sim.vcd
```

<img width="1142" height="726" alt="Screenshot 2025-10-01 at 1 02 42 PM" src="https://github.com/user-attachments/assets/13f094c9-843d-40bd-8bb4-617549836d3a" />

*** 

```
cd output/post_synth_sim && gtkwave post_synth_sim.vcd
```
<img width="1142" height="761" alt="Screenshot 2025-10-01 at 3 33 41 PM" src="https://github.com/user-attachments/assets/9aee0f38-3b7b-4511-9bd2-264ebfe6b250" />



- **Reset**: Check initialization (all zeros during assert)
- **Clocking**: Verify PLL CLK stability 
- **Dataflow**: Trace RISC-V r17 → RV_TO_DAC → DAC OUT (incrementing values)


***

## 📊 Simulation Results \& Analysis

### 🔄 Reset Operation (Pre-Synthesis)

Reset (high) zeros registers (r17=0, OUT=0V). Deassert starts PLL and core fetch. Verifies clean initialization—no hanging states

### 🕒 Clocking (Pre-Synthesis)

PLL enables after ENb_VCO/REF, locks to ~10MHz CLK. Stable edges drive core/DAC sync. No jitter confirms PLL reliability

### 📈 Dataflow Between Modules (Pre-Synthesis)

Core executes (addi increments r17), sends via RV_TO_DAC[9:0] to DAC D input. OUT scales analog. Proves end-to-end functionality. (Trace: r17 → bus → OUT)

### ⚡ Post-Synthesis Comparison

Gate-level (Sky130 cells) matches RTL: Same sequences, No logic changes—synthesis success 

<img width="1043" height="736" alt="Screenshot 2025-10-04 at 5 45 30 PM" src="https://github.com/user-attachments/assets/b224a30e-8038-45fd-baeb-e30783cb2296" />




## 📂 File Structure

```
VSDBabySoC/
├── Makefile                 # 🚀 Build automation (pre/post-synth sims)
├── README.md                # 📖 This guide
├── src/                     # Source code
│   ├── module/              # vsdbabysoc.v, rvmyth.tlv, avsdpll.v, avsddac.v, testbench.v
│   ├── include/             # .vh headers (sandpiper.vh)
│   ├── lib/                 # .lib files (Sky130 std cells)
│   ├── gls_model/           # primitives.v, sky130_fd_sc_hd.v
│   └── script/              # yosys.ys (synthesis script)
├── output/                  # 🛠️ Results (gitignored large files)
│   ├── compiled_tlv/        # rvmyth.v (from TL-Verilog)
│   ├── pre_synth_sim/       # RTL VCD/logs
│   ├── post_synth_sim/      # Gate-level VCD/logs
│   └── synth/               # vsdbabysoc.synth.v + log

```

Disclaimer: Content has been refined with help of generative AI for effiecincy n clean look. Claude 4.5 has been used in code debugging

