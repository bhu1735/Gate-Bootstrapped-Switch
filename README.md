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
- M5: Used alongside switches M7 & M8 to ensure the capacitor C2 acts as a battery during track phase. During sampling, this switch will be closed. This can be implemented using CMOS switch because input VIN ranges from 0 to VDD. Another way is to use NMOS switch with gate connected to gate of M1 to provide the required boosted gate voltage.  
- M3: Used alongside switch M4 to ensure the capacitor C2 gets charged to VDD during hold phase. It can be implemented using NMOS because it is connecting C2 to ground.  
- M6: Used to provide protection to switch M7. This is because when M7   is OFF, it has a large drain-to-source voltage (VDS = VDD + VIN). This affects the reliability of the device and its lifetime will come down. M6 helps ease this by reducing VDS to a nominal value. It is implemented using NMOS because it is connected to VDD.  
- M6 and M7 provide the discharging path for node Vgate of M1 to ground.  
- M2 helps ensure that the node Vgate tracks the input voltage shifted by VDD thereby keeping Vgs across M1 constant.  
- C3: Used to act as a battery during track phase and to get charged during hold phase. It gets charged to VDD through transistors M9 and M10 during hold phase.  
- M11, M12, C1 and C2 form a clock multiplier known as Nakagome charge pump that ensures transistor M9 charges capacitor C3 during hold phase.


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

<p align="center">
  <img width="397" alt="Inv_circuit" src="https://user-images.githubusercontent.com/88243788/156240838-719de82f-a0a5-40f8-9564-adb715b44df3.png">  
</p>

The symbol for the same is shown below:  

<p align="center">
  <img width="370" alt="Inv_symbol" src="https://user-images.githubusercontent.com/88243788/156240915-072707b0-b19b-4cf8-9ce4-a16ea403986d.png">  
</p>

## Gate-Bootstrapped Switch:  
The schematic of gate-bootstrapped switch is as shown below:  

<p align="center">
  <img width="582" alt="Switch_circuit" src="https://user-images.githubusercontent.com/88243788/156240979-4f558412-c737-43b4-82ad-aaf6798f20bf.png">  
</p>

The symbol for the same is shown below:  

<p align="center">
  <img width="463" alt="Switch_symbol" src="https://user-images.githubusercontent.com/88243788/156241012-8ddcfb88-a7fd-4d50-84cc-2932e361e3cd.png">  
</p>

# Simulation Analysis:  
## Inverter:  
The testbench for the inverter is as shown below:  

<p align="center">
  <img width="524" alt="Inv_tb" src="https://user-images.githubusercontent.com/88243788/156241137-e9df7b5f-ed17-40ca-96a1-eeefe7d3f0c0.png">  
</p>

To test the functionality of the inverter, the parameter for the source at the input is shown below:  

<img width="148" alt="Inv_input" src="https://user-images.githubusercontent.com/88243788/156241173-471dd506-8ea6-4560-a35c-d61056abc64d.png">

The transient settings are shown below:  

<img width="341" alt="Inv_analysis" src="https://user-images.githubusercontent.com/88243788/156241257-8b5b46bd-81aa-40d1-b7c2-6456b180dcb5.png">

<img width="960" alt="Inv_analysis2" src="https://user-images.githubusercontent.com/88243788/156241338-fa97ed62-c905-4458-b392-3ce4924915f1.png">

The required waveforms generated are shown below:  

<img width="960" alt="Inv_results" src="https://user-images.githubusercontent.com/88243788/156241291-2c585b02-92d6-498a-ad24-ad63a0d9c914.png">

## Gate-Bootstrapped Switch:  
The testbench for the bootstrap switch is as shown below:  

<p align="center">
  <img width="434" alt="Switch_tb" src="https://user-images.githubusercontent.com/88243788/156241420-8917a9c8-c343-4905-9be7-cb27294de490.png">  
</p>

To test the functionality of the bootstrap switch, the parameters for the various sources are shown below:  

<img width="148" alt="Switch_vdc" src="https://user-images.githubusercontent.com/88243788/156241534-c72f221a-f13c-47a8-9817-8d3b2ecc75cd.png">

<img width="148" alt="Switch_clk" src="https://user-images.githubusercontent.com/88243788/156241570-c40b0c1c-dcd8-4bf3-8131-5829edacca74.png">

<img width="148" alt="Switch_input" src="https://user-images.githubusercontent.com/88243788/156241587-d68c98e9-9e0e-4340-919d-077885bfb660.png">

The transient settings are shown below:  

<img width="340" alt="Switch_analysis" src="https://user-images.githubusercontent.com/88243788/156241645-39a9280e-4e0a-47d5-8748-56c2b37cfdf7.png">

