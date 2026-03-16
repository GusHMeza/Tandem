# Tandem
**Xilinx ZYNQ 7000 based compute module**
Work in progress 🛠

_As the final deliverable to complete FEDEVEL: High Speed Digital Hardware Design course by instructor Phil Salmony._

Since form factor was free to chose, I picked 150x100 mm or less as a target based on a rough estimate of how big of a rectangle could fit all the components and went from there. Next, worked my way through layout with rough calculations to get a sense of interconnect length and layer distribution and finally refined the design based on detailed calculations and simulation work. 

**Compute power**

Xilinx Zynq 7000 series SoC, Part Number: 

**Comunications & Networking:**

1 X Gigabit Ethernet

1 X USB 2.0 (USB On-the-go compatible)

**Configuration**

1 X JTAG interface

**Memory**

2 X DDR Gen 3 low power (16-bit wide data bus) components

1 X 8 Gb of eMMC component

**Power** 

10W (5V) power supply

**Expansion connectors**

2 X Mezzanine connectors (break out some I/O from the Zynq 7000)


Front

<img width="795" height="564" alt="image" src="https://github.com/user-attachments/assets/dad30d31-ed39-4bdc-b585-553b54545ddd" />

Back

<img width="762" height="564" alt="image" src="https://github.com/user-attachments/assets/389d7ed5-5b39-48fc-bd46-af98ceaedce5" />

# Signal Integrity

**Target interconnects & requirements**

The PCB deisgn is mainly driven by the DDR Gen 3 single-ended signals and differential clocks as they have have the highest speed requirements. The selected stackup shall also accomodate a Gigabit Ethernet transciever, with 1 GHz differencial signaling, and a USB PHY close to the SoC.

| Timing Parameters |  |
| --- | --- |
| Transfer rate | 1886 MT/s |
| Clock rate | 0.9 GHz |
| Signal period | 1ns period |

| DDR drivers | | |
| --- | --- | --- |
| Static discipline | Unit/note ||
| VTT | 0.675 |V|
| Vih(ac) | 135 mV |above VTT|
| Vil(ac) | -135 mV |below VTT|
| --- | --- | --- |
| Specification | Unit ||
| C @ 1 GHz | 2 |pF|
| Over/under shoot | 0.1 |V/ns|
| Single ended slew rate max | 5 |V/ns|

| Driver output impedance | | |
| --- | --- | --- |
| Zo | Unit |Note|
| 34.3 | Ohms |Default|
| 40 | Ohms |Alternate|

**Stackup selection**

The standard 10L PCB build-up from PCB way was selected, as their overall pricing is cheap and their capabilities seem sufficient using their 'low difficulty to manufacture' specifications.

<img width="470" height="1249" alt="image" src="https://github.com/user-attachments/assets/10b3ddf7-4f45-4a70-ad24-1cfabd29cc03" />

The layer assignment goes as below, and the expected characteristic impedances obtained from it were calculated using a spreadsheet and the formulae from Hall S., Hall G. and McCall J., High Speed Digital System Design, 2001, Wiley.

Layer assignment considers the DDR control signals are routed more towards the back side of the board as termination resitors are placed on the back side of the board and this layer assignment offers a logical channel architecture. The control signals are intended to have a GND plane above and below to maximize SI. 

DDR data signals are routed on the top layer to obtain faster propagation due to having no dielectric material above, as well as to allocate them sufficient space for them to fan out as needed. Routing DDR data and DDR control lines on the same layer seemed impractical as they are difficul to fan out given the current pin assignment on the CLG400 package.
  
<img width="1435" height="639" alt="image" src="https://github.com/user-attachments/assets/ac9d0ee5-4f5b-4ac2-a8b3-3d87c38d6255" />


**Loss characterization**

Two package models were developed for the Zynq 7000, one considering a generic 25 um Au wire bond on a worst case length for the 17x17mm package and another one considering 90um C4 bumps with a package via in series. An online calculator was used to approximate RLC values for these structures, and the channel was simulated in SPICE software that offest S-parameter visualization (QUCS).

1st package model (generic wire-bond package technology)

<img width="895" height="655" alt="image" src="https://github.com/user-attachments/assets/5a1fa145-b338-4501-92b0-a2f5d718b320" />

2nd package model (C4 bumps used on higher speed packages)

<img width="877" height="636" alt="image" src="https://github.com/user-attachments/assets/81173986-be1c-41b2-9e1c-a92797900233" />

_Conclusion_

-For the frequency of interest for the DDR interface (1 GHz) it is not feasible to typicall wire bond technology, as it causes that the majority of the signal's energy content is reflected back to the source at the frequency of interest. 

-Assuming the Zynq 7000's package uses C4 bumps, the SPICE simulation that considers the C4 bump in series with a package via, one fan out via, the PCB trace and one last connection via shows that insertion loss is -0.498 dB and return loss is -9.659 dB.

To verify if this is a feasible design, the loss budget is calculated below.

| Loss budget | | |
| --- | --- | --- |
| Value | Unit |Note|
| 0.675 | V |VTT|
| 0.135 | V (above VTT) |Vhigh|
| 0.81 | V |Vhigh|
| 0.54 | V |Vdd-Vhigh = V_loss margin|
| -0.9691 | dB |10*log10(V_loss margin / VTT)|

Per the calculations above, singal loss @ 1 GHz is of -0.498 dB is within the loss budget of -0.9691 dB, assuming the IC package uses C4 bumps type packaging.

**Crosstalk estimations**

To account for routing density, the potential crosstalk on the traces was evaluated using the provided IBIS models for the Zynq 7000 on Xilinx's website and a series of circuit models created to simulate cross talk and cross talk induced time delays.

This is work in progress...

<img width="1107" height="257" alt="image" src="https://github.com/user-attachments/assets/c36eaf12-419a-498e-9522-740d7f5a260d" />

<img width="780" height="412" alt="image" src="https://github.com/user-attachments/assets/e5560622-15a3-4f4b-a12f-74a8d096a200" />

<img width="1103" height="525" alt="image" src="https://github.com/user-attachments/assets/078113b0-bf0b-4bd0-941c-a8f710a232f6" />

<img width="735" height="383" alt="image" src="https://github.com/user-attachments/assets/1795a6c5-f55d-49fa-91cd-4898e94a7fb4" />

# Layout

<img width="1180" height="857" alt="image" src="https://github.com/user-attachments/assets/2a90e0fe-653a-403d-8aaf-c53fe55d8f71" />

<img width="1174" height="855" alt="image" src="https://github.com/user-attachments/assets/49087f6a-c42f-45ef-8432-3d9793129d63" />



