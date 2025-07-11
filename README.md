
# Chipstronics T2B Converter Design (SSCS Chipathon 2025 Proposal)

We're **Chipstronics**, a team in the Digital Track of **SSCS Chipathon 2025**.  
Our goal? To build a solid **T2B (Thermometer to Binary) converter**.  
This tool is super important for making complex chip designs easier to manage, especially during verification and simulation.  
We think it'll really help digital designers tackle tricky projects.

## Why This Matters (Background)
In chip design, things get complex fast. Simulating entire systems at the transistor level takes forever.  
Behavioral models, on the other hand, are high-level views that speed up simulations big time.

The trick is accurately turning those detailed transistor designs into high-level behavioral models.  
This "**Thermometer to Binary**" (T2B) conversion is key for quick design changes and thorough testing.  
Our T2B converter aims to automate this, making debugging faster and design completion smoother, even with huge libraries and custom blocks.

## What It Is (Overview)
Our T2B converter is a digital block designed to take detailed transistor data and turn it into simpler, behavioral models.  
A core part of it is an **8:3 priority encoder**. This encoder helps us sort and prioritize incoming signals or internal states.

Think of it this way: raw input comes in, our converter processes it (using things like the priority encoder), and then spits out a formatted behavioral model.

## Specifications

| Specification       | Value | Unit | Notes                                           |
|---------------------|-------|------|-------------------------------------------------|
| Operating Voltage   | 3.3   | V    | Works with GF180MCU D library standards         |
| Maximum Frequency   | 100   | MHz  | Our target speed for efficient conversions      |
| Cell Height         | 9     | Layers | Chose 9 layers |
| Input ports (proposed) | 8  | Ports | For data and control signals  |
| Output ports (proposed) | 4 | Ports | For converted data and status                   |
| Cell Area           | TBD   | um²  | Will know after layout and optimization         |

## How It Works (Design & Work Details)
Our T2B converter will be fully static, using standard logic gates for reliable performance.  
We'll use common CMOS logic (PFET and NFET transistors), carefully optimizing it for small size, high speed, and strong output drive.

The **8:3 Priority Encoder** is a crucial piece. It makes sure that if several signals come in at once, the one with the highest priority gets handled first.

While a typical 8:3 priority encoder uses simple AND, OR, and NOT gates, our design might use more complex building blocks if other parts of the T2B converter need arithmetic operations.  
This could mean sharing some underlying logic components, possibly including elements that full adders are built from, for overall efficiency.

### 8:3 Priority Encoder Truth Table

| Inputs (D7–D0)         | Outputs (Q2 Q1 Q0) | Valid (V) |
|------------------------|--------------------|------------|
| 00000000               | x x x              | 0          |
| xxxxxxx1               | 000                | 1          |
| xxxxxx10               | 001                | 1          |
| xxxxx100               | 010                | 1          |
| xxxx1000               | 011                | 1          |
| xxx10000               | 100                | 1          |
| xx100000               | 101                | 1          |
| x1000000               | 110                | 1          |
| 10000000               | 111                | 1          |

> `'x'` means "don't care." If a higher priority input (like D7=1) is active, lower priority inputs (D0–D6) don't matter.  
> **Valid (V)** is '1' if any input is active, and '0' if all inputs are '0'.

## Our Team & Timeline

We've split up the work:

- **Core T2B Logic Design & Schematic**: Johan, Farhan
- **Overall Layout & Verification**: Mohith, Zeeshan

We'll follow a clear timeline over three months:

1. Proposal & Initial Specs *(where we are now!)*  
2. Schematic Design & Pre-Layout Simulation  
3. Layout Design & Post-Layout Verification  
4. Standard Cell Characterization & Documentation  

## What We Hope To Achieve

We're really hoping our T2B converter design becomes a useful part of the GF180MCU standard cell library.  
By giving designers an efficient way to convert transistor-level designs to behavioral models, we aim to help speed up design cycles, make verification more reliable, and ultimately, build stronger chips.  
We hope our work gets accepted and helps the broader chip design community.

> This project is built using a template set up for the **GlobalFoundries 180nm PDK (gf180mcuD)**, following a common open-source ASIC workflow.