The required waveforms generated are shown below:  

<img width="960" alt="Switch_results" src="https://user-images.githubusercontent.com/88243788/156241680-981ca1c8-7282-408f-b106-1f5bb7baab8d.png">

One can zoom in to see how accurately the output tracks the input as shown below:  

<img width="960" alt="Switch_results2" src="https://user-images.githubusercontent.com/88243788/156241699-6334ea99-0d62-4821-8d82-90f5eb566ead.png">

<img width="960" alt="Switch_results3" src="https://user-images.githubusercontent.com/88243788/156241723-3bee03f0-ebfe-403e-98f8-6b12a150c8ff.png">

# Netlist:  
The netlist for inverter can be found here: [Netlist_Inverter.txt](https://github.com/bhu1735/Gate-Bootstrapped-Switch/files/8164538/Netlist_Inverter.txt)  

The netlist for gate-boostrapped switch can be found here: [Netlist_Switch.txt](https://github.com/bhu1735/Gate-Bootstrapped-Switch/files/8164545/Netlist_Switch.txt)  

# Observations:  
As can be observed from the simulations plots, the circuit switch tracks the input signal during one-half of clock cycle and holds the value during other half which was expected from theory. Further, as we zoom into the plots, we observed that the pedestial error is very low (of the order of few 100uV) but there is a time lag between the input signal and output track signal (of the order of nano-seconds). This may be due to the parasitic elements present in the design. Increasing the width of the sampling gate helps reduce the time lag between the input and output. On other hand, the pedestial error can be reduced by increasing load/hold capacitance CH at the cost of reduced bandwidth.  

# Challenges:  
Some challenges associated with the bootstrapped switch are:  
1) Sizing of the transistors during the gate-boostrapped switch design was quite challenging to get the required waveforms.  
2) Charge Injection: When clock is goes from HIGH to LOW, the charge that was present in the channel (when clock was HIGH), escapes to the source and drain side of the switch M1. So, some amount of charge will get deposited on the hold capacitance CH. This causes change in the actual voltage of the capacitor that is meant to be digitized as additional charges (due to charge leakage) get deposited on CH. One can use a dummy switch in series to M1 to reduce this affect. The dummy switch and M1 operate with out-of-phase clocks.  
3) Clock Feedthrough: During clock transition from HIGH to LOW, there is some overlap capacitance between gate and drain. This capacitance Cov forms a voltage divider with CH which again causes change in the actual voltage of the capacitor output. Different voltage value gets digitized due to clock transitions.  

NOTE: By increasing the capacitance CH, one can mitigate the above two affects at the cost of reduced bandwidth.  

# Summary:  
As a part of this cloud-based analog ic design hackathon, a gate-boostrapped switch has been designed using 28nm Synopsys iPDK library. The output tracks the input waveform during one-half of the clock cycle ('HIGH') and holds the value during other half ('LOW'). However, there is a time lage between the input and output. We discussed some challenges associated with the design and the measures that one may take to mitigate the same. Netlist has also been generated for the bootstrap switch design.

# Acknowledgement:  
1) I would like to express my thanks of gratitude to Mr. Kunal Ghosh (Co-founder [VSD](https://www.vlsisystemdesign.com/) Corp. Pvt. Ltd.), for providing me an opportunity to partake in this hackathon and help understand VLSI design flow process both theoritically and practically.  
2) [Cloud Based Analog IC Design Hackathon](https://www.iith.ac.in/events/2022/02/15/Cloud-Based-Analog-IC-Design-Hackathon/)    
3) I would like to thank [Synopsys](https://www.synopsys.com/) Team/Company for providing access to the server and 28nm iPDK CMOS library for implementing the design.
4) I would also like to thank Mr. Sameer Durgoji, NIT Karnataka and Mr. Chinmay Panda, IIT Hyderabad for providing necessary video tutorials to use Synopsys custom compiler with ease.  
5) Lastly, I appreciate the TAs for clarifying my doubts without whom this work would not have been made presentable.  

# References:  
1) A. M. Abo and P. R. Gray, "A 1.5-V, 10-bit, 14.3-MS/s CMOS pipeline analog-to-digital converter," in IEEE Journal of Solid-State Circuits, vol. 34, no. 5, pp. 599-606, May 1999.  
2) D. Aksin, M. Al-Shyoukh and F. Maloberti, "Switch Bootstrapping for Precise Sampling Beyond Supply Voltage," in IEEE Journal of Solid-State Circuits, vol. 41, no. 8, pp. 1938-1943, Aug. 2006  
3) B. Razavi, “The Bootstrapped Switch [A Circuit for All Seasons]”, in IEEE Solid-State Circuits Magazine, vol. 7, no. 3, pp. 12-15, Summer 2015  
