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



**Loss characterization**


**Crosstalk estimations**


**Quoting**



<img width="1107" height="257" alt="image" src="https://github.com/user-attachments/assets/c36eaf12-419a-498e-9522-740d7f5a260d" />

<img width="780" height="412" alt="image" src="https://github.com/user-attachments/assets/e5560622-15a3-4f4b-a12f-74a8d096a200" />

<img width="1103" height="525" alt="image" src="https://github.com/user-attachments/assets/078113b0-bf0b-4bd0-941c-a8f710a232f6" />

<img width="735" height="383" alt="image" src="https://github.com/user-attachments/assets/1795a6c5-f55d-49fa-91cd-4898e94a7fb4" />

# Layout

<img width="1180" height="857" alt="image" src="https://github.com/user-attachments/assets/2a90e0fe-653a-403d-8aaf-c53fe55d8f71" />

<img width="1174" height="855" alt="image" src="https://github.com/user-attachments/assets/49087f6a-c42f-45ef-8432-3d9793129d63" />



