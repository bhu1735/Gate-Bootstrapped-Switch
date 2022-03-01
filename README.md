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

R_ON=1/(μ_n C_ox (W/L)(V_GS-V_TH ) )  

However, such devices exhibit an input-dependent ON-resistance RON, thereby introducing distortion. Such switches are non-linear in nature and require modifications to linearize the switch. The only way the ON resistance of the switch is going to be constant is by making sure that the gate to source voltage VGS is constant for all values of input voltage. This technique is called “bootstrapping” that helps minimize the variation in RON with input voltage.  

Bootstrapping is a widely used technique in analog to digital converters (ADCs). In high speed ADCs, it is important to collect precise sample values in a very short time to get a digital output and ensure an accurate charging of the sampling capacitor. In this regards, a gate-bootstrapped switch was designed that uses Nakagome charge pump that acts as a voltage shifter or doubler.  

# Reference Circuit Details:  
The reference circuit has been shown in the figure below. It has been previously implemented in 0.6μm CMOS technology. The purpose of this research work is to implement the same in 28nm Synopsys iPDK library and analyze the outputs. Transient analysis has been done to check the efficacy of the aforementioned circuit. The results are shown in next section.  

![image](https://user-images.githubusercontent.com/88243788/156187307-394a1e18-47df-4b83-9dff-fc81e0db27da.jpg)

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


# Observations:

# Challenges:
Sizing of the transistors during the gate-boostrapped switch design was quite challenging to get the required waveforms.

# Limitations:

# Conclusions:

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
