
# Advanced Physical Design Workshop using OpenLane/Sky130

![](https://github.com/shobhit-mittra/vsd_pd_workshop/blob/main/images/cover_img_vsd.png?raw=true)


## Index 

1. [Overview](#overview)
2. [Pre-Requisites](#pre_req) 
3. [Installation](#inst)
4. [Day-1 : Inception of open-source EDA. OpenLANE and Sky130 PDK](#day1)
    - Fundamentals Learned :
        - [Exploring the Software-Hardware coupling](#hw-sw) 
        - [SoC using Open-Source Tools](#soc_os)
        - [Introduction to RTL-to-GDS2 flow](#rtl_gds2) 
        - [OpenLANE flow](#ol_flow)

    - Lab work :
        - [SkyWater PDKs](#sky_pdk)
        - [Initialising OpenLANE](#ini_ol)
        - [Importing Package](#im_pkg)
        - [Design Folder Hierarchy](#des_hier)
        - [Preparing Design](#prep_des)
        - [Running Synthesis](#run_syn)
        - [List of vital openLANE tool commands](#ol_cmd) 
          

5. [Day-2 : Floor-Planning and Introduction to Library Cells](#day2) 
    - Lab work :
        - [Viewing Floorplan and Placement Variables](#fp_pl)
        - [Running Floorplan](#run_fp)
        - [Invoking Magic to view generated Floorplan](#magic_fp)
        - [Running Placement and viewing it on magic](#magic_pl)
    

6. [Day-3 : Designing Library Cells using magic and ngspice tools](#day3) :
    - Lab work :
        - [Importing CMOS-Inveter Files](#import_inv)
        - [Inspecting CMOS-Inverter layout on magic](#magic_inv)
        - [Design Inference](#des_inf)
        - [Extracting SPICE from layout](#ext_spice)
        - [Updating SPICE Deck](#upd_spice)
        - [Running Updated SPICE on ngspice](#ngspice_inv)

7. [Day-4 : Pre-Layout Timing Analysis](#day4)
    - Lab work :
        - [Updating the inverter cell](#upd_inv)
        - [Generate LEF file](#gen_lef)
        - [Preparing and Running OpenLANE flow](#prep_ol)
        - [Pre-Layout STA](#pre_sta)
            - [Preparing for STA](#prep_sta)
            - [Invoking OpenSTA](#inv_sta)
            - [Slack Fixing](#fix_slack)
            - []()
            - []()
        - [Clock Tree Synthesis using TritonCTS](#cts)
        - [Invoking OpenROAD](#inv_or)
      
8. Day-5 : Final stages of RTL-to-GDS2 flow and closure 

9. Overall Experience 

10. Acknowledgements 
<br/>

## Segregation :
The repositry is organised as two seperate directories, one to archieve all the theory-based knowledge gained and the other for the lab work in the workshop. Hence, the division is as follows :
1. [Theory Work](Theory.md)
2. [Lab Work](Labs.md)


<a id="overview"></a>
## Overview

The workshop's goal is to provide fundamental knowledge about the ideas behind the Physical Design flow, an important part of the fundamental VLSI flow. Physical Design is broad topic and would require years to come close to mastering. Yet workshop attempts to convey the principles in a concise manner that is just enough to begin working on actual designs. The program is incredibly insightful and intriguing due to the way that concepts are coupled with the practical experience obtained through lab modules. 

This repository serves as an archive of all the knowledge I acquired and encountered during the session. I have utilised several snippets to demonstrate the ideas I gathered in the lectures and the outcomes of my lab module. The "images" branch compiles all of the illustrations used throughout in chronological order. 

I sincerely hope that anybody reading this discovers something new about physical design and is inspired to explore more about the domain.
<br/>  

<a id="pre_req"> </a>
## Pre-Requisites

### Technical :
- Ubuntu OS-based System
- 25GB+ Disk Space

### Non-Technical :
- Zeal to learn 
<br/>

<a id="inst"></a>
## Installation 

Visit the link : https://github.com/nickson-jose/openlane_build_script for installation steps







