# GATE-BOOTSTRAPPED SWITCH USING 28nm SYNOPSYS iPDK

# DESCRIPTION:  
In the current era of information, analog domain has become a challenging and an important part of IC design. Almost all electronic systems are susceptible to noise and mismatch. Hence, it is important to understand the importance of analog design aspects. In this regard, a 2-week online cloud-based analog IC design hackathon by IITH and VSD-IAT supervised by Synopsys India was conducted from 15th February, 2022 to 1st March, 2022. The hackathon required the VLSI enthusiasts to understand and design an analog circuit of their choice using cloud-based server. Using Synopsys custom compiler and 28nm CMOS PDK, a gate-bootstrapped switch for sample and hold circuit was designed. Basic understanding of electric circuits is beneficial for a beginner.

# CONTENTS:
- [Abstract](#abstract)  
- [Introduction](#introduction)  
- [Reference Circuit Details](#reference-circuit-details)  
- [Reference Circuit Waveforms](#reference-circuit-waveforms)  
- [Tools Used](#tools-used)  
- [Pre-Layout Schematics](#pre-layout-schematics)  
  - [Inverter](#inverter)  
  - [Gate-Boostrapped Switch](#gate-boostrapped-switch)  
- [Simulation Analysis](#simulation-analysis)  
  - [Inverter](#inverter)  
  - [Gate-Boostrapped Switch](#gate-boostrapped-switch)  
- [Netlist](#netlist)
- [Observations](#observations)
- [Limitations](#limitations)
- [Summary](#summary)  
- [Acknowledgement](#acknowledgement) 
- [References](#references) 
  

# Abstract:  
Switches form one of the main building blocks of many analog systems. They help to track and hold values of input continuous time data that is then analyzed digitally. In this paper, we have designed a gate bootstrapped switch for a sample and hold circuit using 28nm Synopsys iPDK.  

# Introduction:  
Since 1950s, transistors have been used as switches in analog circuits. They find a wide variety of applications including DC-DC converters, analog to digital data converters, etc. To operate as a switch, transistors should intend to work in triode region. In triode region, the ON-resistance of transistor is defined as,  

<p align="center">
  <img width="168" alt="Equation" src="https://user-images.githubusercontent.com/88243788/156207030-c2d50d27-ac09-4262-8e72-2c4f52c40df0.PNG">  
</p>

However, such devices exhibit an input-dependent ON-resistance RON, thereby introducing distortion. Such switches are non-linear in nature and require modifications to linearize the switch. The only way the ON resistance of the switch is going to be constant is by making sure that the gate to source voltage VGS is constant for all values of input voltage. This technique is called “bootstrapping” that helps minimize the variation in RON with input voltage.  

Bootstrapping is a widely used technique in analog to digital converters (ADCs). In high speed ADCs, it is important to collect precise sample values in a very short time to get a digital output and ensure an accurate charging of the sampling capacitor. In this regards, a gate-bootstrapped switch was designed that uses Nakagome charge pump that acts as a voltage shifter or doubler.  

# Reference Circuit Details:  
The reference circuit has been shown in the figure below. It has been previously implemented in 0.6μm CMOS technology. The purpose of this research work is to implement the same in 28nm Synopsys iPDK library and analyze the outputs. Transient analysis has been done to check the efficacy of the aforementioned circuit. The results are shown in next section.  

![image](https://user-images.githubusercontent.com/88243788/156187307-394a1e18-47df-4b83-9dff-fc81e0db27da.jpg)

The role of various transistors has been specified below:  
- Clk: Track/sample phase. When Clk is HIGH, the capacitor C3 acts as a battery.  
- Clk_bar: Hold phase  
- M1: Main sampling switch  
- M2: Used alongside switches M5 & M6 to ensure the capacitor C2 acts as a battery during track phase. During sampling, this switch will be closed. This can be implemented using CMOS switch because input VIN ranges from 0 to VDD. Another way is to use NMOS switch with gate connected to gate of M1 to provide the required boosted gate voltage.  
- M3: Used alongside switch M4 to ensure the capacitor C2 gets charged to VDD during hold phase. It can be implemented using NMOS because it is connecting C2 to ground.  
- M4: Implemented using PMOS because it is connected to VDD. Its gate terminal is connected to VG to ensure the switch is OFF during track phase.  
- M5: Implemented using PMOS because it is connected to VDD.  
- M6: Implemented using NMOS because it is connected to VDD.  
- M7: Used to provide protection to switch M6. This is because when M6 is OFF, it has a large drain-to-source voltage (VDS = VDD + VIN). This affects the reliability of the device and its lifetime will come down. M6 helps ease this by reducing VDS to a nominal value.  
- C3: Used to act as a battery during track phase and to get charged during hold phase.  


# Reference Circuit Waveforms:  

![image](https://user-images.githubusercontent.com/88243788/156188181-747c895a-17e4-411b-8be4-4f1efd482f78.jpg)

As can be seen in the waveforms above, the output waveform tracks the input in half the clock cycle duration and holds the sampled value in other half clock cycle.  

# Tools Used:  
Following are the tools used for the design during the hackathon:
1) Synopsys Custom Compiler
2) Synopsys Prime Wave for simulations
3) 28nm iPDK library provided by Synopsys India

We shall now look into the circuit schematics of above design and simulate it using 28nm iPDK library.  

# Pre-Layout Schematics:  
## Inverter:  
The schematic of inverter is as shown below:  

The symbol for the same is shown below:  

## Gate-Bootstrapped Switch:  
The schematic of gate-bootstrapped switch is as shown below:  

The symbol for the same is shown below:  

# Simulation Analysis:  
## Inverter:  
To test the functionality of the inverter, the parameter for the souce at the input is shown below:  

The transient setting are shown below:  

The required waveforms generated are shown below:  

## Gate-Bootstrapped Switch:  
To test the functionality of the inverter, the parameter for the souce at the input is shown below:  

The transient setting are shown below:  

The required waveforms generated are shown below:  

# Netlist:  
*  Generated for: PrimeSim
*  Design library name: Bootstrapped_Switch
*  Design cell name: Track_Hold_new_tb
*  Design view name: schematic
.lib '/PDK/SAED_PDK32nm/hspice/saed32nm.lib' TT

*Custom Compiler Version S-2021.09
*Tue Mar  1 17:54:10 2022

.global gnd!
********************************************************************************
* Library          : Bootstrapped_Switch
* Cell             : Inverter
* View             : schematic
* View Search List : hspice hspiceD schematic spice veriloga
* View Stop List   : hspice hspiceD
********************************************************************************
.subckt inverter in out
xm0 out in gnd! gnd! n105 w=0.1u l=0.03u nf=1 m=1
xm1 out in net9 net9 p105 w=0.25u l=0.03u nf=1 m=1
v2 net9 gnd! dc=1.05
.ends inverter

********************************************************************************
* Library          : Bootstrapped_Switch
* Cell             : Track_Hold_new
* View             : schematic
* View Search List : hspice hspiceD schematic spice veriloga
* View Stop List   : hspice hspiceD
********************************************************************************
.subckt track_hold_new clk vdd vin vout
xm12 vdd net6 net5 net5 n105 w=0.1u l=0.03u nf=1 m=1
xm11 vdd net5 net6 net6 n105 w=0.1u l=0.03u nf=1 m=1
xm10 net2 clk_bar gnd! gnd! n105 w=0.175000m l=0.03u nf=50 m=1
xm9 vdd net5 net3 net3 n105 w=0.15u l=0.03u nf=1 m=1
xm7 net1 clk_bar gnd! gnd! n105 w=0.1u l=0.03u nf=1 m=1
xm6 vgate vdd net1 net1 n105 w=0.1u l=0.03u nf=1 m=1
xm4 net4 clk net2 net2 n105 w=0.1u l=0.03u nf=1 m=1
xm2 vin vgate net2 net2 n105 w=0.1u l=0.03u nf=1 m=1
xm1 vout vgate vin vin n105 w=0.1u l=0.03u nf=1 m=1
xm3 net4 vgate net2 net2 n105 w=0.1u l=0.03u nf=1 m=1
xm8 vgate net4 net3 net3 p105 w=0.15u l=0.03u nf=1 m=1
xm5 net4 clk vdd vdd p105 w=0.25u l=0.03u nf=1 m=1
c15 net3 net2 c=10p
c14 net5 clk_bar c=1p
c13 net6 net7 c=1p
xi21 clk_bar net7 inverter
xi20 clk clk_bar inverter
.ends track_hold_new

********************************************************************************
* Library          : Bootstrapped_Switch
* Cell             : Track_Hold_new_tb
* View             : schematic
* View Search List : hspice hspiceD schematic spice veriloga
* View Stop List   : hspice hspiceD
********************************************************************************
xi0 clk net7 vin vout track_hold_new
v2 clk gnd! dc=0 pulse ( 0 1.05 2.5u 40p 40p 2.5u 5u )
v3 vin gnd! dc=0 sin ( 0.525 0.525 10k 0 0 0 )
v1 net7 gnd! dc=1.05
c4 vout gnd! c=5p








.tran '1u' '200u' name=tran

.option primesim_remove_probe_prefix = 0
.probe v(*) i(*) level=1
.probe tran v(clk) v(vin) v(vout)

.temp 25



.option primesim_output=wdf


.option parhier = LOCAL






.end




*  Generated for: PrimeSim
*  Design library name: Bootstrapped_Switch
*  Design cell name: Inverter_tb
*  Design view name: schematic
.lib '/PDK/SAED_PDK32nm/hspice/saed32nm.lib' TT

*Custom Compiler Version S-2021.09
*Tue Mar  1 18:21:21 2022

.global gnd!
********************************************************************************
* Library          : Bootstrapped_Switch
* Cell             : Inverter
* View             : schematic
* View Search List : hspice hspiceD schematic spice veriloga
* View Stop List   : hspice hspiceD
********************************************************************************
.subckt inverter in out
xm0 out in gnd! gnd! n105 w=0.1u l=0.03u nf=1 m=1
xm1 out in net9 net9 p105 w=0.25u l=0.03u nf=1 m=1
v2 net9 gnd! dc=1.05
.ends inverter

********************************************************************************
* Library          : Bootstrapped_Switch
* Cell             : Inverter_tb
* View             : schematic
* View Search List : hspice hspiceD schematic spice veriloga
* View Stop List   : hspice hspiceD
********************************************************************************
xi0 in out inverter
v1 in gnd! dc=0 pulse ( 0 1.05 0 0.1u 0.1u 5u 10u )
c2 out gnd! c=1p








.tran '1u' '20u' name=tran

.option primesim_remove_probe_prefix = 0
.probe v(*) i(*) level=1
.probe tran v(in) v(out)

.temp 25



.option primesim_output=wdf


.option parhier = LOCAL






.end



# Observations:  
As can be observed from the simulations plots, the circuit switch tracks the input signal during one-half of clock cycle and holds the value during other half which was expected from theory.  

# Challenges:  
Some challenges associated with the bootstrapped switch are:  
1) Sizing of the transistors during the gate-boostrapped switch design was quite challenging to get the required waveforms.  
2) Charge Injection: When clock is goes from HIGH to LOW, the charge that was present in the channel (when clock was HIGH), escapes to the source and drain side of the switch M1. So, some amount of charge will get deposited on the hold capacitance CH. This causes change in the actual voltage of the capacitor that is meant to be digitized as additional charges (due to charge leakage) get deposited on CH. One can use a dummy switch in series to M1 to reduce this affect. The dummy switch and M1 operate with out-of-phase clocks.  
3) Clock Feedthrough: During clock transition from HIGH to LOW, there is some overlap capacitance between gate and drain. This capacitance Cov forms a voltage divider with CH which again causes change in the actual voltage of the capacitor output. Different voltage value gets digitized due to clock transitions.  

NOTE: By increasing the capacitance CH, one can mitigate the above two affects at the cost of reduced bandwidth.  

# Limitations:  

# Conclusions:  
As a part of this cloud-based analog ic design hackathon, a gate-boostrapped switch has been designed using 28nm Synopsys iPDK library. The output tracks the input waveform during one-half of the clock cycle and holds the value during other half.  

# Acknowledgement:  
1) I would like to express my thanks of gratitude to Mr. Kunal Ghosh (Co-founder [VSD](https://www.vlsisystemdesign.com/) Corp. Pvt. Ltd.), for providing me an opportunity to partake in this hackathon and help understand VLSI design flow process both theoritically and practically.  
2) [Cloud Based Analog IC Design Hackathon](https://www.iith.ac.in/events/2022/02/15/Cloud-Based-Analog-IC-Design-Hackathon/)    
3) I would like to thank [Synopsys](https://www.synopsys.com/) Team/Company for providing access to the server and 28nm iPDK CMOS library for implementing the design.
4) I would also like to thank Mr. Sameer Durgoji, NIT Karnataka and Chinmay Panda, IIT Hyderabad for providing necessary video tutorials to use Synopsys custom compiler with ease.  
5) Lastly, I appreciate the TAs for clarifying my doubts without whom this work would not have been made presentable.  

# References:  
1) A. M. Abo and P. R. Gray, "A 1.5-V, 10-bit, 14.3-MS/s CMOS pipeline analog-to-digital converter," in IEEE Journal of Solid-State Circuits, vol. 34, no. 5, pp. 599-606, May 1999.  
2) D. Aksin, M. Al-Shyoukh and F. Maloberti, "Switch Bootstrapping for Precise Sampling Beyond Supply Voltage," in IEEE Journal of Solid-State Circuits, vol. 41, no. 8, pp. 1938-1943, Aug. 2006  
3) B. Razavi, “The Bootstrapped Switch [A Circuit for All Seasons]”, in IEEE Solid-State Circuits Magazine, vol. 7, no. 3, pp. 12-15, Summer 2015  
