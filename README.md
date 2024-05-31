
# Advanced Physical Design Workshop using OpenLane/Sky130

![](https://github.com/shobhit-mittra/vsd_pd_workshop/blob/main/images/cover_img_vsd.png?raw=true)


## Index 

- [Overview](#overview)
- [Pre-Requisites](#pre_req) 
- [Installation](#inst)
- [Day-1 : Inception of open-source EDA. OpenLANE and Sky130 PDK](Theory/Day1.md)
- [Day-2 : Floor-Planning and Introduction to Library Cells](Theory/Day2.md)
- [Day-3 : Designing Library Cells using magic and ngspice tools](Theory/Day3.md)
- [Day-4 : Pre-Layout Timing Analysis](Theory/Day4.md)
- [Day-5 : Final stages of RTL-to-GDS2 flow and closure](Theory/Day5.md) 

- Overall Experience 

- Acknowledgements 
<br/>

## Segregation :
The repositry is organised as two seperate directories, one to archieve all the theory-based knowledge gained and the other for the lab work in the workshop. Hence, the division is as follows :
1. [Theory Work](Theory.md)
2. [Lab Work](Lab.md)
<br/>

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
- Python 3.6 or higher
  - On Ubuntu, you may also need to install venv: `apt-get install python3-venv`


### Non-Technical :
- Zeal to learn 

<a id="inst"></a>
## Installation (updated)
[ Picked from the documentation of openLane : https://openlane.readthedocs.io/en/latest/getting_started/installation/installation_ubuntu.html#installation-of-required-packages ]
```
git clone --depth 1 https://github.com/The-OpenROAD-Project/OpenLane.git
cd OpenLane/
make
make test
```
This will install the openlane and sky130 pdk. If you get an error related to PDK not found ( [ERRoR] : Failed to compare PDKs ), then try running `make pdk`. This might generate an error that may be related to insufficient permissions for `.volare` folder. You may change the permissions of the .volare folder path as seen in  your error message in the terminal and then re-try by running `make pdk`. If the permissions are not getting changed you may use `sudo` and try again. If everything goes well, you will observe the pdks getting installed sequentially. 

After the pdks are installed you may try running `make test` that will run a ~5 minute test that verifies that the flow and the PDK were properly installed. 
Successful output generated is as under :
```
Basic test passed
```






