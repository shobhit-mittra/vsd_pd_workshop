
# Advanced Physical Design Workshop using OpenLane/Sky130

![](https://github.com/shobhit-mittra/vsd_pd_workshop/blob/main/images/cover_img_vsd.png?raw=true)




## Index 

1. [Overview](#overview)
2. [Pre-Requisites](#pre_req) 
3. [Installation](#inst)
4. [Day-1 : Inception of open-source EDA. OpenLANE and Sky130 PDK](#day1)
    - Fundamentals Learned :
        - [Exploring the Software-Hardware coupling](#hw-sw) 
        - [SoC using OpenLANE](#soc_ol)
        - [Introduction to RTL-to-GDS2 flow](#rtl_gds2) 
        - [OpenLANE flow](#ol_flow)

    - Lab work :
        - Preparing for design
        - Running Sythesis and reviewing generated files
        - List of vital openLANE tool commands 
        - Characterizing synthesis results

5. [Day-2 : Floor-Planning and Introduction to Library Cells](#day2) 
    - Fundamentals Learned :
        - con 1 
        - con 2
        - concept 3 
        - concept 4

    - Lab work :
        - act1
        - act 2
        - act 3
        - act 4

6. Day-3 : Designing Library Cells using magic and ngspice tools
    - Fundamentals Learned :
        - con 1 
        - con 2
        - concept 3 
        - concept 4

    - Lab work :
        - act1
        - act 2
        - act 3
        - act 4

7. Day-4 : Pre-Layout Timing Analysis

8. Day-5 : Final stages of RTL-to-GDS2 flow and closure 

9. Overall Experience 

10. Acknowledgements 

<a id="overview"></a>
## Overview

The workshop's goal is to provide fundamental knowledge about the ideas behind the Physical Design flow, an important part of the fundamental VLSI flow. Physical Design is broad topic and would require years to come close to mastering. Yet workshop attempts to convey the principles in a concise manner that is just enough to begin working on actual designs. The program is incredibly insightful and intriguing due to the way that concepts are coupled with the practical experience obtained through lab modules. 

This repository serves as an archive of all the knowledge I acquired and encountered during the session. I have utilised several snippets to demonstrate the ideas I gathered in the lectures and the outcomes of my lab module. The "images" branch compiles all of the illustrations used throughout in chronological order. 

I sincerely hope that anybody reading this discovers something new about physical design and is inspired to explore more about the domain.
  

<a id="pre_req"> </a>
## Pre-Requisites

### Technical :
- Ubuntu OS-based System
- 25GB+ Disk Space

### Non-Technical :
- Zeal to learn 

<a id="inst"></a>
## Installation 

Visit the link : https://github.com/nickson-jose/openlane_build_script for installation steps

<a id="day1"></a>
## Day-1 : Inception of open-source EDA. OpenLANE and Sky130 PDK

The workshop's primary goal on the first day was to familiarise us with the foundational ideologies outlined below in order to lay the groundwork for the days to come.

<a id="hw-sw"></a>
### Exploring the Software-Hardware coupling :

The most commonly used application software or apps such as Microsoft Word, Excel, Powerpoint etc. run on a system i.e the hardware which is essentially a combination of multiple components making up the chip. Hene there exists an elaborate pathway that ensues the communication between the hardaware and the software applications. The illustration below showcases the hardware-software coupling : 

![Hardware-Software Coupling](/images/hw-sw_coupling.png)

As it is evident in the illustration above, there lies an elaborate pathway for the communication between hardware and software. To briefly explain this pathway:

- The application requires an operating system to run on such as linux, MacOs, Windows etc. OS performs numerous tasks involving managment of memories and background processes. In this context, the OS job is to convert the software application into it's respective assembly language and further onto binary(machine language).

- Evidentally, the output of an OS is a simple C/C++/Java or other high-level language.

- The compiler then, uses the source files generated through the high-level language to create object files. These object files contain the **Instruction Sets** whose syntax is specific to the architecture of the chip of the system. eg : 8086 instruction sets, RISC-V instruction sets etc.

- These instruction sets are interpreted by the Assembler and is used to finally generate machine language program that contains 0s and 1s in the form of operation-code or **op-code** in short. These op=code are understood by the chip and directs the hardware to perform the task in order to generate desired results.

<br/>

The flow can be visualized in a better way via an example :
> Let us take an instance of operating a basic Stop-Watch app.
>> Re-tracing the flow from the beginning the output of the OS could look something like under :
>> 
>> ![o/p of OS eg](/images/os_op_eg.png)
>>
>> ###### *A simple C-program capturing the behaviour of stop-watch app.*
>> 
>> The compiler processes this code to generate the instruction set specific to the chip being used. In this workshop we would be focusing on "picorv32a" core, hence the instruction set would follow the RISC-V Architecture. The illustration below showcases the sample generated compiler :
>>
>> ![compiler_op_eg](/images/compiler_op_eg.png)
>> 
>> The instruction set from compiler are then taken by the assembler to generate a machine language program that is interpreted by the chip.
>>
>> ![assembler_op_eg]()
>>
>> As observed in the snippet above, the assembler converts the sample instruction *"add x6,x10,x6"* (that essentially means adding the contents of registers *x6* and *x10* and putting the result into *x6* register) into an op-code that can be implemented by the hardware.
>>
> [!NOTE]
> From this basic example discussed above, it is clear that the *Instruction-Set* acts as an interface between the communication of hardware and software and hence it is also termed as *Abstract Interface*.
    

<a id="soc_ol"></a>
### SoC using OpenLANE : 




<a id="rtl_gds2"></a>
### Introduction to RTL-to-GDS2 flow : 




<a id="ol_flow"></a>
### OpenLANE flow : 



